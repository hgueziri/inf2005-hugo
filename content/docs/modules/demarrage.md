---
title: "Démarrage"
weight: 5
---

# Démarrage

Lors de cette activité de démarrage, vous réalisez les activités que vous avez l'habitude de réaliser au début d'un cours de la TÉLUQ :

- explorer le contenu du cours ;
- planifier votre session ;
- prendre contact avec votre personne tutrice.

Vous préparez aussi l'environnement de programmation C++ que vous utiliserez tout au long du cours.

## Exploration

Lisez attentivement la [présentation du cours]({{< relref "/docs/a-propos/presentation" >}}), si ce n'est pas déjà fait. Notez vos questions : vous pourrez les poser lors de vos premiers échanges avec la personne tutrice.

Parcourez ensuite le site du cours, notamment pour :

- connaître les thèmes traités dans les modules (section **Apprentissage** du menu) ;
- avoir une idée de l'ampleur des textes de référence que vous aurez à étudier ;
- découvrir la nature des activités proposées dans les modules et des évaluations notées : travaux pratiques, projet et examen final (section **Évaluation** du menu).

## Planification

La [feuille de route]({{< relref "/docs/a-propos/feuille-de-route" >}}) propose un cheminement régulier pendant la session, soit neuf heures d'études par semaine pendant quinze semaines. En fonction de vos objectifs, de vos disponibilités et de vos préférences d'études, adaptez-la pour constituer votre propre cheminement : cliquez sur les cases pour répartir les activités, indiquez la date de début de votre session, puis générez un PDF. Vos modifications sont enregistrées dans votre navigateur.

Si vous vous écartez largement de la feuille de route proposée, prévenez la personne tutrice. C'est le cas, par exemple, si vous décidez de réaliser le cours en quelques semaines plutôt qu'en quinze. C'est aussi le cas si, à l'inverse, une indisponibilité déjà prévue pendant la session vous amène à le réaliser sur trente semaines : une demande de report de quatre mois de la date de fin du cours est alors nécessaire.

## Prise de contact

Prenez contact avec la personne tutrice qui vous a été assignée. Ses coordonnées sont inscrites dans la lettre que vous avez reçue par courrier postal ; vous les retrouvez aussi dans votre portail MaTÉLUQ.

Elle pourra notamment répondre aux questions que vous avez notées pendant la lecture de la présentation du cours. Si vous avez défini un cheminement très particulier à l'aide de la feuille de route, faites-lui-en part.

## Outil de programmation

Il existe différents environnements de programmation C++. Pour ce cours, le parcours principal est **VS Code** associé au compilateur **`g++`** (GCC), selon la norme C++17. Si vous ne pouvez pas installer ces outils, vous pouvez utiliser un notebook : **Google Colab**, en ligne et sans installation, ou **Jupyter Notebook**, sur votre ordinateur. La section [Préparer son environnement de travail]({{< relref "/docs/modules/module-2#preparer-son-environnement-de-travail" >}}) du module 2 explique comment installer et vérifier chacun de ces environnements.

Vous pouvez aussi utiliser un autre environnement de programmation C++, si vous en connaissez déjà un. Vous devez toutefois vous assurer que vos programmes se compilent et s'exécutent correctement avec `g++` : c'est avec `g++` (commande `g++ -std=c++17 -Wall -Wextra`) que la personne tutrice évaluera vos travaux.

{{< boite type="important" titre="À faire dès maintenant" >}}
Installez votre environnement et vérifiez votre compilateur dès cette semaine : un problème d'installation se règle plus facilement avant d'entreprendre le module 2 qu'à la veille d'une remise.
{{< /boite >}}
