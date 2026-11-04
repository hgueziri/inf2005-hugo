---
title: "Travail pratique 2 : Premiers programmes C++, entrées-sorties, opérateurs et structures de contrôle"
linkTitle: "Travail pratique 2"
description: "INF 2005 – Programmation orientée objet avec C++"
weight: 20
---

{{< figure-cours src="figures/banner_2.png" page="/docs/modules/module-2" alt="Bannière du cours INF 2005 – Programmation orientée objet avec C++" largeur="100%" >}}

# Travail pratique 2 : Premiers programmes C++, entrées-sorties, opérateurs et structures de contrôle

{{< boite type="consigne" titre="Consignes de remise" >}}
- Utilisez le [gabarit Travail pratique 2](../../a-propos/ressources/gabarits/INF2005_Travail-Pratique-2.docx) (format .docx) pour consigner certaines informations relatives à la résolution des exercices.
- Insérez des commentaires (lignes précédées de `//` ou paragraphes délimités par `/*` et `*/`) dans vos programmes pour en décrire les différents éléments ou étapes.
- Faites la preuve du bon fonctionnement de votre programme en fournissant dans le gabarit une ou plusieurs copie-écrans témoignant de l’exécution du programme, et des résultats obtenus.
- Quand vous avez fini les exercices, finissez de remplir le gabarit, compressez (.zip) l’ensemble des fichiers sources C++ (un pour chacun des quatre exercices) et déposez le tout sur le site de la TÉLUQ. Pour accéder au dépôt, rejoignez MaTÉLUQ puis En cours > INF 2005 > tableau présentant les différentes activités du cours.
{{< /boite >}}

{{< boite type="contenu" >}}
**Objectif du travail :** écrire des programmes C++ corrects, lisibles et testés, en utilisant les bases du langage : entrées-sorties, opérateurs, conditions, boucles et affichage structuré des résultats.
{{< /boite >}}

## Table des matières {#table-des-matieres}

