---
title: "Module 3 : Fonctions, tableaux, tri, recherche et chaînes de caractères"
linkTitle: "Module 3"
description: "INF 2005 – Programmation orientée objet avec C++"
weight: 30
---

{{< figure-cours src="figures/banner_3.png" alt="Bannière du cours INF 2005 – Programmation orientée objet avec C++" largeur="100%" >}}

# Module 3 : Fonctions, tableaux, tri, recherche et chaînes de caractères

{{< boite type="objectif" >}}
À la fin de ce module, l'étudiante ou l'étudiant devrait être capable de :

- définir, appeler et tester une fonction en C++ ;
- distinguer paramètres, arguments, valeurs de retour et portée des variables ;
- expliquer les effets du passage par valeur et du passage par référence ;
- déclarer, initialiser et parcourir des tableaux à une ou deux dimensions ;
- appliquer et expliquer des algorithmes simples de recherche et de tri ;
- justifier les conditions nécessaires à une recherche binaire ;
- manipuler des chaînes avec `std::string` et reconnaître les contraintes des chaînes C.

{{< /boite >}}

{{< boite type="contenu" >}}
**Contenu du module :** maîtriser l'écriture de fonctions, la manipulation de tableaux, les algorithmes simples de tri et de recherche, ainsi que les chaînes de caractères en C++.
{{< /boite >}}

{{< boite type="fiche" >}}
| | |
|---|---|
| Cours | INF 2005 – Programmation orientée objet avec C++ |
| Document | Module 3 – Fonctions et structures de données de base |
| Thèmes principaux | Fonctions, paramètres, surcharge, fonctions `inline`, tableaux, tri à bulle, recherche linéaire, recherche binaire et chaînes de caractères |
| Environnement recommandé | Jupyter Notebook et VS Code avec `g++` |
| Norme recommandée | C++17 ou version plus récente |
{{< /boite >}}

## Table des matières {#table-des-matieres}

