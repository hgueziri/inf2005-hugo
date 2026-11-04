---
title: "Travail pratique 1 : Analyse et conception orientée objet"
linkTitle: "Travail pratique 1"
description: "INF 2005 – Programmation orientée objet avec C++"
weight: 10
---

{{< figure-cours src="figures/banner_1.png" page="/docs/modules/module-1" alt="Bannière du cours INF 2005 – Programmation orientée objet avec C++" largeur="100%" >}}

# Travail pratique 1 : Analyse et conception orientée objet

{{< boite type="consigne" titre="Consignes de remise" >}}
- Utilisez le [gabarit Travail pratique 1](../../a-propos/ressources/gabarits/INF2005_Travail-Pratique-1.docx) (format .docx) pour consigner certaines informations relatives à la résolution des exercices.
- Quand vous avez fini les exercices, finissez de remplir le gabarit et déposez-le sur le site de la TÉLUQ. Pour accéder au dépôt, rejoignez MaTÉLUQ puis En cours > INF 2005 > tableau présentant les différentes activités du cours.
{{< /boite >}}

{{< boite type="contenu" >}}
**Objectif du travail :** évaluer la capacité de l'étudiante ou de l'étudiant à analyser un problème, identifier les objets importants, proposer des classes cohérentes et justifier des choix de conception orientée objet.
{{< /boite >}}

## Table des matières {#table-des-matieres}

