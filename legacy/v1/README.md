# OpenTelemetry: vous ne pourrez plus vous passer de monitoring en prod

## Abstract
Pour toutes les personnes qui travaillent dans un système distribué, il est aujourd’hui vital de monitorer son architecture. L’optimisation d’une architecture passe avant tout par une connaissance accrue de son fonctionnement. C’est à partir de cette problématique qu’est né OpenTelemetry.

OpenTelemetry, c’est quoi ? Comment s'inscrit cette outil dans vos développements ?

On passera un peu de temps à vous présenter ce projet, puis on rentrera dans le vif du sujet. Une fois passée l’étape du tutoriel, on se retrouve souvent face à la dure réalité de mettre ça en place sur sa stack en production. Comment faire pour monitorer plus de 400 microservices en prod ? Quelles techniques peut-on utiliser pour concrètement optimiser les ressources dont on a besoin ?

On ressort souvent des conférences avec de belles démo et s’ensuit ce qu’on aime appeler le Hype Driven Development. Mais lorsqu’il faut mettre en place ce monitoring sur une stack existante, comment ça marche ?

A travers un retour d’expérience et des exemples concrets d’utilisation, on vous présentera les enjeux et les bonnes pratiques pour monitorer votre production.

## Pitch
Dans cette conférence, on présentera en premier lieu les concepts derrière OpenTelemetry et on rentrera rapidement dans les détails.
La présentation sera sous forme de slide entrecoupé de démo et de code, pour rendre l'expérience la plus dynamique possible.
L’idée principale reste de pouvoir présenter un réel cas d'implémentation de cette stack dans un environnement de prod. 

On présentera les mécaniques d’auto-instrumentation, de configuration, et même d’auto-scaling pour avoir une consommation la plus juste de nos ressources.

Nous ne savons pas encore si le client nous permettra de le citer, donc nous évitons toute référence pour le moment. Mais si nous en avons l’autorisation, nous présenterons la réelle mise en place qu’on a pu faire. Sinon, on anonymisera un peu tout ça.
Mais on restera sur un réel cas d’usage.

## Powered by [Slidev](https://github.com/slidevjs/slidev)!

To start the slide show:

- `npm install`
- `npm run dev`
- visit http://localhost:3030

Edit the [slides.md](./slides.md) to see the changes.

Learn more about Slidev on [documentations](https://sli.dev/).
