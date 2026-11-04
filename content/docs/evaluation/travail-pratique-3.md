---
title: "Travail pratique 3 : Fonctions, tableaux, tri, recherche et chaînes de caractères"
linkTitle: "Travail pratique 3"
description: "INF 2005 – Programmation orientée objet avec C++"
weight: 30
---

{{< figure-cours src="figures/banner_3.png" page="/docs/modules/module-3" alt="Bannière du cours INF 2005 – Programmation orientée objet avec C++" largeur="100%" >}}

# Travail pratique 3 : Fonctions, tableaux, tri, recherche et chaînes de caractères

{{< boite type="consigne" titre="Consignes de remise" >}}
- Utilisez le [gabarit Travail pratique 3](../../a-propos/ressources/gabarits/INF2005_Travail-Pratique-3.docx) (format .docx) pour consigner certaines informations relatives à la résolution des exercices.
- Insérez des commentaires (lignes précédées de `//` ou paragraphes délimités par `/*` et `*/`) dans vos programmes pour en décrire les différents éléments ou étapes.
- Faites la preuve du bon fonctionnement de votre programme en fournissant dans le gabarit une ou plusieurs copie-écrans témoignant de l’exécution du programme, et des résultats obtenus.
- Quand vous avez fini les exercices, finissez de remplir le gabarit, compressez (.zip) l’ensemble des fichiers sources C++ (un pour chacun des quatre exercices) et déposez le tout sur le site de la TÉLUQ. Pour accéder au dépôt, rejoignez MaTÉLUQ puis En cours > INF 2005 > tableau présentant les différentes activités du cours.
{{< /boite >}}

{{< boite type="contenu" >}}
**Objectif du travail :** écrire des programmes C++ mieux structurés en utilisant des fonctions, des tableaux, des matrices, des algorithmes simples de tri et de recherche, ainsi que des chaînes de caractères.
{{< /boite >}}

## Table des matières {#table-des-matieres}