- [1 Présentation du travail pratique](#presentation-du-travail-pratique)
- [2 Exercice 1 – Identifier les objets d'un système (2 pts)](#exercice-1-identifier-les-objets-d-un-systeme-2-pts)
- [3 Exercice 2 – Encapsulation (2 pts)](#exercice-2-encapsulation-2-pts)
- [4 Exercice 3 – Héritage ou composition ? (2 pts)](#exercice-3-heritage-ou-composition-2-pts)
- [5 Exercice 4 – Conception orientée objet (4 pts)](#exercice-4-conception-orientee-objet-4-pts)
- [6 Barème récapitulatif](#bareme-recapitulatif)

## 1. Présentation du travail pratique {#presentation-du-travail-pratique}

{{< boite type="synthese" titre="Synthèse – lecture rapide" >}}
Ce travail pratique porte sur les fondements du module 1. Il ne s'agit pas seulement de réciter des définitions, mais de montrer une capacité d'analyse et de conception. Les exercices demandent de transformer une description textuelle en classes, attributs, méthodes et relations entre objets.
{{< /boite >}}

{{< boite type="consigne" >}}

- Répondez à toutes les questions dans un document clair et structuré.
- Justifiez vos choix de conception avec des phrases complètes.
- Utilisez le vocabulaire du module : objet, classe, instance, attribut, méthode, encapsulation, héritage, composition, polymorphisme et message.
- Lorsque cela est demandé, remplissez les tableaux proposés.
- Les réponses très courtes ou seulement descriptives ne suffisent pas : chaque choix important doit être expliqué.

{{< /boite >}}

## 2. Exercice 1 – Identifier les objets d'un système (2 pts) {#exercice-1-identifier-les-objets-d-un-systeme-2-pts}

On souhaite concevoir une application de gestion d'une bibliothèque universitaire.

La bibliothèque contient des livres, des étudiants, ainsi que des emprunts. Un étudiant peut emprunter plusieurs livres. Un livre possède un titre, un auteur, une année de publication et un état indiquant s'il est disponible ou emprunté.

### Questions {#questions}

1. Identifier les principaux objets du système.
2. Proposer les classes nécessaires :
   - Pour chaque classe, proposer au moins trois attributs.
   - Pour chaque classe, proposer au moins deux méthodes.
3. Expliquer la différence entre une classe et une instance dans ce contexte.

### Tableau à compléter {#tableau-a-completer}

{{< tableau >}}
| Classe | Attributs proposés | Méthodes proposées |
|---|---|---|
| &nbsp; |  |  |
| &nbsp; |  |  |
| &nbsp; |  |  |
{{< /tableau >}}

## 3. Exercice 2 – Encapsulation (2 pts) {#exercice-2-encapsulation-2-pts}

Un étudiant propose la classe suivante pour gérer la billetterie d'un spectacle :

{{< tableau >}}
| | | |
|---|---|---|
| **Classe :** |  |  |
|  | `Spectacle` | Classe pour gérer la billetterie d'un spectacle |
| **Attributs :** |  |  |
|  | `Titre` | Titre du spectacle (chaîne de caractères) |
|  | `PlacesDisponibles` | Nombre de places encore disponibles (nombre entier) |
| **Méthodes :** |  |  |
|  | `CreerSpectacle` | Créer un nouveau spectacle |
|  | `SupprimerSpectacle` | Supprimer un spectacle existant |
{{< /tableau >}}

Exemple d'utilisation:

```cpp {linenos=table}
spectacle = CreerSpectacle("Concert de jazz", 200)
spectacle.PlacesDisponibles = spectacle.PlacesDisponibles - 3
```

Dans cet exemple, un spectacle est créé avec 200 places disponibles. La vente de trois billets est ensuite enregistrée en retirant directement 3 places, dont le nombre passe à 197.

### Questions {#questions-2}

1. Identifiez les problèmes que pourrait présenter cette conception. Illustrez votre réponse par un exemple concret.
2. Proposer une meilleure conception en utilisant l'encapsulation.
3. Ajouter deux méthodes pertinentes à cette conception.
4. Expliquez comment votre nouvelle conception contribue à préserver l'intégrité des données et à améliorer la fiabilité de l'application.

## 4. Exercice 3 – Héritage ou composition ? (2 pts) {#exercice-3-heritage-ou-composition-2-pts}

Pour chaque situation, indiquez s'il est préférable d'utiliser une relation d'héritage ou une relation de composition. Justifiez chaque réponse.

{{< tableau >}}
| Situation | Relation choisie | Justification |
|---|---|---|
| Un ordinateur portable possède une batterie. |  |  |
| Un chat est un mammifère. |  |  |
| Un album contient plusieurs chansons. |  |  |
| Un violon est un instrument de musique. |  |  |
| Un train comporte plusieurs wagons. |  |  |
{{< /tableau >}}

## 5. Exercice 4 – Conception orientée objet (4 pts) {#exercice-4-conception-orientee-objet-4-pts}

On souhaite concevoir une application de jeu vidéo simple.

Le jeu contient :

- un joueur ;
- des ennemis ;
- des obstacles ;
- des projectiles ;
- un score ;
- une zone de jeu.

### Questions {#questions-3}

1. Identifier au moins cinq classes utiles pour représenter ce système :
   - Pour chaque classe, proposer les attributs essentiels (au moins 3).
   - Pour chaque classe, proposer les méthodes principales (au moins 3).
2. Identifier au moins une relation d'héritage possible.
3. Identifier au moins une relation de composition possible.
4. Expliquer comment le polymorphisme pourrait être utilisé dans ce jeu.
5. Décrire un scénario d'exécution sous forme de messages échangés entre objets.

### Tableau à compléter {#tableau-a-completer-2}

{{< tableau >}}
| Classe | Rôle | Attributs | Méthodes |
|---|---|---|---|
| &nbsp; |  |  |  |
| &nbsp; |  |  |  |
| &nbsp; |  |  |  |
| &nbsp; |  |  |  |
| &nbsp; |  |  |  |
{{< /tableau >}}

{{< boite type="livrable" >}}
Pour cet exercice, la réponse doit contenir :

- un tableau des classes ;
- une explication des relations entre classes ;
- une justification de l'héritage ou de la composition ;
- un court scénario décrivant les messages échangés entre objets.

{{< /boite >}}

## 6. Barème récapitulatif {#bareme-recapitulatif}

{{< boite type="bareme" >}}

| Élément évalué | Points |
|---|---|
| Exercice 1 – Identification des objets et classes | 2 |
| Exercice 2 – Encapsulation et protection des données | 2 |
| Exercice 3 – Héritage ou composition | 2 |
| Exercice 4 – Mini-projet de conception orientée objet | 4 |
| **Total** | **10** |

{{< /boite >}}