- [1 Présentation du travail pratique](#presentation-du-travail-pratique)
- [2 Rappel : compiler et exécuter un fichier C++](#rappel-compiler-et-executer-un-fichier-c)
  - [2.1 Dans VS Code](#dans-vs-code)
  - [2.2 Dans Jupyter Notebook ou Google Colab](#dans-jupyter-notebook-ou-google-colab)
- [3 Exercice 1 – Convertisseur de devises (2 pts)](#exercice-1-convertisseur-de-devises-2-pts)
- [4 Exercice 2 – Table de multiplication (2 pts)](#exercice-2-table-de-multiplication-2-pts)
- [5 Exercice 3 – Carrés inférieurs à une limite (2 pts)](#exercice-3-carres-inferieurs-a-une-limite-2-pts)
- [6 Exercice 4 – Analyse du temps de travail (4 pts)](#exercice-4-analyse-du-temps-de-travail-4-pts)
- [7 Barème récapitulatif](#bareme-recapitulatif)
- [8 Critères généraux d'évaluation](#criteres-generaux-d-evaluation)

## 1. Présentation du travail pratique {#presentation-du-travail-pratique}

{{< boite type="synthese" titre="Synthèse – lecture rapide" >}}
Ce travail pratique renforce les bases du Module 2. Les exercices ne demandent pas seulement d'obtenir un résultat numérique : ils exigent aussi une validation des entrées, un affichage propre, des tests avec plusieurs cas et une courte justification des choix de programmation.
{{< /boite >}}

{{< boite type="consigne" >}}

- Remettez un fichier source C++ par exercice : `TP2_exercice1.cpp`, `TP2_exercice2.cpp`, `TP2_exercice3.cpp` et `TP2_exercice4.cpp`.
- Chaque programme doit contenir des commentaires utiles pour expliquer les étapes importantes.
- Chaque programme doit compiler avec la commande `g++ -std=c++17 -Wall -Wextra`.
- Fournissez au moins deux captures d'écran par exercice : une exécution normale et un cas de test particulier.
- Les résultats doivent être affichés proprement à l'écran, de préférence sous forme de tableau lorsque c'est demandé.
- Les programmes doivent refuser ou corriger les entrées invalides lorsque l'énoncé le demande.

{{< /boite >}}

{{< boite type="important" >}}
La syntaxe C++ est la même dans VS Code, Jupyter Notebook et Google Colab. Ce qui change uniquement est la manière de créer le fichier, de compiler et d'exécuter le programme.
{{< /boite >}}

## 2. Rappel : compiler et exécuter un fichier C++ {#rappel-compiler-et-executer-un-fichier-c}

### 2.1. Dans VS Code {#dans-vs-code}

Créer un fichier source, par exemple `TP2_exercice1.cpp`, puis exécuter dans le terminal :

```bash
g++ -std=c++17 -Wall -Wextra TP2_exercice1.cpp -o exercice1
./exercice1
```

Sous Windows, l'exécution peut aussi se faire avec :

```bash
exercice1.exe
```

### 2.2. Dans Jupyter Notebook ou Google Colab {#dans-jupyter-notebook-ou-google-colab}

Première cellule : créer le fichier source.

```bash
%%writefile TP2_exercice1.cpp
#include <iostream>

int main() {
    std::cout << "Test du TP2" << std::endl;
    return 0;
}
```

Deuxième cellule : compiler et exécuter.

```bash
%%bash
g++ -std=c++17 -Wall -Wextra TP2_exercice1.cpp -o exercice1
./exercice1
```

## 3. Exercice 1 – Convertisseur de devises (2 pts) {#exercice-1-convertisseur-de-devises-2-pts}

On souhaite convertir une somme exprimée en dollars canadiens vers l'euro selon plusieurs taux de change.

### Travail demandé {#travail-demande}

Écrire un programme C++ qui :

1. demande à l'utilisateur une somme en dollars canadiens ;
2. refuse une somme négative ou nulle ;
3. utilise les trois taux suivants : `1.35`, `1.40` et `1.60`, pour calculer la conversion en euros pour chaque taux ;
4. affiche les résultats sous forme de tableau ;

### Contraintes obligatoires {#contraintes-obligatoires}

- Utiliser au moins une structure conditionnelle.
- Utiliser au moins une boucle pour parcourir les trois taux.
- Afficher les montants avec deux chiffres après la virgule.
- Le programme doit être compréhensible et commenté.

### Exemple d'affichage attendu {#exemple-d-affichage-attendu}

```text
Entrez un montant en dollars canadiens : 200

+----------------+----------------+----------------+
| Montant CAD    | Taux CAD/EUR   | Montant EUR    |
+----------------+----------------+----------------+
| 200.00         | 1.35           | 148.15         |
| 200.00         | 1.40           | 142.86         |
| 200.00         | 1.60           | 125.00         |
+----------------+----------------+----------------+
```

{{< boite type="livrable" >}}
Fichier attendu : `TP2_exercice1.cpp`. Inclure une capture d'écran avec un montant valide et une capture d'écran avec un montant invalide.
{{< /boite >}}

## 4. Exercice 2 – Table de multiplication (2 pts) {#exercice-2-table-de-multiplication-2-pts}

Écrire un programme qui affiche la table de multiplication d'un nombre entré par l'utilisateur. Le nombre doit être compris entre `1` et `10`.

### Travail demandé {#travail-demande-2}

Le programme doit :

1. demander un nombre entier à l'utilisateur ;
2. refuser les valeurs strictement inférieures à `1` ou strictement supérieures à `10` ;
3. redemander la valeur tant qu'elle est invalide ;
4. afficher la table de multiplication de `1` à `10` ;
5. afficher à la fin la somme des dix résultats obtenus ;
6. indiquer combien de résultats sont pairs et combien sont impairs.

### Contraintes obligatoires {#contraintes-obligatoires-2}

- Utiliser une boucle `while` ou `do/while` pour valider l'entrée.
- Utiliser une boucle `for` pour afficher la table.
- Utiliser une condition pour déterminer si un résultat est pair ou impair.
- Présenter les résultats proprement.

### Exemple d'affichage attendu {#exemple-d-affichage-attendu-2}

```text
Entrez un nombre entre 1 et 10 : 12
Valeur invalide. Recommencez.

Entrez un nombre entre 1 et 10 : 7

Table de multiplication de 7

7 x 1  = 7
7 x 2  = 14
7 x 3  = 21
...
7 x 10 = 70

Somme des résultats : 385
Nombre de résultats pairs : 5
Nombre de résultats impairs : 5
```

{{< boite type="livrable" >}}
Fichier attendu : `TP2_exercice2.cpp`. Inclure une capture d'écran avec une valeur invalide puis une valeur valide.
{{< /boite >}}

## 5. Exercice 3 – Carrés inférieurs à une limite (2 pts) {#exercice-3-carres-inferieurs-a-une-limite-2-pts}

Afficher tous les carrés inférieurs ou égaux à un nombre *limite* choisi par l'utilisateur.

### Travail demandé {#travail-demande-3}

Écrire un programme qui :

1. demande à l'utilisateur un nombre entier entre `100` et `1000` ;
2. redemande le nombre tant qu'il est invalide ;
3. affiche tous les carrés inférieurs ou égaux à ce nombre : pour chaque ligne afficher le nombre, son carré et la parité du carré ;
4. calcule le nombre total de carrés affichés ;
5. calcule la somme de tous les carrés affichés.

### Contraintes obligatoires {#contraintes-obligatoires-3}

- Utiliser une boucle de validation de l'entrée.
- Utiliser une boucle pour générer les carrés.
- Utiliser une condition pour afficher `pair` ou `impair`.
- Ne pas utiliser de tableau pour cet exercice.

### Exemple d'affichage attendu {#exemple-d-affichage-attendu-3}

```text
Entrez une limite entre 100 et 1000 : 150

+----------+----------+----------+
| Nombre   | Carre    | Parite   |
+----------+----------+----------+
| 1        | 1        | impair   |
| 2        | 4        | pair     |
| 3        | 9        | impair   |
...
| 12       | 144      | pair     |
+----------+----------+----------+

Nombre de carres affiches : 12
Somme des carres : 650
```

{{< boite type="livrable" >}}
Fichier attendu : `TP2_exercice3.cpp`. Inclure une capture d'écran avec une limite valide et une capture d'écran montrant la validation d'une limite invalide.
{{< /boite >}}

## 6. Exercice 4 – Analyse du temps de travail (4 pts) {#exercice-4-analyse-du-temps-de-travail-4-pts}

Une entreprise souhaite estimer le temps de travail perdu et le coût associé aux pauses extérieures prises par certains employés.

Chaque employé concerné consacre en moyenne *M* minutes par jour de son temps de travail à ces pauses. L’entreprise compte *N* employés fumeurs, dont le salaire horaire moyen est de *S* $.

Vous devez développer un programme permettant de calculer le nombre total d’heures de travail perdues ainsi que le coût salarial correspondant, sur différentes périodes : par jour, par semaine, par mois et par année.

Les résultats doivent être présentés sous la forme d’un tableau récapitulatif, indiquant pour chaque période le temps de travail perdu et le coût associé.

### Travail demandé {#travail-demande-4}

Écrire un programme C++ qui :

1. demande le nombre d'employés concernés *N*;
2. demande le nombre moyen de minutes perdues par employé et par jour *M* ;
3. demande le salaire horaire moyen *S* ;
4. valide que toutes les valeurs sont strictement positives et numériques ;
5. calcule le nombre total d'heures perdues par jour, semaine, mois et année ;
6. calcule le coût correspondant par jour, semaine, mois et année ;
7. affiche les résultats sous forme de tableau ;
8. compare le coût annuel obtenu avec un seuil de 10 000 $ et affiche un message d'analyse.

### Hypothèses à utiliser {#hypotheses-a-utiliser}

- Une semaine contient `5` jours de travail.
- Un mois contient `22` jours de travail.
- Une année contient `260` jours de travail.

### Contraintes obligatoires {#contraintes-obligatoires-4}

- Utiliser des variables de type `int` et `double` pour les entrées.
- Utiliser des conditions pour valider les données.
- Utiliser une présentation tabulaire avec des colonnes alignées.
- Afficher les coûts avec deux chiffres après la virgule.

### Exemple d'affichage attendu {#exemple-d-affichage-attendu-4}

```text
Nombre d'employes concernes : 50
Minutes perdues par employe et par jour : 5
Salaire horaire moyen : 17

+----------+----------------+----------------+
| Periode  | Heures perdues | Cout estime    |
+----------+----------------+----------------+
| Jour     | 4.17           | 70.83          |
| Semaine  | 20.83          | 354.17         |
| Mois     | 91.67          | 1558.33        |
| Annee    | 1083.33        | 18416.67       |
+----------+----------------+----------------+

Analyse : le cout annuel depasse 10000 dollars.
```

{{< boite type="livrable" >}}
Fichier attendu : `TP2_exercice4.cpp`. Inclure une capture d'écran avec les valeurs de l'énoncé et une autre capture avec des valeurs différentes.
{{< /boite >}}

## 7. Barème récapitulatif {#bareme-recapitulatif}

{{< boite type="bareme" >}}

| Élément évalué | Points |
|---|---|
| Exercice 1 – Convertisseur de devises amélioré | 2 |
| Exercice 2 – Table de multiplication contrôlée | 2 |
| Exercice 3 – Carrés inférieurs à une limite | 2 |
| Exercice 4 – Analyse du temps de travail perdu | 4 |
| **Total** | **10** |

{{< /boite >}}

## 8. Critères généraux d'évaluation {#criteres-generaux-d-evaluation}

{{< tableau >}}
| Critère | Attentes |
|---|---|
| Compilation | Le programme compile sans erreur avec `g++ -std=c++17 -Wall -Wextra`. |
| Exactitude | Les calculs produits sont corrects pour plusieurs cas de test. |
| Validation | Les entrées invalides sont détectées et traitées correctement. |
| Lisibilité | Le code est indenté, organisé et contient des commentaires utiles. |
| Affichage | Les résultats sont présentés clairement, en particulier sous forme de tableau lorsque demandé. |
| Preuves d'exécution | Les captures d'écran montrent clairement les tests effectués et les résultats obtenus. |
{{< /tableau >}}

{{< boite type="attention" >}}
Un programme qui donne seulement le résultat pour un seul cas, sans validation et sans preuve d'exécution, ne répond pas complètement aux attentes de ce travail pratique.
{{< /boite >}}
