---
theme: seriph
favicon: /images/otel-logo.png
background: /images/stars.avif
class: text-center
transition: slide-left
title: Opentelemetry
titleTemplate: OpenTelemetry - vmaleze
mdc: true
hideInToc: true
---

<h1 class="absolute-center z-1 w-5/6 ">OpenTelemetry: vous ne pourrez plus vous passer de monitoring en prod</h1>
<img src="/images/otel-logo.png" class="absolute-center op-60 z-0"/>


---
title: About Me
layout: about-me
hideInToc: true
speakerName: Vivien MALEZE
speakerTitle: Technical Architect
speakerImage: /images/profile_cropped.jpeg
speakerCompanyLogo: /images/ippon.png
---

::details::

* Background java <logos-java />
* +10 ans d'xp
* +6 ans chez Ippon
* Bordeaux, France 🇫🇷
* Sujets du moments
    * Microservices <logos-kubernetes />
    * DevOps 🛠️

* <logos-twitter /> <logos-github-octocat />@vmaleze

---
layout: image-blur
image: /images/default-architecture.png
imageHeight: h-3/5
contentClass: text-4xl
---

::header::
# Pourquoi monitorer ?

::content::
<v-clicks>

* Connaitre son système
* Dimensionner
* Alerter
* Anticiper

</v-clicks>

---
title: Logs
layout: image
image: /images/logs.webp
---

<h1 class="over-image w-30">Logs</h1>

---
title: Metrics
layout: image
image: /images/metrics.webp
---

<h1 class="over-image w-42">Metrics</h1>

---
title: Tracing
layout: image
image: /images/distributed-tracing.png
---

<h1 class="over-image w-39">Traces</h1>


---
layout: two-cols-header
---

# C'est quoi OpenTelemetry ?

::left::

<v-click>

# C'est <uil-check color="green" />

</v-click>
<v-clicks>

* Un projet open-source
* Un framework d'observabilité  
* Un outil de collecte de données
* Un standard dans le monde du monitoring
* Une intégration dans la plupart des langages du marché

</v-clicks>

::right::

<v-click>

# Ce n'est pas <uil-times color="red" />

</v-click>
<v-clicks>

* Un outil tout en un comme datadog ou dynatrace
* Un backend de traitement de donnée
</v-clicks>

---
layout: image-blur
image: /images/one-ring.png
imageHeight: h-1/2
contentClass: text-2xl
---

::header::
# Pourquoi faire ?

::content::
<v-clicks>

* Un outil unique
* Pas besoin de changer son code si on change d'outil
* Simplifier l'instrumentation

</v-clicks>

---
layout: default
transition: slide-up
---

# Et comment on instrumente ?

<logos-java v-click class="text-8xl mt-10" />
<div v-after>
```java
//opentelemetry spring auto-configuration
implementation("io.opentelemetry.instrumentation:opentelemetry-spring-boot:OTEL_VERSION")
//opentelemetry
implementation("io.opentelemetry:opentelemetry-api:OTEL_VERSION")
//opentelemetry exporter
implementation("io.opentelemetry:opentelemetry-exporters-otlp:OTEL_VERSION")
```
</div>

---
title: Docker instrumentation
layout: default
---

<logos-docker class="text-9xl center" />

<div>

```docker
FROM openjdk:17

RUN mkdir -p /app/bin

ADD https://github.com/open-telemetry/opentelemetry-java-instrumentation/
    releases/latest/download/opentelemetry-javaagent.jar 
    /app/bin/opentelemetry-javaagent.jar
COPY target/*.jar /app/bin/app.jar

CMD java -javaagent:/app/bin/opentelemetry-javaagent.jar \
    -jar /app/bin/app.jar
```
</div>

---
layout: default
---

# Comment ça marche ?

<img class="flex justify-center mt-4rem" src="/images/how-it-works.png" />

---
layout: default
transition: fade
---

# Vers où exporte les données ?
Vers les backend directement

|                                                                                   |                               |
| --------------------------------------------------------------------------------- | ----------------------------- |
| <kbd>OTEL_SERVICE_NAME</kbd>                                                      | Nom du service                |
| <kbd>OTEL_TRACES_EXPORTER</kbd> / <kbd>OTEL_EXPORTER_OTLP_TRACES_ENDPOINT</kbd>   | Export des traces distribuées |
| <kbd>OTEL_METRICS_EXPORTER</kbd> / <kbd>OTEL_EXPORTER_OTLP_METRICS_ENDPOINT</kbd> | Export des metrics            |
| <kbd>OTEL_LOGS_EXPORTER</kbd> / <kbd>OTEL_EXPORTER_OTLP_LOGS_ENDPOINT</kbd>       | Export des logs               |

---
layout: default
---

# Vers où exporte les données ?
Vers un collecteur opentelemetry

<div class="mt-4rem">