- [1 Présentation du travail pratique](#presentation-du-travail-pratique)
- [2 Rappel : compiler et exécuter un fichier C++](#rappel-compiler-et-executer-un-fichier-c)
  - [2.1 Dans VS Code](#dans-vs-code)
  - [2.2 Dans Jupyter Notebook ou Google Colab](#dans-jupyter-notebook-ou-google-colab)
- [3 Exercice 1 – Analyse de notes avec fonctions et tableaux (3 pts)](#exercice-1-analyse-de-notes-avec-fonctions-et-tableaux-3-pts)
- [4 Exercice 2 – Matrices et fonctions (4 pts)](#exercice-2-matrices-et-fonctions-4-pts)
- [5 Exercice 3 – Tri, recherche et comparaisons (4 pts)](#exercice-3-tri-recherche-et-comparaisons-4-pts)
- [6 Exercice 4 – Analyse de chaînes de caractères (4 pts)](#exercice-4-analyse-de-chaines-de-caracteres-4-pts)
- [7 Barème récapitulatif](#bareme-recapitulatif)
- [8 Critères généraux d'évaluation](#criteres-generaux-d-evaluation)

## 1. Présentation du travail pratique {#presentation-du-travail-pratique}

{{< boite type="synthese" titre="Synthèse – lecture rapide" >}}
Ce travail pratique renforce les notions du Module 3. Les exercices exigent une programmation plus structurée que dans le travail précédent : chaque solution doit être découpée en fonctions, testée avec plusieurs cas et présentée avec un affichage clair.
{{< /boite >}}

{{< boite type="consigne" >}}

- Remettez un fichier source C++ par exercice : `TP3_exercice1.cpp`, `TP3_exercice2.cpp`, `TP3_exercice3.cpp` et `TP3_exercice4.cpp`.
- Chaque programme doit contenir au moins trois fonctions en plus de la fonction `main`, sauf indication contraire.
- Chaque programme doit compiler avec la commande `g++ -std=c++17 -Wall -Wextra`.
- Les tableaux doivent être utilisés lorsque l'énoncé le demande.
- Les entrées invalides doivent être détectées et traitées proprement.
- Les résultats doivent être affichés clairement, sous forme de tableau lorsque c'est pertinent.
- Fournissez au moins deux captures d'écran par exercice : un cas normal et un cas particulier.

{{< /boite >}}

{{< boite type="important" >}}
Le but de ce travail pratique n'est pas seulement d'obtenir un résultat, mais de produire un code organisé, lisible et modulaire. Les fonctions doivent avoir des responsabilités claires.
{{< /boite >}}

## 2. Rappel : compiler et exécuter un fichier C++ {#rappel-compiler-et-executer-un-fichier-c}

### 2.1. Dans VS Code {#dans-vs-code}

Créer un fichier source, par exemple `TP3_exercice1.cpp`, puis exécuter dans le terminal :

```bash
g++ -std=c++17 -Wall -Wextra TP3_exercice1.cpp -o exercice1
./exercice1
```

Sous Windows, l'exécution peut aussi se faire avec :

```bash
exercice1.exe
```

### 2.2. Dans Jupyter Notebook ou Google Colab {#dans-jupyter-notebook-ou-google-colab}

Première cellule : créer le fichier source.

```bash
%%writefile TP3_exercice1.cpp
#include <iostream>

int main() {
    std::cout << "Test du TP3" << std::endl;
    return 0;
}
```

Deuxième cellule : compiler et exécuter.

```bash
%%bash
g++ -std=c++17 -Wall -Wextra TP3_exercice1.cpp -o exercice1
./exercice1
```

## 3. Exercice 1 – Analyse de notes avec fonctions et tableaux (3 pts) {#exercice-1-analyse-de-notes-avec-fonctions-et-tableaux-3-pts}

On souhaite analyser les notes obtenues par un groupe d'étudiantes et d'étudiants dans le cours INF 2005.

### Travail demandé {#travail-demande}

Écrire un programme C++ qui :

1. demande à l'utilisateur le nombre de notes à saisir, entre `5` et `20` ;
2. lit les notes dans un tableau ;
3. refuse toute note inférieure à `0` ou supérieure à `100` ;
4. une fois toutes les notes entrées :
   - calcule la moyenne du groupe ;
   - trouve la note minimale et la note maximale ;
   - compte le nombre de notes supérieures ou égales à `50` ;
   - affiche un tableau récapitulatif des notes avec la mention *réussi* ou *échoué*.

### Fonctions obligatoires {#fonctions-obligatoires}

Le programme doit contenir au minimum les fonctions suivantes :

```cpp
void lireNotes(double notes[], int taille);
double calculerMoyenne(const double notes[], int taille);
double trouverMinimum(const double notes[], int taille);
double trouverMaximum(const double notes[], int taille);
int compterReussites(const double notes[], int taille);
void afficherRapport(const double notes[], int taille);
```

### Contraintes {#contraintes}

- Utiliser un tableau de type `double`.
- Ne pas effectuer tous les calculs directement dans `main`.
- Ajouter des commentaires expliquant le rôle des fonctions.
- Afficher les résultats avec deux chiffres après la virgule.

### Exemple d'affichage attendu {#exemple-d-affichage-attendu}

```text
Nombre de notes : 6

Note 1 : 80
Note 2 : 42
Note 3 : 76
Note 4 : 91
Note 5 : 55
Note 6 : 48

+----------+----------+----------+
| Etudiant | Note     | Resultat |
+----------+----------+----------+
| 1        | 80.00    | reussi   |
| 2        | 42.00    | echoue   |
| 3        | 76.00    | reussi   |
| 4        | 91.00    | reussi   |
| 5        | 55.00    | reussi   |
| 6        | 48.00    | echoue   |
+----------+----------+----------+

Moyenne : 65.33
Minimum : 42.00
Maximum : 91.00
Nombre de reussites : 4
```

{{< boite type="livrable" >}}
Fichier attendu : `TP3_exercice1.cpp`. Inclure une capture d'écran avec des notes valides et une capture montrant le refus d'une note invalide.
{{< /boite >}}

## 4. Exercice 2 – Matrices et fonctions (4 pts) {#exercice-2-matrices-et-fonctions-4-pts}

On souhaite manipuler deux matrices carrées contenant des entiers.

### Travail demandé {#travail-demande-2}

Écrire un programme C++ qui :

1. utilise deux matrices carrées de taille `5 x 5` ;
2. remplit automatiquement les deux matrices avec des valeurs entières séquentielles ;
3. affiche les deux matrices ;
4. calcule et affiche la matrice somme ;
5. calcule et affiche le produit des deux matrices *A* × *B* ;
6. calcule la somme de chaque ligne de la matrice somme ;
7. affiche la plus grande valeur présente dans la matrice somme.

### Fonctions obligatoires {#fonctions-obligatoires-2}

Le programme doit contenir au minimum les fonctions suivantes :

```cpp
void remplirMatrice(int matrice[][5], int taille, int depart);
void afficherMatrice(const int matrice[][5], int taille);
void additionnerMatrices(const int A[][5], const int B[][5], int S[][5], int taille);
void multiplierMatrices(const int A[][5], const int B[][5], int M[][5], int taille);
void afficherSommeLignes(const int matrice[][5], int taille);
int trouverMaximumMatrice(const int matrice[][5], int taille);
```

### Contraintes {#contraintes-2}

- Utiliser des tableaux à deux dimensions.
- Utiliser des fonctions pour chaque traitement important.
- Ne pas écrire le même code d'affichage plusieurs fois.
- Présenter les matrices avec des colonnes alignées.

### Exemple d'affichage attendu {#exemple-d-affichage-attendu-2}

```text
Matrice A
1   2   3   4   5
6   7   8   9   10
...

Matrice B
10  11  12  13  14
15  16  17  18  19
...

Matrice somme
11  13  15  17  19
21  23  25  27  29
...

Somme des lignes de la matrice somme :
Ligne 1 : 75
Ligne 2 : 125
...

Maximum de la matrice somme : 59
```

{{< boite type="livrable" >}}
Fichier attendu : `TP3_exercice2.cpp`. Inclure une capture d'écran montrant les deux matrices, la matrice somme, le produit *A* × *B* et les statistiques demandées.
{{< /boite >}}

## 5. Exercice 3 – Tri, recherche et comparaisons (4 pts) {#exercice-3-tri-recherche-et-comparaisons-4-pts}

On souhaite trier un tableau d'entiers, puis rechercher une valeur dans ce tableau.

### Travail demandé {#travail-demande-3}

Écrire un programme C++ qui :

1. crée un tableau de `50` entiers ;
2. remplit le tableau avec des valeurs aléatoires comprises entre `1` et `200` ;
3. affiche le tableau avant le tri ;
4. trie le tableau par ordre croissant en utilisant le tri à bulle ;
5. affiche le tableau trié par ordre croissant ;
6. affiche le tableau par ordre décroissant ;
7. demande à l'utilisateur une valeur à rechercher ;
8. recherche cette valeur dans le tableau trié à l'aide d'une recherche linéaire ;
9. indique si la valeur a été trouvée ;
10. affiche la position de la première occurrence trouvée ;
11. affiche le nombre de comparaisons effectuées pendant la recherche.

### Fonctions obligatoires {#fonctions-obligatoires-3}

Le programme doit contenir au minimum les fonctions suivantes :

```cpp
void remplirAleatoire(int tableau[], int taille);
void afficherTableau(const int tableau[], int taille);
void trierBulle(int tableau[], int taille);
void afficherDecroissant(const int tableau[], int taille);
int rechercherValeur(const int tableau[], int taille, int valeur, int& comparaisons);
```

### Contraintes {#contraintes-3}

- Utiliser le tri à bulle.
- Utiliser une fonction de recherche séparée.
- Utiliser le passage par référence pour récupérer le nombre de comparaisons.
- La première position du tableau est considérée comme la position `1`.
- Tester le programme avec une valeur présente et une valeur absente.

### Exemple d'affichage attendu {#exemple-d-affichage-attendu-3}

```text
Tableau initial :
42  17  93  17  120 ...

Tableau trie croissant :
3  8  17  17  25 ...

Tableau trie decroissant :
199  180  175  160 ...

Valeur a rechercher : 17
Valeur trouvee a la position : 3
Nombre de comparaisons : 3
```

{{< boite type="livrable" >}}
Fichier attendu : `TP3_exercice3.cpp`. Inclure une capture d'écran avec une valeur présente et une autre avec une valeur absente.
{{< /boite >}}

## 6. Exercice 4 – Analyse de chaînes de caractères (4 pts) {#exercice-4-analyse-de-chaines-de-caracteres-4-pts}

On souhaite analyser une phrase entrée par l'utilisateur.

### Travail demandé {#travail-demande-4}

Écrire un programme C++ qui :

1. demande à l'utilisateur d'entrer une phrase contenant au moins `20` caractères ;
2. redemande la phrase tant qu'elle est trop courte ;
3. demande une lettre à rechercher ;
4. affiche la phrase en remplaçant chaque occurrence de cette lettre par sa version majuscule ;
5. affiche toutes les positions où la lettre apparaît ;
6. compte le nombre total d'occurrences ;
7. compte le nombre de voyelles dans la phrase ;
8. compte le nombre de consonnes dans la phrase ;
9. indique si la lettre recherchée est absente ou présente.

### Fonctions obligatoires {#fonctions-obligatoires-4}

Le programme doit contenir au minimum les fonctions suivantes :

```cpp
std::string lirePhraseValide();
char lireLettre();
int compterOccurrences(const std::string& phrase, char lettre);
void afficherPositions(const std::string& phrase, char lettre);
std::string mettreOccurrencesEnMajuscule(const std::string& phrase, char lettre);
int compterVoyelles(const std::string& phrase);
int compterConsonnes(const std::string& phrase);
```

### Contraintes {#contraintes-4}

- Utiliser `std::string`.
- Utiliser au moins une fonction de la bibliothèque `<cctype>`.
- Ignorer la différence entre majuscules et minuscules lors de la recherche.
- La première position de la phrase est considérée comme la position `1`.
- Le programme doit fonctionner avec des espaces dans la phrase.

### Exemple d'affichage attendu {#exemple-d-affichage-attendu-4}

```text
Entrez une phrase d'au moins 20 caracteres :
la programmation en cpp est importante

Lettre a rechercher : p

Phrase modifiee :
la Programmation en cPP est imPortante

Positions trouvees : 4 22 23 31
Nombre d'occurrences : 4
Nombre de voyelles : 12
Nombre de consonnes : 21
```

{{< boite type="livrable" >}}
Fichier attendu : `TP3_exercice4.cpp`. Inclure une capture d'écran avec une lettre présente et une capture avec une lettre absente.
{{< /boite >}}

## 7. Barème récapitulatif {#bareme-recapitulatif}

{{< boite type="bareme" >}}

| Élément évalué | Points |
|---|---|
| Exercice 1 – Analyse de notes avec fonctions et tableaux | 3 |
| Exercice 2 – Matrices et fonctions | 4 |
| Exercice 3 – Tri, recherche et comparaisons | 4 |
| Exercice 4 – Analyse de chaînes de caractères | 4 |
| **Total** | **15** |

{{< /boite >}}

## 8. Critères généraux d'évaluation {#criteres-generaux-d-evaluation}

{{< tableau >}}
| Critère | Attentes |
|---|---|
| Compilation | Le programme compile sans erreur avec `g++ -std=c++17 -Wall -Wextra`. |
| Modularisation | Le programme est découpé en fonctions claires et réutilisables. |
| Utilisation des tableaux | Les tableaux et matrices sont utilisés correctement lorsque demandés. |
| Exactitude | Les résultats sont corrects pour plusieurs cas de test. |
| Validation | Les entrées invalides sont détectées et traitées correctement. |
| Lisibilité | Le code est indenté, organisé et contient des commentaires utiles. |
| Preuves d'exécution | Les captures d'écran montrent clairement les tests effectués et les résultats obtenus. |
{{< /tableau >}}

{{< boite type="attention" >}}
Un programme qui fonctionne seulement pour un cas particulier, sans fonctions, sans validation ou sans preuve d'exécution, ne répond pas complètement aux attentes de ce travail pratique.
{{< /boite >}}