- [1 Introduction : organiser un programme avec des fonctions](#introduction-organiser-un-programme-avec-des-fonctions)
  - [1.1 Première fonction : un programme guidé](#premiere-fonction-un-programme-guide)
- [2 Fonctions : définition, appel et paramètres](#fonctions-definition-appel-et-parametres)
  - [2.1 Définition et valeur de retour](#definition-et-valeur-de-retour)
  - [2.2 Appel, arguments et paramètres](#appel-arguments-et-parametres)
- [3 Paramètres et portée des variables](#parametres-et-portee-des-variables)
  - [3.1 Variables locales et portée](#variables-locales-et-portee)
  - [3.2 Passage par valeur](#passage-par-valeur)
  - [3.3 Passage par référence](#passage-par-reference)
- [4 Déclaration et surcharge des fonctions](#declaration-et-surcharge-des-fonctions)
  - [4.1 La déclaration d'une fonction (prototype)](#la-declaration-d-une-fonction-prototype)
  - [4.2 La surcharge des fonctions](#la-surcharge-des-fonctions)
- [5 Tableaux](#tableaux)
  - [5.1 Déclaration, initialisation et parcours](#declaration-initialisation-et-parcours)
  - [5.2 Passer un tableau à une fonction](#passer-un-tableau-a-une-fonction)
  - [5.3 Tableaux à plusieurs dimensions](#tableaux-a-plusieurs-dimensions)
- [6 Rechercher et trier dans les tableaux](#rechercher-et-trier-dans-les-tableaux)
  - [6.1 Recherche linéaire](#recherche-lineaire)
  - [6.2 Tri à bulle](#tri-a-bulle)
  - [6.3 Recherche binaire](#recherche-binaire)
  - [6.4 Mettre les recherches à l'essai](#mettre-les-recherches-a-l-essai)
- [7 Manipulation des chaînes de caractères](#manipulation-des-chaines-de-caracteres)
  - [7.1 Déclarer et utiliser `std::string`](#declarer-et-utiliser-std-string)
  - [7.2 Rechercher dans une chaîne avec `find()`](#rechercher-dans-une-chaine-avec-find)
  - [7.3 Chaînes C : tableaux de caractères](#chaines-c-tableaux-de-caracteres)
  - [7.4 Fonctions de la bibliothèque `<cstring>` (comparaison)](#fonctions-de-la-bibliotheque-cstring-comparaison)
- [8 Mise en pratique et synthèse](#mise-en-pratique-et-synthese)
  - [8.1 Mini-projet progressif : analyser les notes d'un groupe](#mini-projet-progressif-analyser-les-notes-d-un-groupe)
  - [8.2 Questions de révision](#questions-de-revision)
- [Synthèse finale du module](#synthese-finale-du-module)
- [Lecture complémentaire : inline et static](#lecture-complementaire-facultative-inline-et-static)

## 1. Introduction : organiser un programme avec des fonctions {#introduction-organiser-un-programme-avec-des-fonctions}

Dans le module précédent, nous avons appris à écrire des programmes C++ utilisant des variables, des conditions et des boucles. À mesure qu'un programme grandit, regrouper toutes les instructions dans `main()` rend le code plus difficile à lire, à tester et à modifier. Les **fonctions** permettent de décomposer un problème en tâches plus simples, chacune ayant un rôle précis.

Nous avons déjà rencontré `main()`, le point d'entrée d'un programme C++, ainsi que des éléments de la bibliothèque standard tels que `std::cout` pour l'affichage et `std::cin` pour la lecture. Nous allons maintenant écrire nos propres fonctions et apprendre à leur transmettre des données. Les tableaux, les algorithmes de recherche et de tri, puis les chaînes de caractères prolongeront ces connaissances. Ces outils serviront plus tard à programmer les méthodes des classes présentées dans le module 1.

{{< boite type="important" >}}
Une fonction regroupe un traitement ayant une responsabilité identifiable. Des noms comme `somme`, `afficherMenu`, `calculerMoyenne` ou `rechercherElement` indiquent clairement le rôle du traitement.
{{< /boite >}}

### 1.1. Première fonction : un programme guidé {#premiere-fonction-un-programme-guide}

Le programme suivant réutilise les notions de compilation vues au module 2. Il contient une fonction `somme` et la fonction `main()` qui l'appelle.

**Programme complet :** copier le code dans un fichier `main.cpp`, puis le compiler et l'exécuter.

```cpp {linenos=table}
#include <iostream>

int somme(int a, int b)
{
    return a + b;
}

int main()
{
    int resultat = somme(2, 3);
    std::cout << "La somme est : " << resultat << '\n';
    return 0;
}
```

Listing 1 – Premier programme avec une fonction

{{< boite type="exemple" titre="Résultat attendu" >}}

```cpp
La somme est : 5
```

{{< /boite >}}

{{< tableau >}}
| Élément | Rôle |
|---|---|
| `int somme(int a, int b)` | Définit une fonction qui reçoit deux nombres entiers et renvoie un entier. |
| `return a + b;` | Calcule la somme et transmet le résultat à l'appelant. |
| `somme(2, 3)` | Appelle la fonction avec les valeurs 2 et 3. |
| `int resultat = ...;` | Conserve la valeur renvoyée par la fonction. |
| `std::cout` | Affiche le résultat de l'appel. |
{{< /tableau >}}

{{< boite type="exemple" titre="À essayer" >}}
Remplacez l'appel `somme(2, 3)` par `somme(10, 4)`. **Avant de compiler**, prédisez la valeur affichée, puis vérifiez votre réponse (`14`). Supprimez ensuite volontairement le point-virgule à la fin de la ligne d'affichage, observez le message du compilateur, corrigez l'erreur et recompilez.
{{< /boite >}}

## 2. Fonctions : définition, appel et paramètres {#fonctions-definition-appel-et-parametres}

### 2.1. Définition et valeur de retour {#definition-et-valeur-de-retour}

Une fonction est définie par son **type de retour**, son **nom**, sa liste de **paramètres** et son **corps**. Sa forme générale est :

**Extrait schématique (non compilable tel quel) :**

```cpp {linenos=table}
type_de_retour nom_de_la_fonction(type parametre1, type parametre2)
{
    // instructions
    return valeur;
}
```

Le type de retour indique la nature de la valeur produite par la fonction. Le corps, délimité par des accolades, contient les instructions à exécuter. L'instruction `return` transmet une valeur de retour et termine l'exécution de la fonction.

{{< figure-cours src="figures/figure_01_anatomie_fonction.png" numero="1" legende="Structure générale d'une fonction C++." largeur="95%" >}}

La figure présente l'anatomie d'une fonction : il s'agit d'un **schéma explicatif**, non d'un programme autonome. Dans un programme réel, chaque variable utilisée dans le corps (par exemple `resultat`) doit avoir été déclarée avant son utilisation.

**Extrait :** définition de la fonction utilisée dans le premier programme.

```cpp {linenos=table}
int somme(int premierNombre, int deuxiemeNombre)
{
    return premierNombre + deuxiemeNombre;
}
```

Si une fonction n'a pas de valeur à renvoyer, son type de retour est `void`. Le `return;` final n'est alors pas nécessaire, sauf si l'on souhaite quitter la fonction avant la fin du corps.

**Extrait :**

```cpp {linenos=table}
void afficherMessage()
{
    std::cout << "Bonjour !\n";
}
```

Cet extrait suppose que `<iostream>` est inclus dans le programme complet. Une fonction `void` peut être appelée avec `afficherMessage();` sans qu'une valeur soit récupérée.

### 2.2. Appel, arguments et paramètres {#appel-arguments-et-parametres}

Une fonction est appelée en écrivant son nom suivi de parenthèses. Les **paramètres** sont les variables déclarées dans son en-tête ; les **arguments** sont les valeurs ou expressions fournies lors de l'appel. Dans `somme(2, 3)`, les nombres 2 et 3 sont des arguments, alors que `a` et `b` dans `int somme(int a, int b)` sont des paramètres.

Une fonction peut être appelée depuis `main()` ou depuis une autre fonction. Les parenthèses sont obligatoires, même si aucun argument n'est nécessaire : `afficherMessage();`.

{{< boite type="remarque" titre="Remarque" >}}
Dans un premier temps, on peut placer la définition d'une fonction avant `main()`. Nous verrons ensuite comment utiliser un prototype pour placer sa définition après `main()`.
{{< /boite >}}

## 3. Paramètres et portée des variables {#parametres-et-portee-des-variables}

### 3.1. Variables locales et portée {#variables-locales-et-portee}

Une **variable locale** est déclarée dans une fonction ou dans un bloc délimité par des accolades. Elle n'est accessible que dans la portée autorisée par ce bloc, à partir de sa déclaration. Les paramètres d'une fonction sont également locaux à celle-ci. Deux fonctions peuvent utiliser un même nom de variable sans partager la même variable.

**Programme complet :**

```cpp {linenos=table}
#include <iostream>

int calculerCarre(int nombre)
{
    int resultat = nombre * nombre;
    return resultat;
}

int main()
{
    int resultat = calculerCarre(4);
    std::cout << resultat << '\n';  // affiche 16
    return 0;
}
```

Dans cet exemple, les deux variables nommées `resultat` sont **distinctes**. La variable locale de `calculerCarre` ne peut pas être utilisée directement dans `main()`, mais sa *valeur* peut être renvoyée par `return`. Une variable locale ordinaire cesse normalement d'exister lorsque l'exécution sort de son bloc.

{{< boite type="exemple" titre="Vérifier la portée" >}}
Renommez la variable `resultat` dans `main()` en `valeur`. Le programme fonctionne toujours. Essayez ensuite d'afficher `nombre` directement dans `main()` et expliquez l'erreur du compilateur : `nombre` est un paramètre local à `calculerCarre`.
{{< /boite >}}

### 3.2. Passage par valeur {#passage-par-valeur}

Par défaut, pour un paramètre tel que `int nombre`, l'argument est transmis **par valeur** : la fonction travaille sur une copie. Modifier le paramètre n'affecte pas la variable de l'appelant.

**Extrait (à insérer avant `main()`) :**

```cpp {linenos=table}
void ajouterUnParValeur(int nombre)
{
    nombre++;
}
```

### 3.3. Passage par référence {#passage-par-reference}

Un paramètre déclaré `int& nombre` désigne directement la variable transmise ; les modifications dans la fonction sont donc visibles dans le programme appelant.

**Extrait (à insérer avant `main()`) :**

```cpp {linenos=table}
void ajouterUnParReference(int& nombre)
{
    nombre++;
}
```

{{< figure-cours src="figures/figure_04_valeur_reference.png" numero="2" legende="Différence entre passage par valeur et passage par référence." largeur="95%" >}}

**Programme complet comparant les deux modes de passage :**

```cpp {linenos=table}
#include <iostream>

void ajouterUnParValeur(int nombre)
{
    nombre++;
}

void ajouterUnParReference(int& nombre)
{
    nombre++;
}

int main()
{
    int n = 4;
    ajouterUnParValeur(n);
    std::cout << "Apres valeur : " << n << '\n';
    ajouterUnParReference(n);
    std::cout << "Apres reference : " << n << '\n';
    return 0;
}
```

{{< boite type="exemple" titre="Résultat attendu" >}}

```cpp
Apres valeur : 4
Apres reference : 5
```

{{< /boite >}}

L'exemple initial suivant illustre également une référence, mais utilise cette fois une fonction qui renvoie la valeur calculée :

**Programme complet :**

```cpp {linenos=table}
#include <iostream>

int doubler(int& nombre)
{
    nombre += nombre;
    return nombre;
}

int main()
{
    int un = 4;
    std::cout << "Avant : un = " << un << '\n';
    int resultat = doubler(un);
    std::cout << "Apres : un = " << un << '\n';
    std::cout << "resultat = " << resultat << '\n';
    return 0;
}
```

{{< boite type="important" >}}
Le passage par référence est utile lorsqu'une fonction doit modifier volontairement la variable de l'appelant. Pour lire un objet potentiellement coûteux à copier sans le modifier, on peut utiliser une **référence constante**, par exemple `const std::string& texte`. Pour de petits types comme `int`, le passage par valeur reste généralement simple et approprié.
{{< /boite >}}

## 4. Déclaration et surcharge des fonctions {#declaration-et-surcharge-des-fonctions}

### 4.1. La déclaration d'une fonction (prototype) {#la-declaration-d-une-fonction-prototype}

En C++, le compilateur doit connaître la déclaration d'une fonction avant son premier appel. On peut placer sa définition avant `main()`, ou déclarer un **prototype** avant `main()` puis placer sa définition plus loin.

{{< figure-cours src="figures/figure_02_cycle_fonction.png" numero="3" legende="Lien entre déclaration, appel et définition d'une fonction." largeur="95%" >}}

{{< boite type="remarque" titre="Remarque" >}}
La figure montre l'**ordre des éléments écrits dans un fichier source**, et non une chronologie d'exécution. Quand `main()` appelle `somme`, le corps de cette fonction est exécuté, même si sa définition apparaît plus bas dans le fichier.
{{< /boite >}}

**Programme complet :**

```cpp {linenos=table}
#include <iostream>

int somme(int, int);  // prototype

int main()
{
    int resultat = somme(2, 5);
    std::cout << "resultat = " << resultat << '\n';
    return 0;
}

int somme(int premierNombre, int deuxiemeNombre)
{
    return premierNombre + deuxiemeNombre;
}
```

{{< boite type="exemple" titre="Expérimentation" >}}
Supprimez temporairement le prototype, sans déplacer la définition. Essayez de compiler, puis restaurez-le. Cette manipulation montre pourquoi le compilateur doit connaître la fonction avant l'appel.
{{< /boite >}}

{{< boite type="remarque" titre="Bonne pratique" >}}
Dans un projet plus important, les déclarations de fonctions sont souvent placées dans des fichiers d'en-tête `.h` ou `.hpp`, tandis que les définitions sont placées dans des fichiers `.cpp`. Cette organisation sera détaillée ultérieurement.
{{< /boite >}}

### 4.2. La surcharge des fonctions {#la-surcharge-des-fonctions}

La **surcharge** permet à plusieurs fonctions de porter le même nom si les types, le nombre ou l'ordre de leurs paramètres permettent de les distinguer. Le choix est effectué lors de la compilation selon les arguments fournis. **Le seul type de retour ne suffit pas** pour distinguer deux fonctions surchargées.

{{< figure-cours src="figures/figure_03_surcharge_fonctions.png" numero="4" legende="Principe de sélection d'une fonction surchargée." largeur="95%" >}}

La figure présente trois versions de `somme` ; le programme ci-dessous définit effectivement ces trois signatures, y compris celle avec des arguments de types mixtes.

**Programme complet :**

```cpp {linenos=table}
#include <iostream>

int somme(int a, int b)
{
    return a + b;
}

double somme(double a, double b)
{
    return a + b;
}

double somme(int a, double b)
{
    return a + b;
}

int main()
{
    std::cout << somme(4, 5) << '\n';
    std::cout << somme(1.2, 3.12) << '\n';
    std::cout << somme(4, 2.5) << '\n';
    return 0;
}
```

{{< boite type="attention" >}}
Deux appels peuvent être ambigus si plusieurs surcharges sont également pertinentes. Les valeurs par défaut peuvent aussi créer des ambiguïtés. Par exemple, deux définitions qui ne diffèrent que par le type de retour ne constituent pas des surcharges valides.
{{< /boite >}}

## 5. Tableaux {#tableaux}

Un **tableau C** regroupe plusieurs éléments du même type dans des cases consécutives en mémoire. Il permet, par exemple, de conserver des notes, des mesures ou des identifiants. Nous commençons par ces tableaux pour comprendre les indices et le parcours des données.

{{< boite type="remarque" titre="Les collections en C++ moderne" >}}
La bibliothèque standard offre également `std::array`, un tableau de taille fixe avec une interface plus pratique, et `std::vector`, dont la taille peut varier. Ces conteneurs seront utiles dans des programmes plus élaborés ; nous nous concentrons ici sur les tableaux C pour comprendre les mécanismes de base.
{{< /boite >}}

### 5.1. Déclaration, initialisation et parcours {#declaration-initialisation-et-parcours}

Un tableau à une dimension se déclare à l'aide d'un type, d'un nom et d'une taille :

**Syntaxe schématique :**

```cpp {linenos=table}
type nomDuTableau[taille];
```

**Extraits :**

```cpp {linenos=table}
int tableauDesEntiers[10];
char tableauDeCaracteres[20];
int notes[20];
```

Dans ce cas, les valeurs des cases des tableaux locaux de types fondamentaux **ne sont pas initialisées** : il ne faut pas les lire avant leur affectation. Pour initialiser toutes les cases d'un tableau d'entiers à zéro, on peut écrire `int tableauDesEntiers[10]{};`.

Les indices commencent à zéro : un tableau de cinq éléments utilise les indices `0`, `1`, `2`, `3` et `4`.

{{< figure-cours src="figures/figure_05_tableau_indices.png" numero="5" legende="Indices d'un tableau à une dimension." largeur="92%" >}}

Un tableau peut aussi recevoir ses valeurs dès sa déclaration :

```cpp {linenos=table}
int tableauDesEntiers[10] = {0, 1, 2, 3, 4, 5, 6, 7, 8, 9};
int nombre[3][2] = {{1, 2}, {12, 9}, {5, 4}};
```

**Programme complet :**

```cpp {linenos=table}
#include <iostream>

int main()
{
    const int dimensionTableau = 5;
    int tableauEntier[dimensionTableau]{};

    for (int i = 0; i < dimensionTableau; i++)
    {
        tableauEntier[i] = i + 1;
    }

    for (int i = 0; i < dimensionTableau; i++)
    {
        std::cout << "tableauEntier[" << i << "] = "
                  << tableauEntier[i] << '\n';
    }
    return 0;
}
```

{{< boite type="important" >}}
Dans un tableau de cinq éléments, seuls les indices `0` à `4` sont valides. Un accès à `tableau[5]` est hors limites et entraîne un **comportement indéfini** : le programme peut afficher une valeur erronée, sembler fonctionner ou s'interrompre. Le compilateur ne détecte pas nécessairement ce type d'erreur.
{{< /boite >}}

{{< boite type="exemple" titre="À essayer" >}}
Modifiez le remplissage pour affecter `i * 2` à chaque case. Avant d'exécuter, prédisez la suite affichée : `0, 2, 4, 6, 8`.
{{< /boite >}}

### 5.2. Passer un tableau à une fonction {#passer-un-tableau-a-une-fonction}

Lorsqu'un tableau C est transmis à une fonction sous la forme d'un paramètre `int notes[]`, celui-ci se comporte comme un **pointeur vers le premier élément**. La fonction ne reçoit pas automatiquement sa taille : il faut lui transmettre une taille valide, comme dans `ajouterDeux(notes, 5)`. Cette notion de pointeur sera approfondie plus tard.

**Extrait : définition à placer avant `main()`.**

```cpp {linenos=table}
void ajouterDeux(int notes[], int taille)
{
    for (int i = 0; i < taille; i++)
    {
        notes[i] += 2;
    }
}
```

**Extrait : appel à placer dans `main()`, après la définition ou la déclaration de la fonction.**

```cpp {linenos=table}
int notesCoursINF2005[5] = {70, 65, 82, 90, 55};
ajouterDeux(notesCoursINF2005, 5);
```

{{< boite type="remarque" titre="Remarque" >}}
Les modifications des éléments du tableau sont visibles dans le programme appelant. Le paramètre `taille` doit correspondre au nombre de cases effectivement accessibles ; transmettre une taille trop grande peut entraîner un accès hors limites.
{{< /boite >}}

### 5.3. Tableaux à plusieurs dimensions {#tableaux-a-plusieurs-dimensions}

Un tableau à deux dimensions peut être représenté par une grille de lignes et de colonnes. Par exemple, `int tableauNotes[3][4];` désigne trois lignes et quatre colonnes. Chaque élément est désigné par deux indices : `tableauNotes[ligne][colonne]`.

{{< figure-cours src="figures/figure_06_tableau_2d.png" numero="6" legende="Représentation d'un tableau à deux dimensions." largeur="90%" >}}

**Programme complet :**

```cpp {linenos=table}
#include <iostream>

int main()
{
    int tableauNotes[3][4] = {
        {80, 75, 90, 85},
        {60, 70, 65, 72},
        {95, 88, 91, 93}
    };

    for (int ligne = 0; ligne < 3; ligne++)
    {
        for (int colonne = 0; colonne < 4; colonne++)
        {
            std::cout << tableauNotes[ligne][colonne] << ' ';
        }
        std::cout << '\n';
    }
    return 0;
}
```

{{< boite type="exemple" titre="Résultat attendu" >}}

```cpp
80 75 90 85
60 70 65 72
95 88 91 93
```

{{< /boite >}}

Pour une valeur fixée de `ligne`, la boucle intérieure parcourt toutes les colonnes. À la fin de chaque ligne, l'instruction `std::cout << '\n';` passe à la ligne suivante. **Question :** quelle est la valeur de `tableauNotes[1][2]` ? Réponse : `65`.

## 6. Rechercher et trier dans les tableaux {#rechercher-et-trier-dans-les-tableaux}

La recherche permet de trouver un élément particulier dans une collection ; le tri permet de réorganiser les valeurs. Nous commencerons par une recherche simple qui fonctionne sur des données non triées, puis nous verrons comment le tri rend possible une recherche plus rapide.

### 6.1. Recherche linéaire {#recherche-lineaire}

La **recherche linéaire** compare la clé recherchée à chaque élément en partant du début. Elle ne nécessite pas que le tableau soit trié. La fonction suivante renvoie l'indice de la première valeur trouvée, ou `-1` en cas d'absence.

**Extrait : fonction à placer avant `main()`.**

```cpp {linenos=table}
int rechercheLineaire(const int tableau[], int taille, int cle)
{
    for (int i = 0; i < taille; i++)
    {
        if (tableau[i] == cle)
        {
            return i;
        }
    }
    return -1;
}
```

{{< boite type="important" >}}
La valeur `-1` signale l'absence de résultat. Elle est distincte de l'indice `0`, qui désigne le premier élément du tableau. Le paramètre `const int tableau[]` précise que cette fonction ne modifie pas les éléments du tableau par cet accès.
{{< /boite >}}

### 6.2. Tri à bulle {#tri-a-bulle}

Le **tri à bulle** compare des éléments voisins et les échange s'ils sont dans le mauvais ordre. À chaque passage complet, l'une des plus grandes valeurs restantes se place vers la fin du tableau.

{{< figure-cours src="figures/figure_07_tri_bulle.png" numero="7" legende="Principe du tri à bulle : comparaison puis échange." largeur="95%" >}}

{{< tableau >}}
| État | Tableau |
|---|---|
| Initial | `7 3 5 2 9` |
| Après le 1er passage | `3 5 2 7 9` |
| Après le 2e passage | `3 2 5 7 9` |
| Après le 3e passage | `2 3 5 7 9` |
{{< /tableau >}}

**Programme complet :** la définition de `triBulle` apparaît une seule fois, après `main()`, grâce au prototype.

```cpp {linenos=table}
#include <iostream>

void triBulle(int tableau[], int taille);

int main()
{
    const int nombreElements = 10;
    int notes[nombreElements] = {1, 5, 7, 89, 64, 75, 32, 45, 56, 10};
    triBulle(notes, nombreElements);

    std::cout << "Les donnees triees : ";
    for (int i = 0; i < nombreElements; i++)
    {
        std::cout << notes[i] << ' ';
    }
    std::cout << '\n';
    return 0;
}

void triBulle(int tableau[], int taille)
{
    for (int iteration = 0; iteration < taille - 1; iteration++)
    {
        for (int i = 0; i < taille - 1 - iteration; i++)
        {
            if (tableau[i] > tableau[i + 1])
            {
                int tampon = tableau[i];
                tableau[i] = tableau[i + 1];
                tableau[i + 1] = tampon;
            }
        }
    }
}
```

{{< boite type="exemple" titre="Sortie attendue" >}}

```cpp
Les donnees triees : 1 5 7 10 32 45 56 64 75 89
```

{{< /boite >}}

{{< boite type="attention" >}}
Cette version du tri à bulle demande un nombre d'opérations proportionnel à *n*² pour un tableau de *n* éléments. Son intérêt est pédagogique : elle aide à comprendre comparaisons, échanges et boucles imbriquées. Dans les programmes usuels, la bibliothèque standard propose notamment `std::sort` pour trier plus efficacement.
{{< /boite >}}

### 6.3. Recherche binaire {#recherche-binaire}

La **recherche binaire** exige que le tableau soit trié dans le même ordre que celui utilisé pour les comparaisons (ici, l'ordre croissant). Elle compare la clé à l'élément central, puis recommence dans la moitié où la clé peut encore se trouver.

{{< figure-cours src="figures/figure_08_recherches.png" numero="8" legende="Différence entre recherche linéaire et recherche binaire." largeur="95%" >}}

**Extrait : fonction de recherche binaire sur un tableau trié croissant.**

```cpp {linenos=table}
int rechercheBinaire(const int tableau[], int taille, int cle)
{
    int inferieur = 0;
    int superieur = taille - 1;

    while (inferieur <= superieur)
    {
        int milieu = inferieur + (superieur - inferieur) / 2;
        if (tableau[milieu] == cle)
            return milieu;
        else if (cle < tableau[milieu])
            superieur = milieu - 1;
        else
            inferieur = milieu + 1;
    }
    return -1;
}
```

Pour le tableau `2 4 6 8 10 12 14`, on recherche la clé `12` :

{{< tableau >}}
| Étape | Inf. | Sup. | Milieu | Valeur | Décision |
|:---:|:---:|:---:|:---:|:---:|---|
| 1 | 0 | 6 | 3 | 8 | Chercher dans la moitié droite |
| 2 | 4 | 6 | 5 | 12 | Élément trouvé à l'indice 5 |
{{< /tableau >}}

{{< boite type="remarque" titre="Remarque" >}}
Pour *n* éléments, la recherche linéaire peut demander jusqu'à *n* comparaisons, tandis que la recherche binaire réduit approximativement l'intervalle de moitié à chaque étape. Si des doublons sont présents, cet algorithme ne garantit pas de retourner la première occurrence.
{{< /boite >}}

### 6.4. Mettre les recherches à l'essai {#mettre-les-recherches-a-l-essai}

Le programme complet suivant définit les deux fonctions de recherche et les applique à un même tableau déjà trié, pour une valeur présente et une valeur absente.

```cpp {linenos=table}
#include <iostream>

int rechercheLineaire(const int valeurs[], int taille, int cle)
{
    for (int i = 0; i < taille; i++)
        if (valeurs[i] == cle) return i;
    return -1;
}

int rechercheBinaire(const int valeurs[], int taille, int cle)
{
    int bas = 0, haut = taille - 1;
    while (bas <= haut)
    {
        int milieu = bas + (haut - bas) / 2;
        if (valeurs[milieu] == cle) return milieu;
        if (cle < valeurs[milieu]) haut = milieu - 1;
        else bas = milieu + 1;
    }
    return -1;
}

int main()
{
    int nombres[7] = {2, 4, 6, 8, 10, 12, 14};
    std::cout << "Lineaire (12) : "
              << rechercheLineaire(nombres, 7, 12) << '\n';
    std::cout << "Binaire (12) : "
              << rechercheBinaire(nombres, 7, 12) << '\n';
    std::cout << "Binaire (7) : "
              << rechercheBinaire(nombres, 7, 7) << '\n';
    return 0;
}
```

{{< boite type="exemple" titre="Sortie attendue" >}}

```cpp
Lineaire (12) : 5
Binaire (12) : 5
Binaire (7) : -1
```

{{< /boite >}}

## 7. Manipulation des chaînes de caractères {#manipulation-des-chaines-de-caracteres}

En C++ moderne, `std::string` est une façon habituelle de représenter du texte. Il s'agit d'un **objet**, doté d'opérations telles que l'affichage, la copie, la concaténation ou la recherche. Cet exemple renoue avec les notions d'objets et de méthodes présentées au module 1.

### 7.1. Déclarer et utiliser `std::string` {#declarer-et-utiliser-std-string}

**Programme complet :**

```cpp {linenos=table}
#include <iostream>
#include <string>

int main()
{
    std::string prenom = "Alex";
    std::string message = "Bonjour " + prenom;
    std::cout << message << '\n';
    std::cout << "Longueur : " << prenom.size() << '\n';
    return 0;
}
```

{{< boite type="exemple" titre="Sortie attendue" >}}

```cpp
Bonjour Alex
Longueur : 4
```

{{< /boite >}}

La notation `prenom.size()` appelle une **méthode** de l'objet `prenom`. La même chaîne peut être copiée directement : `std::string copie = prenom;`.

{{< figure-cours src="figures/figure_09_chaines.png" numero="9" legende="Deux manières de représenter une chaîne de caractères." largeur="95%" >}}

### 7.2. Rechercher dans une chaîne avec `find()` {#rechercher-dans-une-chaine-avec-find}

La méthode `find()` recherche un caractère ou une sous-chaîne et renvoie la **position de sa première occurrence**, en commençant à zéro. Si aucun résultat n'est trouvé, elle renvoie la valeur spéciale `std::string::npos`. Il faut vérifier ce résultat avant d'utiliser la position comme indice.

**Programme complet :**

```cpp {linenos=table}
#include <iostream>
#include <string>

int main()
{
    std::string texte = "Aujourd'hui";
    auto position = texte.find("hui");

    if (position != std::string::npos)
        std::cout << "Position trouvee : " << position << '\n';
    else
        std::cout << "Chaine introuvable\n";
    return 0;
}
```

**Résultat attendu :** `Position trouvee : 8`.

L'argument facultatif de `find()` indique à partir de quelle position commencer la recherche. Ainsi, en répétant la recherche à partir de la position précédente augmentée de 1, on peut retrouver plusieurs occurrences :

**Programme complet :**

```cpp {linenos=table}
#include <iostream>
#include <string>

int main()
{
    std::string phrase = "Aujourd'hui nous sommes lundi";
    auto position = phrase.find('u');
    while (position != std::string::npos)
    {
        std::cout << position << '\n';
        position = phrase.find('u', position + 1);
    }
    return 0;
}
```

{{< boite type="remarque" titre="Remarque" >}}
La méthode `rfind()` cherche la dernière occurrence d'une sous-chaîne ou d'un caractère. Dans les exemples en ASCII, une position correspond à un caractère affiché. Pour du texte accentué encodé en UTF-8, certains caractères occupent plusieurs octets : `size()` et `find()` ne comptent pas directement les caractères visuels.
{{< /boite >}}

### 7.3. Chaînes C : tableaux de caractères {#chaines-c-tableaux-de-caracteres}

C++ permet aussi d'utiliser des **chaînes C**, représentées par des tableaux `char[]` terminés par le caractère nul `'\0'`. Ce caractère marque la fin du texte ; il occupe une case dans le tableau.

**Extraits :**

```cpp {linenos=table}
char chaine[] = {'B', 'o', 'n', 'j', 'o', 'u', 'r', '\0'};
char autreChaine[] = "Bonjour";
```

{{< boite type="attention" >}}
La chaîne `"Bonjour"` contient sept lettres, mais nécessite **huit cases** pour inclure le caractère nul `'\0'`. Un tableau trop petit peut entraîner des erreurs de mémoire. Pour du nouveau code C++, `std::string` est habituellement préférable.
{{< /boite >}}

### 7.4. Fonctions de la bibliothèque `<cstring>` (comparaison) {#fonctions-de-la-bibliotheque-cstring-comparaison}

Les fonctions suivantes permettent de lire ou manipuler des chaînes C. Elles demeurent présentes dans de nombreux programmes existants ; il faut cependant connaître leurs contraintes.

{{< tableau >}}
| Fonction | Rôle et précaution |
|---|---|
| `std::strlen` | Donne la longueur d'une chaîne C sans compter le caractère nul. |
| `std::strcpy` | Copie une chaîne C ; ne vérifie pas la capacité de la destination. |
| `std::strncpy` | Copie au plus le nombre de caractères demandé, sans garantir le caractère nul final si la source est trop longue. |
| `std::strcat` | Concatène des chaînes ; la destination doit contenir assez d'espace. |
| `std::strcmp` | Compare deux chaînes C suivant l'ordre lexicographique de leurs octets. |
{{< /tableau >}}

**Programme complet (pour comprendre une API C existante) :**

```cpp {linenos=table}
#include <cstring>
#include <iostream>

int main()
{
    char chaine1[] = "Nul n'est prophete en son pays";
    char chaine2[80];
    std::strcpy(chaine2, chaine1);
    std::cout << "chaine1 : " << chaine1 << '\n';
    std::cout << "chaine2 : " << chaine2 << '\n';
    return 0;
}
```

La copie réussit dans cet exemple **parce que** le tableau `chaine2` est assez grand pour recevoir tous les caractères et le marqueur de fin. `std::strcpy` ne vérifie pas cette capacité. En pratique, préférez la copie d'un objet `std::string` : `std::string copie = original;`.

## 8. Mise en pratique et synthèse {#mise-en-pratique-et-synthese}

### 8.1. Mini-projet progressif : analyser les notes d'un groupe {#mini-projet-progressif-analyser-les-notes-d-un-groupe}

Ce mini-projet met en relation les fonctions, les tableaux et les chaînes. Effectuez les étapes dans l'ordre, en compilant et en exécutant le programme après chaque modification.

1. Déclarez un tableau contenant cinq notes et affichez-les avec une boucle.
2. Écrivez une fonction `calculerMoyenne` qui reçoit le tableau et sa taille, puis renvoie une moyenne de type `double`.
3. Écrivez une fonction `rechercheLineaire` et essayez de retrouver une note présente, puis une valeur absente ; affichez l'indice ou un message adapté.
4. Triez les notes par ordre croissant avec le tri à bulle, puis appliquez une recherche binaire. Vérifiez que vous ne lancez pas cette recherche avant le tri.
5. Utilisez `std::string` pour construire et afficher un court bilan du groupe.

**Squelette de départ :**

```cpp {linenos=table}
#include <iostream>
#include <string>

int main()
{
    int notes[5] = {70, 85, 60, 90, 75};
    std::string titre = "Notes du groupe";
    std::cout << titre << '\n';

    // Etape 1 : afficher les cinq notes.
    // Ajouter ensuite les fonctions demandees.
    return 0;
}
```

{{< boite type="remarque" titre="Critères de vérification" >}}
Pour les notes `70, 85, 60, 90, 75`, la moyenne attendue est `76`. Après le tri croissant, le tableau doit contenir `60, 70, 75, 85, 90`. La recherche de `85` renvoie alors l'indice `3`, et la recherche de `100` doit indiquer l'absence de résultat (`-1`).
{{< /boite >}}

### 8.2. Questions de révision {#questions-de-revision}

1. Pourquoi une variable locale déclarée dans une fonction ne peut-elle pas être utilisée directement dans une autre ?
2. Quelle différence observe-t-on entre un paramètre `int x` et un paramètre `int& x` ?
3. Pourquoi une recherche binaire ne peut-elle pas être appliquée sans précaution à un tableau non trié ?
4. Dans un tableau de cinq éléments, quel est le dernier indice valide ?
5. Que signifie `std::string::npos` après un appel à `find()` ?

## Synthèse finale du module {#synthese-finale-du-module}

{{< boite type="important" titre="Ce qu'il faut maîtriser avant de passer à la suite" >}}

| Notion | Vérification rapide |
|---|---|
| Fonctions | Savoir écrire, appeler et tester une fonction, avec ou sans prototype. |
| Paramètres et portée | Distinguer paramètres et arguments, variables locales et valeur renvoyée. |
| Passage par valeur / référence | Expliquer quelle variable est modifiée et pourquoi. |
| Surcharge | Distinguer les fonctions par leur liste de paramètres, pas seulement par leur type de retour. |
| Tableaux | Déclarer, initialiser et parcourir un tableau sans sortir de ses limites. |
| Tableaux 2D | Accéder à une case grâce aux indices de ligne et de colonne. |
| Recherche et tri | Distinguer recherche linéaire, tri à bulle et recherche binaire sur tableau trié. |
| Chaînes | Utiliser `std::string`, ses méthodes et reconnaître les contraintes des chaînes C. |

{{< /boite >}}

{{< boite type="synthese" titre="Synthèse – lecture rapide" >}}
Les fonctions, les paramètres et la portée des variables permettent de mieux organiser les traitements. Les tableaux stockent des ensembles de valeurs, tandis que les algorithmes de recherche et de tri permettent de les exploiter. Les objets `std::string` illustrent enfin des opérations accessibles par des méthodes. Ces notions préparent l'écriture de programmes utilisant des classes et des objets.
{{< /boite >}}

## Lecture complémentaire (facultative) : `inline` et `static` {#lecture-complementaire-facultative-inline-et-static}

### Le mot clé `inline` {#le-mot-cle-inline}

Lorsqu'une fonction est appelée, le programme exécute les instructions qu'elle contient, puis reprend son exécution à l'endroit où l'appel a été effectué. Dans certains cas, notamment pour des fonctions très courtes, le compilateur peut optimiser cette opération en remplaçant directement l'appel par les instructions de la fonction. On parle alors de **développement en ligne** (*inlining*).

Considérons la fonction suivante :

```cpp {linenos=table}
inline int carre(int x)
{
    return x * x;
}

int main()
{
    int resultat = carre(5);
    return 0;
}
```

La fonction `carre()` retourne le carré de son argument. Dans cet exemple, `carre(5)` retourne donc 25.

Le compilateur peut choisir de remplacer l'appel à `carre(5)` par le calcul `5 * 5`, évitant ainsi un appel de fonction. Cependant, **le mot clé `inline` ne garantit pas cette optimisation**. Le compilateur décide lui-même si cette transformation est avantageuse et peut également l'effectuer sans le mot clé `inline`.

En C++ moderne, le rôle principal de `inline` concerne également l'organisation du code dans plusieurs fichiers. Dans un projet comportant plusieurs fichiers `.cpp`, certaines fonctions peuvent être définies directement dans des fichiers d'en-tête (`.h` ou `.hpp`).

Par exemple, la définition suivante peut être placée dans un fichier `calculs.hpp` :

```cpp {linenos=table}
// Fichier calculs.hpp
#pragma once

inline int carre(int x)
{
    return x * x;
}
```

Plusieurs fichiers `.cpp` peuvent ensuite inclure cet en-tête et utiliser la fonction. Le mot clé `inline` permet que la même définition soit présente dans plusieurs unités de traduction, à condition de respecter les règles du langage concernant les définitions identiques.

Une **unité de traduction** correspond, de manière simplifiée, à un fichier source `.cpp` accompagné du contenu des fichiers d'en-tête qu'il inclut lors de la compilation.

Sans `inline`, placer la définition d'une fonction ordinaire dans un en-tête inclus par plusieurs fichiers `.cpp` peut provoquer une erreur de définitions multiples lors de l'édition des liens.

{{< boite type="important" >}}
Le mot clé `inline` ne doit pas être considéré comme une commande permettant d'accélérer automatiquement un programme. Son utilisation est notamment pertinente pour définir certaines fonctions directement dans les fichiers d'en-tête.

Pour les programmes simples composés d'un seul fichier `.cpp`, son utilisation n'est généralement pas nécessaire.
{{< /boite >}}

### Le mot clé `static` appliqué à une fonction libre {#le-mot-cle-static-applique-a-une-fonction-libre}

Dans un programme constitué de plusieurs fichiers `.cpp`, certaines fonctions sont destinées à être utilisées uniquement à l'intérieur du fichier où elles sont définies.

Le mot clé `static`, lorsqu'il est appliqué à une fonction libre au niveau de l'espace de noms, permet de limiter la **liaison de son nom au fichier source concerné**.

Considérons l'exemple suivant :

```cpp {linenos=table}
// Fichier calculs.cpp

static int sommeLocale(int a, int b)
{
    return a + b;
}

int calculerTotal(int prix, int frais)
{
    return sommeLocale(prix, frais);
}
```

Dans cet exemple, deux fonctions sont définies :

- `sommeLocale()` est une fonction auxiliaire qui additionne deux entiers. Le mot clé `static` limite son utilisation par son nom à cette unité de traduction.
- `calculerTotal()` utilise `sommeLocale()` pour effectuer son calcul. Elle possède une liaison externe et peut donc être appelée depuis un autre fichier `.cpp`, à condition qu'une déclaration appropriée y soit accessible.

Cette distinction permet de séparer les fonctions destinées à être utilisées par d'autres parties du programme de celles qui servent uniquement à réaliser des opérations internes.

Par exemple, dans un logiciel de gestion des stocks, une fonction auxiliaire qui effectue un calcul intermédiaire pourrait être déclarée `static`, tandis qu'une fonction principale permettant de calculer le montant d'une commande serait accessible depuis d'autres fichiers.

Cette organisation limite les conflits de noms entre les fichiers d’un projet.

{{< boite type="remarque" titre="Remarque" >}}
Le mot clé `static` possède plusieurs significations en C++, selon le contexte dans lequel il est utilisé.

Lorsqu'il est appliqué à une fonction libre au niveau de l'espace de noms, comme dans cet exemple, il lui donne une **liaison interne**. Cela signifie que son nom n'est pas accessible directement depuis les autres unités de traduction.

Cette utilisation est différente de celle d'une variable locale `static`, qui conserve sa valeur entre plusieurs appels d'une fonction, ou d'un membre `static` d'une classe, qui sera étudié ultérieurement.

En C++ moderne, on utilise également les espaces de noms anonymes pour limiter la liaison de fonctions et d'autres éléments à une unité de traduction.
{{< /boite >}}