|                                   |                          |
| --------------------------------- | ------------------------ |
| <kbd>OTEL_SERVICE_NAME</kbd>      | Nom du service           |
| <kbd>OTEL_EXPORTER_OTLP_ENDPOINT</kbd> | Collecteur opentelemetry |

</div>

---
title: Architecture collecteur OpenTelemetry
layout: image
image: /images/otel-collector-archi.png
---

---
layout: image
image: /images/orc.png
---

# Au travail

---
layout: default
---

# On ajoute quoi au cluster ?

<div class="text-lg mt-5rem">

|                                   |                          |
| --------------------------------- | ------------------------ |
| <kbd>Operator</kbd>      | Manage les resources OpenTelemetry via les CRDs k8s           |
| <kbd>Collector</kbd> | Reçoit et exportes les données |
| <kbd>Auto Instrumentation</kbd> | Injecte l’agent java directement dans le conteneur docker |

</div>

---
layout: two-cols-three-span
classRight: col-span-2 overflow-auto
clicks: 4
highlighter: shiki
---

# Le collecteur
Déploiement et configuration

<div class="mt-2rem">

<v-clicks>

* Mode de déploiement
  * Sidecar
  * Daemonset
* Collecte des données
  * Push / Pull
* Export des données
  * Liste des différents backend
  * Exposition de données
* Config des différentes services

</v-clicks>
</div>

::right::

```yaml {1-15|6|9-13|17-25|27-36} {lines:true, at:0, maxHeight:'full'}
apiVersion: opentelemetry.io/v1alpha1
kind: OpenTelemetryCollector
metadata:
  name: otel-sidecar
spec:
  mode: sidecar
  config: |

    receivers:
      otlp:
        protocols:
          grpc:
          http:
    processors:
      batch:

    exporters:
      loki:
        endpoint: http://loki.monitoring:3100/loki/api/v1/push
      otlp/tempo:
        endpoint: tempo.monitoring:4317
        tls:
          insecure: true
      prometheus:
        endpoint: "0.0.0.0:8889"

    service:
      pipelines:
        traces:
          receivers: [otlp]
          processors: [batch]
          exporters: [otlp/tempo]
        metrics:
          receivers: [otlp]
          processors: [batch]
          exporters: [prometheus]
```

---
layout: default
---

# Injection de l'agent
Auto Instrumentation

<div class="mt-6rem">

```yaml {lines:true}
apiVersion: opentelemetry.io/v1alpha1
kind: Instrumentation
metadata:
  name: otel-auto-instrumentation
spec:
  exporter:
    endpoint: http://0.0.0.0:4317
```

</div>

---
layout: default
clicks: 2
---

# On applique ça sur le déploiement


<div class="mt-6rem">

<v-clicks at="0">

* Ajout du sidecar
* Injection de l'agent java

</v-clicks>

```yaml {all|4|5} {lines:true, at:0, maxHeight:'full'}
template:
  metadata:
    annotations:
      sidecar.opentelemetry.io/inject: "true"
      instrumentation.opentelemetry.io/inject-java: "true"
```

</div>

---
title: Logs & trace
layout: image
image: /images/it-crowd.jpeg
---

<div class="h-full grid place-content-center">

<h1 class="!text-white !text-7xl"> Et c'est parti ! </h1>

</div>

---
title: Products
layout: iframe
url: http://localhost:8081/swagger-ui/index.html
---

---
title: Stocks
layout: iframe
url: http://localhost:8082/swagger-ui/index.html
---

---
title: Shopping Cart
layout: iframe
url: http://localhost:8083/swagger-ui/index.html
---

---
title: Order
layout: iframe
url: http://localhost:8084/swagger-ui/index.html
---

---
title: Grafana
layout: iframe
url: http://localhost:3000
---

---
title: Derrière tout ça
layout: image
image: /images/minions.webp
---

# Y'a quoi derrière tout ça ?

---
layout: image-blur
image: /images/tempo.png
imageHeight: h-1/2
contentClass: text-2xl
---

::header::
# Pour les traces
Tempo

::content::

<v-clicks>

* Outil de gestion des traces distribuées
* Basé sur le standard opentelemetry
* Compatible avec les formats open source
  * Zipkin
  * Jaeger
* Integration poussée avec grafana

</v-clicks>

---
layout: image-blur
image: /images/loki.png
imageHeight: h-1/2
contentClass: text-2xl
---

::header::
# Pour les logs
Loki

::content::
<v-clicks>

* Outil d'aggregation de logs
* Parse les entrèes pour en extraire les informations importantes
  * Dates
  * Erreurs
  * Traces
* Basé sur un collecteur de logs tels que
  * FluentBit / FluentD
  * FileLogReceiver

</v-clicks>

---
layout: image-blur
image: /images/prometheus.png
imageHeight: h-1/2
contentClass: text-2xl
---

::header::
# Pour les metrics
Prometheus

::content::

<v-clicks>

* Système de monitoring et d'alerting basé sur des metrics
* *Scrape* les données plutôt que de les recevoir
* Gère les données grace a une format basé sur les time-series

</v-clicks>
