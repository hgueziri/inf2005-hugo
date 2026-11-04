---
title: "Feuille de route"
weight: 20
# Feuille de route proposée, affichée par le shortcode « feuille-route ».
# Une ligne « groupe » est un intertitre ; une ligne « nom » est une activité.
# Une activité avec « ponderation » est une évaluation (case rose), sinon une période d'étude (case bleue).
feuille_route:
  semaines: 15
  lignes:
    - nom: "Démarrage"
      lien: "/docs/modules/demarrage"
      semaines: [1]
    - groupe: "Module 1"
      lien: "/docs/modules/module-1"
    - nom: "Lecture"
      semaines: [1, 2]
    - nom: "Travail pratique 1"
      lien: "/docs/evaluation/travail-pratique-1"
      ponderation: "10 %"
      semaines: [2]
    - groupe: "Module 2"
      lien: "/docs/modules/module-2"
    - nom: "Lecture"
      semaines: [3, 4]
    - nom: "Travail pratique 2"
      lien: "/docs/evaluation/travail-pratique-2"
      ponderation: "10 %"
      semaines: [5]
    - groupe: "Module 3"
      lien: "/docs/modules/module-3"
    - nom: "Lecture"
      semaines: [6, 7]
    - nom: "Travail pratique 3"
      lien: "/docs/evaluation/travail-pratique-3"
      ponderation: "15 %"
      semaines: [8]
    - groupe: "Module 4"
      lien: "/docs/modules/module-4"
    - nom: "Lecture"
      semaines: [9, 10]
    - nom: "Travail pratique 4"
      lien: "/docs/evaluation/travail-pratique-4"
      ponderation: "15 %"
      semaines: [11]
    - groupe: "Module 5"
      lien: "/docs/modules/module-5"
    - nom: "Lecture"
      semaines: [12]
    - nom: "Clôture"
      lien: "/docs/modules/cloture"
      semaines: [13]
    - nom: "Projet"
      lien: "/docs/evaluation/projet"
      ponderation: "30 %"
      semaines: [13, 14]
    - nom: "Examen final"
      lien: "/docs/evaluation/examen-final"
      ponderation: "20 %"
      semaines: [15]
---

# Feuille de route

La feuille de route vous propose un cheminement régulier pendant la session, c’est-à-dire neuf heures d’études toutes les semaines.

Selon votre expertise préalable en programmation informatique et selon vos disponibilités et préférences d’études, vous voudrez peut-être adapter cette feuille de route.

{{< feuille-route >}}
