---
title: "Présentation"
weight: 10
---

# Bienvenue dans le cours INF 2005

Votre navigateur web, le moteur de votre jeu vidéo préféré, le logiciel d'un robot ou d'une voiture moderne : il y a de bonnes chances qu'une partie de ces programmes soit écrite en C++. Dans ce cours, vous passez de l'autre côté de l'écran. Vous apprendrez à concevoir des logiciels organisés autour d'objets, puis à les programmer en C++, pas à pas, en écrivant, en compilant et en testant vos propres programmes.

## Pourquoi le C++ et l'orienté objet ?

**Le C++, c'est la performance et la proximité de la machine.** Rapide et exigeant, ce langage est utilisé partout où chaque milliseconde compte : moteurs de jeux vidéo, navigateurs web, systèmes embarqués, robotique, finance, calcul scientifique. L'apprendre, c'est aussi comprendre ce qui se passe « sous le capot » : la compilation, les types, la mémoire. Ces connaissances vous suivront dans n'importe quel autre langage, que ce soit Java, C# ou Python.

**L'orienté objet, c'est une façon de penser.** Plutôt que d'écrire une longue suite d'instructions, vous découpez un problème en objets qui ont chacun un rôle précis : un article d'inventaire, un compte bancaire, une figure à dessiner. Chaque objet protège ses données et offre des services aux autres. Résultat : des programmes plus faciles à comprendre, à corriger, à faire évoluer et à réutiliser. C'est cette approche qui permet de bâtir et d'entretenir les grands logiciels d'aujourd'hui.

## Programmer à l'ère de l'IA

Une IA peut aujourd'hui écrire une fonction ou une classe en quelques secondes. Alors, pourquoi apprendre tout cela ? Parce qu'écrire du code n'est qu'une partie du travail. Décider quelles classes votre logiciel doit contenir, ce que chacune doit cacher ou offrir, comment elles collaborent, quand utiliser l'héritage plutôt qu'une simple composition : ce sont des choix de **conception**, et ils restent les vôtres. Pour tirer parti d'une IA, vous devez aussi savoir lire le code qu'elle propose, y repérer les erreurs, juger s'il est bien conçu et pouvoir l'expliquer. C'est exactement ce que ce cours vous apprend : le Module 1 commence d'ailleurs par la conception, avant même la première ligne de C++.

{{< boite type="objectif" >}}
À la fin du cours, vous devriez être capable de :

- expliquer les principes de la programmation orientée objet et la distinguer des autres façons de programmer ;
- concevoir une application simple en identifiant ses classes, leurs responsabilités et leurs relations ;
- écrire, compiler, tester et corriger des programmes C++ ;
- utiliser l'héritage, le polymorphisme et la bibliothèque standard pour construire des programmes réutilisables ;
- participer à l'élaboration de programmes plus complexes.
{{< /boite >}}

## Le cours en bref

- **Durée** : 135 heures, réparties sur 15 semaines. Au besoin, vous pouvez profiter d'un report de la fin du cours ; consultez le *Guide des études à distance* pour les précisions.
- **Environnement** : C++17, avec VS Code et le compilateur `g++` ; Google Colab ou Jupyter Notebook en solution de remplacement.
- **Encadrement** : une personne tutrice vous accompagne tout au long du cours, principalement par courriel. Elle répond à vos questions sur les textes et les consignes, vous conseille sur votre cheminement et évalue vos travaux en vous donnant une rétroaction détaillée.

### Votre parcours

La section **Apprentissage** vous guide du premier programme jusqu'aux notions avancées :

- [Démarrage]({{< relref "/docs/modules/demarrage" >}}) : pour bien commencer.
- [Module 1]({{< relref "/docs/modules/module-1" >}}) – Introduction à l'approche orientée objet : objets, classes, abstraction, encapsulation, héritage et polymorphisme, vus sous l'angle de la conception.
- [Module 2]({{< relref "/docs/modules/module-2" >}}) – Premiers pas en C++ : écrire, compiler et exécuter un programme ; variables, entrées-sorties, opérateurs, conditions et boucles.
- [Module 3]({{< relref "/docs/modules/module-3" >}}) – Fonctions, tableaux, tri, recherche et chaînes de caractères.
- [Module 4]({{< relref "/docs/modules/module-4" >}}) – Vos premières classes C++, l'héritage, le polymorphisme et des notions avancées : surcharge d'opérateurs, fonctions amies, fichiers et bibliothèque standard (STL). Son [annexe]({{< relref "/docs/modules/module-4/module-4-annexe" >}}) propose des approfondissements, dont un projet en plusieurs fichiers.
- [Module 5]({{< relref "/docs/modules/module-5" >}}) – Programmation parallèle, distribuée et réseau : threads, mutex, sockets et patrons (*templates*).
- [Clôture]({{< relref "/docs/modules/cloture" >}}) : pour faire le bilan.

Chaque module combine un texte de référence, de nombreux exemples de code à compiler et à modifier, et de courtes activités (« À essayer », « Exercice guidé ») pour vérifier votre compréhension au fur et à mesure.

La section **Évaluation** du menu regroupe vos quatre travaux pratiques, le projet et l'examen final.

La formation à distance demande de la discipline et fait appel à votre autonomie. Si elle est nouvelle pour vous, consultez les sections *Stratégies d'étude* et *L'art de vivre ses études* du site de la TÉLUQ : vous y trouverez de précieux conseils.

## L'IA générative dans ce cours

Vous pouvez utiliser des outils d'IA générative (Copilot, ChatGPT, Gemini, etc.) dans ce cours, y compris pour vos travaux, à condition de le faire de façon éthique, intègre et responsable, comme le prévoit l'[énoncé institutionnel de l'Université TÉLUQ](https://bibliotheque.teluq.ca/c.php?g=742145). Concrètement, citez l'IA dans votre travail et dans votre liste de références, et documentez les requêtes utilisées ainsi que les réponses obtenues. Servez-vous-en pour comprendre, explorer ou déboguer, pas pour penser à votre place : assurez-vous de pouvoir expliquer tout le code que vous remettez, car vous demeurez responsable de toute erreur, omission ou « hallucination » qu'il contient. Une utilisation littérale (copier-coller) ou déguisée qui empêche d'évaluer vos compétences constitue une infraction au [Règlement disciplinaire sur l'intégrité intellectuelle](https://www.teluq.ca/site/documents/universite/reglement-integrite-intellectuelle.pdf). Les consignes de chaque évaluation peuvent préciser ou restreindre cet usage : lisez-les attentivement.

Pour aller plus loin : la formation [Étudier à l'ère de l'IA](https://plagiat-integrite.teluq.ca/etudier-ere-ia/) et la page [Savoir citer](https://bibliotheque.teluq.ca/c.php?g=728431&p=5225468) de la Bibliothèque (section « Intelligence artificielle générative »).
