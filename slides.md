---
theme: seriph
colorSchema: light
favicon: /images/platform_engineering_org_logo.png
background: /images/plateforme.jpg
class: text-center
transition: slide-left
title: L'observabilité au coeur de ta plateforme
titleTemplate: Observability - Ippon
mdc: true
hideInToc: true
---

# L'observabilité au coeur de ta plateforme

---
title: IceBreaker
layout: default
---

# Kids

<v-clicks>

<img src="/images/kid-paint.jpeg" class="absolute-center w-1/2 rotate-10 z-0"/>
<img src="/images/kid-hair.jpeg" class="absolute-center w-1/2 -rotate-10 z-1"/>
<img src="/images/kids-jumping.jpeg" class="absolute-center z-2"/>

</v-clicks>

---
title: About Vivien
layout: about-me
hideInToc: true
speakerName: Vivien MALEZE
speakerTitle: Technical Architect
speakerImage: /images/vivien-speaker.jpeg
speakerCompanyLogo: /images/ippon.png
---

::details::

* Background java <logos-java />
* +12 ans d'xp
* +7 ans chez Ippon
* Bordeaux, France 🇫🇷
* Sujets du moment
  * Developer Experience <logos-kubernetes />
  * Platform Engineering 🛠️
* <logos-twitter /> <logos-github-octocat />@vmaleze

---
title: Monitoring
layout: image
image: /images/monitoring.png
---

---
layout: default
---

# Observabilité vs Monitoring

<div class="grid grid-cols-2 gap-8 mt-10 text-left text-lg">
  <div class="border-4 border-gray-700 p-6 rounded-xl">
    <h2 class="text-2xl font-bold text-center mb-4">Monitoring</h2>
    <ul class="space-y-4">
      <li>🔍 Que s'est il passé ?</li>
      <li>🚨 Est-ce que ça arrive souvent ?</li>
      <li>🛠️ Comment on corrige ?</li>
    </ul>
  </div>
  <div class="border-4 border-gray-700 p-6 rounded-xl">
    <h2 class="text-2xl font-bold text-center mb-4">Observability</h2>
    <ul class="space-y-4">
      <li>❓ Pourquoi est-ce arrivé ?</li>
      <li>⚙️ Est-ce que le système va bien ?</li>
      <li>🔁 Comment on fait pour que le système s'auto gère ?</li>
    </ul>
  </div>
</div>

---
title: Data
layout: image
image: /images/data.png
---

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
title: All in one
layout: default
---

# All in one - OpenTelemetry

<img src="/images/otel-logo.png" class="absolute-center"/>

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
title: Architecture collecteur OpenTelemetry
layout: image
image: /images/otel-collector-archi.png
---

---
layout: default
---

# La librairie
Au plus proche du code

<img src="/images/otel-librairies.png" class="absolute-center h-100 mt-10"/>

---
layout: default
---

# La collecteur
Au centre de la plateforme

<img src="/images/otel-collector-infra.png" class="absolute-center h-100 mt-10"/>

---
layout: default
---

# Fonctionnement du collecteur

<img src="/images/otel-collector.png" class="absolute-center h-full mt-10"/>

---
layout: default
---

# Exemple d'archi sous grafana

<img src="/images/grafana-archi.png" class="absolute-center h-100 mt-10"/>

---
layout: default
---

# Enfin un APM open source

<img src="/images/signoz.png" class="absolute-center h-100 mt-10"/>


---
title: Signoz
layout: iframe
url: https://signoz.devoxx-demo.sbx.aws.ippon.fr/
---

---
title: End
layout: image
image: /images/ippon-contact.png
---
