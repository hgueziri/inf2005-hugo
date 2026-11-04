---
title: "Module 2 : Premiers pas en C++, entrées-sorties, opérateurs et structures de contrôle"
linkTitle: "Module 2"
description: "INF 2005 – Programmation orientée objet avec C++"
weight: 20
bookCollapseSection: true
---

{{< figure-cours src="figures/banner_2.png" alt="Bannière du cours INF 2005 – Programmation orientée objet avec C++" largeur="100%" >}}

# Module 2 : Premiers pas en C++, entrées-sorties, opérateurs et structures de contrôle

{{< boite type="objectif" >}}
À la fin de ce module, l'étudiante ou l'étudiant devrait être capable de :

- créer un fichier source C++, le compiler et exécuter le programme obtenu ;
- distinguer le rôle de l'éditeur, du compilateur, du terminal et du programme exécutable ;
- identifier et corriger quelques erreurs de compilation courantes ;
- déclarer, initialiser et modifier des variables de types simples ;
- lire et afficher des données avec `std::cin` et `std::cout` ;
- utiliser les opérateurs arithmétiques, d'affectation, relationnels et logiques ;
- écrire des conditions avec `if`, `else if`, `else` et `switch` ;
- programmer des boucles avec `while`, `do/while` et `for`, et expliquer l'effet de `break`, `continue` et `return`.

{{< /boite >}}

{{< boite type="contenu" >}}
**Contenu du module :** passer de la création d'un premier programme C++ à la réalisation de programmes interactifs utilisant des variables, des calculs, des conditions et des boucles.
{{< /boite >}}

## Table des matières {#table-des-matieres}

- [1 Introduction et première compilation en C++](#introduction-et-premiere-compilation-en-c)
  - [1.1 Comprendre le rôle des outils](#comprendre-le-role-des-outils)
  - [1.2 Préparer son environnement de travail](#preparer-son-environnement-de-travail)
  - [1.3 Tutoriel guidé : créer, compiler et exécuter son premier programme](#tutoriel-guide-creer-compiler-et-executer-son-premier-programme)
    - [1.3.1 Étape 1 : créer et enregistrer main.cpp](#etape-1-creer-et-enregistrer-main-cpp)
    - [1.3.2 Étape 2 : compiler le programme](#etape-2-compiler-le-programme)
    - [1.3.3 Étape 3 : exécuter et observer le résultat](#etape-3-executer-et-observer-le-resultat)
    - [1.3.4 Étape 4 : modifier, recompiler et vérifier](#etape-4-modifier-recompiler-et-verifier)
    - [1.3.5 Étape 5 : provoquer et corriger une erreur](#etape-5-provoquer-et-corriger-une-erreur)
    - [1.3.6 Comprendre chaque ligne](#comprendre-chaque-ligne)
  - [1.4 Parcours alternatif : Google Colab et Jupyter Notebook](#parcours-alternatif-google-colab-et-jupyter-notebook)
  - [1.5 Ressources complémentaires facultatives](#ressources-complementaires-facultatives)
- [2 Variables, types de données et affectation](#variables-types-de-donnees-et-affectation)
  - [2.1 Déclarer et initialiser une variable](#declarer-et-initialiser-une-variable)
  - [2.2 Lire et modifier une valeur](#lire-et-modifier-une-valeur)
  - [2.3 Identifier les mots clés du langage](#identifier-les-mots-cles-du-langage)
- [3 Les entrées-sorties](#les-entrees-sorties)
  - [3.1 Afficher du texte et des valeurs](#afficher-du-texte-et-des-valeurs)
  - [3.2 Lire une valeur au clavier](#lire-une-valeur-au-clavier)
  - [3.3 Lire du texte et ses limites](#lire-du-texte-et-ses-limites)
- [4 Opérateurs et expressions](#operateurs-et-expressions)
  - [4.1 Calculs arithmétiques et conversions](#calculs-arithmetiques-et-conversions)
  - [4.2 Affectation simple et composée](#affectation-simple-et-composee)
  - [4.3 Incrémentation et décrémentation](#incrementation-et-decrementation)
  - [4.4 Comparer des valeurs](#comparer-des-valeurs)
  - [4.5 Combiner les conditions : opérateurs logiques](#combiner-les-conditions-operateurs-logiques)
  - [4.6 Priorité des opérateurs](#priorite-des-operateurs)
- [5 Structures conditionnelles](#structures-conditionnelles)
  - [5.1 La structure if](#la-structure-if)
  - [5.2 Les structures if/else et else if](#les-structures-if-else-et-else-if)
  - [5.3 L'opérateur conditionnel ?:](#l-operateur-conditionnel)
  - [5.4 La structure switch](#la-structure-switch)
- [6 Structures répétitives et instructions de contrôle](#structures-repetitives-et-instructions-de-controle)
  - [6.1 La boucle while](#la-boucle-while)
  - [6.2 La boucle do/while](#la-boucle-do-while)
  - [6.3 La boucle for](#la-boucle-for)
  - [6.4 Suivre l'exécution pas à pas](#suivre-l-execution-pas-a-pas)
  - [6.5 Modifier le contrôle : break, continue, return](#modifier-le-controle-break-continue-return)
- [7 Activités de consolidation et synthèse](#activites-de-consolidation-et-synthese)
  - [7.1 Trois activités de difficulté progressive](#trois-activites-de-difficulte-progressive)
  - [7.2 Étude de cas : premier menu de gestion d'inventaire](#etude-de-cas-premier-menu-de-gestion-d-inventaire)

## 1. Introduction et première compilation en C++ {#introduction-et-premiere-compilation-en-c}

Dans le module 1, nous avons étudié les notions d'objet, de classe, d'attribut et de méthode. Avant de programmer des classes en C++, il faut apprendre à écrire des instructions, à les faire exécuter et à vérifier leurs résultats. Ce module introduit ces bases à travers de petits programmes exécutés dans un terminal.

Pour commencer, il suffit de savoir créer et enregistrer un fichier sur son ordinateur. Aucune connaissance préalable de la compilation n'est supposée. Les exemples sont compatibles avec C++17. Ils utilisent d'abord uniquement l'affichage, puis introduisent progressivement les variables, les opérations, les conditions et les boucles.

### 1.1. Comprendre le rôle des outils {#comprendre-le-role-des-outils}

{{< boite type="definition" >}}
Un **fichier source** (par exemple `main.cpp`) contient les instructions écrites par le programmeur. Le **compilateur C++** (ici `g++`) traduit ce code et produit, si aucune erreur bloquante n'est détectée, un **programme exécutable**. Le **terminal** permet de lancer la compilation, puis le programme. **VS Code** sert principalement à écrire et à modifier le fichier ; il ne remplace pas le compilateur.
{{< /boite >}}

{{< figure-cours src="figures/chaine_compilation.svg" alt="Code source main.cpp, puis compilation avec g++, puis exécutable main, puis exécution et résultat." largeur="68%" >}}

{{< boite type="important" >}}
**Le cycle à retenir :** écrire ou modifier le fichier `.cpp` → l'enregistrer → compiler → exécuter → observer le résultat. Une modification du fichier source ne change pas l'exécutable déjà produit : il faut recompiler.
{{< /boite >}}

### 1.2. Préparer son environnement de travail {#preparer-son-environnement-de-travail}

Dans ce cours, **VS Code avec le compilateur `g++`** constitue le parcours principal. Google Colab permet de suivre une variante sans installation locale. Jupyter Notebook est également utilisable lorsqu'un environnement compatible est configuré. Il n'est pas nécessaire d'utiliser les trois outils : choisissez un parcours et conservez-le pour les premiers exercices.

{{< tableau >}}
| Outil | Rôle et prérequis |
|---|---|
| [VS Code](https://code.visualstudio.com/download) + `g++` | Écrire des programmes dans des fichiers `.cpp`, les compiler et les exécuter depuis le terminal. VS Code et un compilateur doivent être installés. |
| [Google Colab](https://colab.research.google.com/) | Créer un fichier `.cpp` dans un notebook et lancer `g++` dans un environnement en ligne, avec un compte et une connexion Internet. |
| [Jupyter Notebook](https://jupyter.org/install) | Même principe dans un notebook local, à condition de disposer de Python/IPython, de `g++` et d'un environnement compatible avec les commandes du tutoriel. |
{{< /tableau >}}

**Vérifier le compilateur.** Si vous choisissez VS Code, installez d'abord un compilateur C++ : par exemple MinGW-w64 via MSYS2 sous Windows, les outils de compilation GCC sous Linux ou les outils de ligne de commande Xcode/Clang sous macOS. Pour suivre précisément les commandes `g++` du module sur macOS, vérifiez qu'une commande `g++` est disponible ; selon l'installation, elle peut lancer Clang.

- **Windows :** consultez les instructions officielles [Configurer VS Code et MinGW-w64 (MSYS2)](https://code.visualstudio.com/docs/cpp/config-mingw). Après l'installation, ouvrez un *nouveau* terminal pour que le chemin du compilateur soit pris en compte.
- **Linux (Ubuntu/Debian) :** consultez le [guide officiel GCC sous VS Code](https://code.visualstudio.com/docs/cpp/config-linux). Si nécessaire, installez `g++` à l'aide du gestionnaire de paquets de votre distribution.
- **macOS :** suivez le [guide officiel Clang sous VS Code](https://code.visualstudio.com/docs/cpp/config-clang-mac) ; les commandes de compilation peuvent être adaptées à `clang++`.

Dans VS Code, ouvrez *Terminal > Nouveau terminal*, puis saisissez :

```bash
g++ --version
```

Une indication de version ou de fournisseur doit s'afficher. Si la commande est inconnue, le compilateur est absent ou son dossier n'est pas accessible dans le *PATH*. Il faut corriger cette configuration avant de continuer.

### 1.3. Tutoriel guidé : créer, compiler et exécuter son premier programme {#tutoriel-guide-creer-compiler-et-executer-son-premier-programme}

#### 1.3.1. Étape 1 : créer et enregistrer main.cpp {#etape-1-creer-et-enregistrer-main-cpp}

Dans VS Code, créez un dossier nommé `premier_cpp`, ouvrez-le avec *Fichier > Ouvrir un dossier*, puis créez un fichier `main.cpp`. Copiez le programme complet suivant et enregistrez-le (*Ctrl+S* ou *Cmd+S*).

```cpp {linenos=table}
#include <iostream>

int main()
{
    std::cout << "Bienvenue au cours de C++ !" << std::endl;
    return 0;
}
```

#### 1.3.2. Étape 2 : compiler le programme {#etape-2-compiler-le-programme}

Ouvrez le terminal intégré dans le dossier `premier_cpp`. La commande ci-dessous doit être exécutée **dans le terminal, et non dans le fichier C++** :

```bash
g++ -std=c++17 main.cpp -o main
```

{{< tableau >}}
| Élément | Signification |
|---|---|
| `g++` | Lance le compilateur C++. |
| `-std=c++17` | Choisit la norme C++17. |
| `main.cpp` | Nom du fichier source à compiler. |
| `-o main` | Demande de nommer `main` le programme produit (`main.exe` sous Windows). |
{{< /tableau >}}

{{< boite type="important" >}}
Une **compilation réussie peut ne rien afficher du tout**. Si aucune erreur n'est signalée et qu'un fichier exécutable apparaît dans le dossier, passez à l'étape suivante. En cas d'erreur, lisez la première ligne pertinente du diagnostic et vérifiez le nom du fichier et la syntaxe.
{{< /boite >}}

#### 1.3.3. Étape 3 : exécuter et observer le résultat {#etape-3-executer-et-observer-le-resultat}

Sous Linux, macOS et dans un terminal Bash compatible :

```bash
./main
```

Sous Windows avec PowerShell, après la compilation MinGW-w64 :

```bash
.\main.exe
```

Le programme doit afficher :

{{< boite type="code" titre="Syntaxe" >}}

```cpp
Bienvenue au cours de C++ !
```

{{< /boite >}}

#### 1.3.4. Étape 4 : modifier, recompiler et vérifier {#etape-4-modifier-recompiler-et-verifier}

Remplacez le message par `"Mon premier programme fonctionne !"`, enregistrez, puis relancez *les deux commandes* : compilation et exécution. Comparez le nouveau résultat avec l'ancien. Vous venez de réaliser un cycle complet de programmation.

#### 1.3.5. Étape 5 : provoquer et corriger une erreur {#etape-5-provoquer-et-corriger-une-erreur}

Supprimez volontairement le point-virgule qui termine l'instruction `std::cout`, enregistrez et compilez. Un diagnostic semblable à `expected ';' before 'return'` peut apparaître ; son libellé exact dépend du compilateur. Rétablissez le point-virgule, enregistrez, compilez de nouveau et exécutez.

{{< tableau >}}
| Symptôme | Vérification utile |
|---|---|
| `g++` introuvable | Vérifier l'installation et le chemin du compilateur. |
| `main.cpp` introuvable | Enregistrer le fichier et vérifier le dossier courant du terminal. |
| `expected ';'` ou erreur de syntaxe | Examiner les points-virgules, les accolades et les guillemets près de la ligne indiquée. |
| Le résultat n'a pas changé | Vérifier l'enregistrement et relancer la compilation avant l'exécution. |
| Le programme compile, mais le résultat est faux | Relire les calculs et la logique : il s'agit d'une erreur de comportement, pas de compilation. |
{{< /tableau >}}

#### 1.3.6. Comprendre chaque ligne {#comprendre-chaque-ligne}

{{< tableau >}}
| Code | Rôle |
|---|---|
| `#include <iostream>` | Rend disponibles les déclarations nécessaires pour l'affichage standard. |
| `int main()` | Définit la fonction qui sert de point d'entrée au programme. |
| `{ ... }` | Délimite le corps de la fonction. |
| `std::cout << ...` | Envoie le message vers la sortie standard, généralement le terminal. |
| `std::endl` | Insère un saut de ligne et vide le tampon de sortie (`'\n'` suffit souvent pour un simple saut de ligne). |
| `return 0;` | Termine explicitement `main` avec un code de succès. Cette instruction est facultative à la fin de `main`. |
{{< /tableau >}}

Les lignes commençant par `//` sont des commentaires : elles servent à expliquer le programme et ne sont pas exécutées. Chaque instruction simple se termine généralement par un point-virgule. Les accolades délimitent des blocs d'instructions.

{{< boite type="attention" >}}
Les formes anciennes `main()` sans type de retour et `#include <iostream.h>` ne conviennent pas au C++ moderne. Écrivez `int main()` et `#include <iostream>`.
{{< /boite >}}

### 1.4. Parcours alternatif : Google Colab et Jupyter Notebook {#parcours-alternatif-google-colab-et-jupyter-notebook}

Si vous ne pouvez pas installer VS Code et `g++`, ouvrez [Google Colab](https://colab.research.google.com/) et créez un notebook Python. Dans une **première cellule**, saisissez la commande spéciale `%%writefile`, suivie du programme C++. La commande `%%writefile main.cpp` permet de créer un fichier `main.cpp` sur le disque à partir du contenu de la cellule, qui pourra ensuite être compilé avec `g++`.

```text
%%writefile main.cpp
#include <iostream>

int main()
{
    std::cout << "Bienvenue au cours de C++ !" << std::endl;
    return 0;
}
```

Exécutez la cellule. Dans une **deuxième cellule** code, compilez puis exécutez le fichier :

```text
%%bash
g++ -std=c++17 main.cpp -o main
./main
```

Le résultat attendu est identique à celui de VS Code. Pour changer le programme, modifiez et réexécutez la première cellule, puis la deuxième. Le fichier et l'exécutable sont conservés dans l'environnement temporaire de la session ; ils peuvent disparaître à sa fermeture.

Dans **Jupyter Notebook local**, cette procédure suppose un noyau IPython avec les commandes `%%writefile` et `%%bash` ainsi qu'un environnement Bash où `g++` est installé. Sur Windows, une installation Jupyter standard ne fournit pas nécessairement Bash : privilégiez alors VS Code ou Colab.

{{< boite type="important" >}}
Quel que soit l'environnement, les instructions C++ restent les mêmes. Ce sont les étapes de création des fichiers et de lancement des commandes qui changent. Choisissez *un* parcours pour les activités de ce module.
{{< /boite >}}

### 1.5. Ressources complémentaires facultatives {#ressources-complementaires-facultatives}

Le présent tutoriel suffit pour réaliser les activités. Pour approfondir l'installation et voir la procédure en vidéo, vous pouvez consulter la [documentation officielle VS Code/MinGW-w64](https://code.visualstudio.com/docs/cpp/config-mingw) ou la vidéo YouTube [*Comment configurer Visual Studio Code pour C et C++ ?*](https://www.youtube.com/watch?v=wNsA4K3382k). Pour la syntaxe du langage et sa bibliothèque standard, la référence [cppreference](https://en.cppreference.com/w/) peut également être consultée. Ces ressources ne sont pas obligatoires.

{{< boite type="exemple" titre="Exemple guidé" >}}
**À faire avant de poursuivre :** exécutez le premier programme, modifiez son message, provoquez puis corrigez une erreur de syntaxe. Vous devez savoir répéter ces trois opérations sans suivre les instructions ligne par ligne.
{{< /boite >}}

## 2. Variables, types de données et affectation {#variables-types-de-donnees-et-affectation}

Après un programme qui affiche un message fixe, nous souhaitons manipuler des valeurs. Dans un programme de gestion de magasin, par exemple, il faut connaître la quantité d'articles en stock et pouvoir la modifier. Une **variable** associe un nom à une valeur d'un type donné.

### 2.1. Déclarer et initialiser une variable {#declarer-et-initialiser-une-variable}

```cpp {linenos=table}
int quantite = 5;           // entier
int prixUnitaire = 12;     // entier
int total = quantite * prixUnitaire;
std::cout << "Total : " << total << '\n';
```

Ce fragment suppose que l'on se trouve dans le corps d'une fonction et que `<iostream>` est inclus. Le premier exemple complet apparaît ci-dessous.

{{< tableau >}}
| Type | Utilisation typique |
|---|---|
| `int` | Nombre entier (quantité, âge, nombre d'articles). |
| `double` | Nombre avec partie décimale (prix, mesure). |
| `char` | Caractère unique, par exemple `'A'`. |
| `bool` | Valeur logique `true` ou `false`. |
| `std::string` | Texte, par exemple un nom ; nécessite `#include <string>`. |
{{< /tableau >}}

**Déclaration, initialisation et affectation** sont des opérations différentes :

```cpp {linenos=table}
int age;         // déclaration (pas de valeur garantie ici)
age = 20;        // affectation
int note = 85;   // déclaration avec initialisation
note = 90;      // nouvelle affectation
```

{{< boite type="attention" >}}
Une variable locale de type fondamental, comme `int age;`, ne reçoit pas automatiquement une valeur déterminée. Il faut lui donner une valeur avant de la lire. Pour débuter, privilégiez une initialisation explicite (par exemple `int age = 0;`).
{{< /boite >}}

### 2.2. Lire et modifier une valeur {#lire-et-modifier-une-valeur}

L'affectation `=` remplace la valeur d'une variable. Elle ne signifie pas « est égal à » comme en mathématiques. Ainsi, si `quantite` vaut 5, l'instruction `quantite = quantite + 2;` lui donne la valeur 7. La forme `quantite += 2;` exprime la même opération pour un entier.

```cpp {linenos=table}
#include <iostream>

int main()
{
    int quantite = 5;
    double prixUnitaire = 12.50;
    double valeur = quantite * prixUnitaire;

    std::cout << "Valeur du stock : " << valeur << '\n';
    return 0;
}
```

Le programme affiche `Valeur du stock : 62.5`. Testez-le en changeant `quantite` de 5 à 8, puis recompilez : le résultat doit devenir `100`.

### 2.3. Identifier les mots clés du langage {#identifier-les-mots-cles-du-langage}

Un **mot clé** est un terme réservé par C++ : il ne peut pas servir librement de nom de variable. Pour ce module, retenez surtout `int`, `double`, `char`, `bool`, `if`, `else`, `switch`, `for`, `while`, `do`, `break`, `continue` et `return`. Les mots clés `class`, `public`, `private` et `virtual` serviront plus tard pour les objets.

Les identificateurs (noms de variables ou de fonctions) peuvent contenir des lettres, des chiffres et le caractère de soulignement, mais ne doivent pas commencer par un chiffre. Ils distinguent les majuscules des minuscules : `note` et `Note` ne désignent pas la même variable. Évitez les espaces et les noms réservés comme `class` ou `return`.

{{< boite type="exemple" titre="Exemple guidé" >}}
**Vérification rapide :** dans `int stock = 5;`, repérez le type, le nom de la variable et sa valeur initiale. Puis modifiez le programme pour afficher la valeur du stock après l'ajout de trois articles.
{{< /boite >}}

## 3. Les entrées-sorties {#les-entrees-sorties}

Jusqu'ici, nos données étaient fixées dans le code source. Pour rendre un programme interactif, il faut pouvoir afficher des informations et lire des valeurs fournies par l'utilisateur. En C++, les entrées-sorties standard reposent sur des **flots**.

{{< boite type="definition" >}}
Un **flot** représente une source ou une destination de données. En pratique, `std::cin` lit généralement depuis le clavier, `std::cout` écrit vers le terminal et `std::cerr` est utilisé pour les messages d'erreur.
{{< /boite >}}

{{< tableau >}}
| Flot | Utilisation |
|---|---|
| `std::cout` | Afficher avec `<<` (insertion dans le flot). |
| `std::cin` | Lire avec `>>` (extraction du flot). |
| `std::cerr` | Afficher un message d'erreur. |
{{< /tableau >}}

Ces objets sont déclarés par l'en-tête `<iostream>` et appartiennent à l'espace de noms `std`. Le préfixe `std::` évite ici d'utiliser la directive générale `using namespace std;`.

### 3.1. Afficher du texte et des valeurs {#afficher-du-texte-et-des-valeurs}

```cpp {linenos=table}
int n = 30;
std::cout << "Valeur : " << n << '\n';
```

Les symboles `<<` permettent de chaîner plusieurs éléments. `'\n'` crée un saut de ligne ; `std::endl` produit également un saut de ligne, mais vide aussi le tampon du flot.

{{< boite type="exemple" titre="Exemple guidé" >}}
**À essayer :** dans le programme sur la valeur du stock, affichez aussi la quantité et le prix unitaire, chacun sur une ligne différente. Observez l'effet de plusieurs instructions `std::cout`.
{{< /boite >}}

### 3.2. Lire une valeur au clavier {#lire-une-valeur-au-clavier}

L'opérateur `>>` extrait une valeur du flot `std::cin` et la stocke dans une variable compatible. Exemple complet :

```cpp {linenos=table}
#include <iostream>

int main()
{
    int quantite = 0;
    std::cout << "Combien d'articles ? ";
    std::cin >> quantite;
    std::cout << "Quantite saisie : " << quantite << '\n';
    return 0;
}
```

Exécutez le programme, entrez `8`, puis appuyez sur Entrée. Le programme affiche `Quantite saisie : 8`. Si la saisie ne correspond pas à un entier, `std::cin` peut échouer ; le traitement détaillé des erreurs d'entrée sera abordé ultérieurement.

{{< boite type="attention" >}}
N'inversez pas les opérateurs : on affiche avec `std::cout << valeur;` et on lit avec `std::cin >> variable;`. L'opérateur `>>` lit généralement un mot à la fois lorsqu'il s'applique à `std::string`.
{{< /boite >}}

### 3.3. Lire du texte et ses limites {#lire-du-texte-et-ses-limites}

```cpp {linenos=table}
#include <iostream>
#include <string>

int main()
{
    std::string ville;
    std::cout << "Votre ville : ";
    std::cin >> ville;
    std::cout << "Vous habitez a " << ville << '\n';
    return 0;
}
```

Ce programme fonctionne pour `Montreal`, mais une saisie comme `Quebec City` n'est pas lue entièrement : l'extraction avec `>>` s'arrête au premier espace. Pour lire une ligne complète, on peut utiliser `std::getline(std::cin, ville);` lorsque la variable est de type `std::string`. Si vous combinez `>>` et `std::getline`, il faut faire attention au caractère de fin de ligne restant dans le flot.

{{< boite type="attention" >}}
Après une lecture avec `>>`, la fin de ligne produite par la touche Entrée reste dans le flot. Un appel à `std::getline()` placé juste après la trouve aussitôt : il renvoie une chaîne vide, sans attendre la saisie. Pour l'éviter, on peut d'abord ignorer les espaces et les fins de ligne restants avec `std::ws` :

```cpp {linenos=table}
int age = 0;
std::string nom;
std::cin >> age;
std::getline(std::cin >> std::ws, nom);
```

{{< /boite >}}

{{< boite type="exemple" titre="Exemple guidé" >}}
**Exercice guidé :** demandez à l'utilisateur la quantité et le prix unitaire d'un article, puis affichez leur produit. Pour commencer, reprenez le programme de lecture d'une quantité et ajoutez une variable `double prixUnitaire = 0.0;`, une deuxième instruction `std::cin` et une multiplication.
{{< /boite >}}

## 4. Opérateurs et expressions {#operateurs-et-expressions}

Une **expression** combine des valeurs, des variables et des opérateurs pour produire un résultat. Certaines expressions modifient aussi une variable, notamment les affectations et les incrémentations. Nous commençons par les calculs, puis abordons les tests logiques utiles aux conditions.

### 4.1. Calculs arithmétiques et conversions {#calculs-arithmetiques-et-conversions}

{{< tableau >}}
| Opérateur | Fonction |
|---|---|
| `+`, `-`, `*` | Addition, soustraction, multiplication. |
| `/` | Division : entière si les deux opérandes sont entiers. |
| `%` | Reste de la division entière (modulo). |
{{< /tableau >}}

```cpp {linenos=table}
#include <iostream>

int main()
{
    int a = 7;
    int b = 2;
    std::cout << a / b << '\n';  // 3 : division entiere
    std::cout << a % b << '\n';  // 1 : reste
    std::cout << 7.0 / b << '\n'; // 3.5 : division reelle
    return 0;
}
```

C++ autorise également des **expressions mixtes**. Par exemple, si `n` est de type `int` et `x` de type `double`, l'expression `n * x` est calculée en type `double` après conversion arithmétique appropriée. Les parenthèses précisent le regroupement des calculs : `(a + b) * c` diffère en général de `a + b * c`. Elles ne garantissent toutefois pas à elles seules l'ordre d'évaluation de tous les opérandes.

Dans un calcul, une valeur de type `char` est d'abord convertie en entier : l'expression `'A' + 1` vaut 66, le code de la lettre B, et elle est de type `int`. Pour obtenir un caractère, on range le résultat dans une variable de type `char`, par exemple `char suivante = 'A' + 1;`.

{{< boite type="attention" >}}
La division par zéro est invalide. Avant une division par une variable, il faut vérifier que son dénominateur n'est pas nul. Attention également : `7 / 2` produit `3`, même si le résultat est ensuite placé dans une variable `double`.
{{< /boite >}}

### 4.2. Affectation simple et composée {#affectation-simple-et-composee}

Lorsque `x` est initialisée, les écritures suivantes produisent la même valeur :

```cpp {linenos=table}
x = x + 8;
x += 8;   // forme composee de l'affectation
```

{{< tableau >}}
| Longue | Abrégée | Effet |
|---|---|---|
| `x = x + y;` | `x += y;` | Additionner `y`. |
| `x = x - y;` | `x -= y;` | Soustraire `y`. |
| `x = x * y;` | `x *= y;` | Multiplier par `y`. |
| `x = x / y;` | `x /= y;` | Diviser par `y` non nul. |
| `x = x % y;` | `x %= y;` | Calculer le reste pour des types entiers. |
{{< /tableau >}}

L'affectation est aussi une expression en C++ : `k = i = 5;` affecte 5 à `i`, puis à `k`. Cette écriture est valide, mais les affectations séparées sont souvent plus faciles à comprendre au début.

### 4.3. Incrémentation et décrémentation {#incrementation-et-decrementation}

Les opérateurs `++` et `--` augmentent ou diminuent de 1 la valeur de leur opérande modifiable. Dans une boucle, `i++` signifie simplement que `i` augmente de 1 à chaque itération.

{{< tableau >}}
| Expression | Valeur de l'expression |
|---|---|
| `++x` | Incrémente `x`, puis fournit sa nouvelle valeur. |
| `x++` | Fournit l'ancienne valeur de `x`, puis l'incrémente. |
| `--x` | Décrémente `x`, puis fournit sa nouvelle valeur. |
| `x--` | Fournit l'ancienne valeur de `x`, puis la décrémente. |
{{< /tableau >}}

```cpp {linenos=table}
int x = 5;
std::cout << x++ << '\n'; // affiche 5 ; x devient 6
std::cout << ++x << '\n'; // x devient 7 ; affiche 7
```

{{< boite type="important" >}}
Pour une première lecture d'une boucle, retenez surtout `i++` comme « ajouter 1 à `i` ». N'utilisez pas plusieurs modifications de la même variable dans une expression compliquée : privilégiez des instructions distinctes et faciles à vérifier.
{{< /boite >}}

### 4.4. Comparer des valeurs {#comparer-des-valeurs}

Les comparaisons produisent une valeur de type `bool` (`true` ou `false`).

{{< tableau >}}
| Opérateur | Sens |
|---|---|
| `==`, `!=` | Égal à, différent de. |
| `<`, `<=` | Inférieur à, inférieur ou égal à. |
| `>`, `>=` | Supérieur à, supérieur ou égal à. |
{{< /tableau >}}

{{< boite type="attention" >}}
Ne confondez pas `=` (affectation) et `==` (comparaison). Par exemple, `note == 50` vérifie si la note vaut 50 ; `note = 50` modifie la variable.
{{< /boite >}}

### 4.5. Combiner les conditions : opérateurs logiques {#combiner-les-conditions-operateurs-logiques}

Les opérateurs `&&` (ET), `||` (OU) et `!` (NON) permettent de composer plusieurs tests :

```cpp {linenos=table}
int note = 75;
bool valide = (note >= 0 && note <= 100); // true
bool admis = (note >= 50);                // true
bool absent = (note == -1);              // false
bool present = !absent;                  // true
```

{{< tableau >}}
| Opérateur | Résultat vrai lorsque... |
|---|---|
| `&&` | Les deux conditions sont vraies. |
| `\|\|` | Au moins une condition est vraie. |
| `!` | La condition est fausse. |
{{< /tableau >}}

Pour `&&`, la seconde condition n'est pas évaluée si la première est fausse ; pour `||`, elle n'est pas évaluée si la première est vraie. Ce fonctionnement est appelé *évaluation à court-circuit*. Par exemple, `(n != 0 && 10 / n > 2)` évite de calculer `10 / n` lorsque `n` vaut zéro.

### 4.6. Priorité des opérateurs {#priorite-des-operateurs}

Le tableau suivant résume les principales priorités, de la plus forte à la plus faible. L'associativité indique comment les opérateurs de même priorité se regroupent ; elle ne doit pas être confondue avec l'ordre réel d'évaluation des opérandes.

{{< tableau >}}
| Opérateurs | Associativité | Catégorie |
|---|---|---|
| `x++`, `x--`, appel `f()` | Gauche vers droite | Postfixes / appels |
| `++x`, `--x`, `!`, `+x`, `-x` | Droite vers gauche | Préfixes / unaires |
| `*`, `/`, `%` | Gauche vers droite | Multiplicatifs |
| `+`, `-` | Gauche vers droite | Additifs |
| `<<`, `>>` | Gauche vers droite | Décalage / insertion / extraction selon le type |
| `<`, `<=`, `>`, `>=` | Gauche vers droite | Comparaisons relationnelles |
| `==`, `!=` | Gauche vers droite | Égalité |
| `&&`, puis `\|\|` | Gauche vers droite | ET, puis OU logiques |
| `?:` | Droite vers gauche | Opérateur conditionnel |
| `=`, `+=`, `-=`, etc. | Droite vers gauche | Affectations |
{{< /tableau >}}

{{< boite type="exemple" titre="Exemple guidé" >}}
**Vérification :** prédisez la valeur de `(7 + 2) * 3`, puis celle de `7 + 2 * 3`. Compilez un petit programme qui affiche les deux résultats. **Réponses :** 27 puis 13.
{{< /boite >}}

## 5. Structures conditionnelles {#structures-conditionnelles}

Les structures conditionnelles permettent au programme de choisir les instructions à exécuter selon la valeur d'un test logique. Maintenant que nous savons produire des valeurs `bool`, nous pouvons employer ces tests dans `if`, `else if`, `else` ou `switch`.

### 5.1. La structure if {#la-structure-if}

Une instruction `if` exécute son bloc seulement lorsque la condition est vraie :

{{< boite type="code" titre="Syntaxe" >}}

```cpp
if (condition)
{
    instructions;
}
```

{{< /boite >}}

```cpp {linenos=table}
int note = 70;
if (note >= 50)
{
    std::cout << "Cours reussi" << '\n';
}
```

Ce fragment suppose que `<iostream>` est déjà inclus et que les instructions figurent dans `main`. Pour `note = 70`, le message apparaît ; pour `note = 40`, rien n'est affiché.

{{< figure-cours src="figures/figure_if.svg" numero="1" legende="Diagramme de contrôle de la structure `if`." alt="Diagramme de contrôle de la structure if." largeur="55%" >}}

### 5.2. Les structures if/else et else if {#les-structures-if-else-et-else-if}

Lorsque deux actions sont possibles, `if/else` permet d'en choisir une seule :

{{< boite type="code" titre="Syntaxe" >}}

```cpp
if (condition)
{
    action_si_vrai;
}
else
{
    action_si_faux;
}
```

{{< /boite >}}

```cpp {linenos=table}
int note = 45;
if (note >= 50)
{
    std::cout << "Cours reussi" << '\n';
}
else
{
    std::cout << "Cours echoue" << '\n';
}
```

{{< figure-cours src="figures/figure_if_else.svg" numero="2" legende="Diagramme de contrôle de la structure `if/else`." alt="Diagramme de contrôle de la structure if/else." largeur="90%" >}}

{{< boite type="important" >}}
Il est conseillé de conserver les accolades même lorsqu'un bloc ne contient qu'une instruction. Sans accolades, seule l'instruction qui suit immédiatement la condition est contrôlée.
{{< /boite >}}

Pour choisir parmi plusieurs intervalles, on utilise une chaîne de `else if`. Les tests sont évalués dans l'ordre, de haut en bas :

```cpp {linenos=table}
int note = 72;
if (note >= 75)
{
    std::cout << "A" << '\n';
}
else if (note >= 68)
{
    std::cout << "B" << '\n';
}
else if (note >= 60)
{
    std::cout << "C" << '\n';
}
else if (note >= 50)
{
    std::cout << "D" << '\n';
}
else
{
    std::cout << "E" << '\n';
}
```

Ici, la valeur 72 donne la cote `B`. Une note de 80 donne `A`, car le premier test est déjà vrai. On suppose dans cet exemple que les notes ont été validées et se situent entre 0 et 100.

### 5.3. L'opérateur conditionnel ?: {#l-operateur-conditionnel}

L'opérateur `?:` est une expression concise qui choisit entre deux valeurs :

```cpp {linenos=table}
int note = 70;
std::cout << (note >= 50 ? "Reussi" : "Echoue") << '\n';
```

Pour des traitements comportant plusieurs instructions, la structure `if/else` est généralement plus lisible.

### 5.4. La structure switch {#la-structure-switch}

La structure `switch` convient notamment à un choix parmi plusieurs valeurs entières, caractères ou énumérations. Chaque `case` correspond à une valeur possible, et `default` peut traiter les autres valeurs.

{{< boite type="code" titre="Syntaxe" >}}

```cpp
switch (choix)
{
    case 1:
        instructions;
        break;
    case 2:
        instructions;
        break;
    default:
        instructions;
}
```

{{< /boite >}}

{{< figure-cours src="figures/figure_switch.svg" numero="3" legende="Diagramme de contrôle de la structure `switch`." alt="Diagramme de contrôle de la structure switch." largeur="74%" >}}

```cpp {linenos=table}
#include <iostream>

int main()
{
    int choix = 0;
    std::cout << "1. Ajouter  2. Afficher : ";
    std::cin >> choix;

    switch (choix)
    {
        case 1:
            std::cout << "Ajouter un article" << '\n';
            break;
        case 2:
            std::cout << "Afficher les articles" << '\n';
            break;
        default:
            std::cout << "Choix invalide" << '\n';
    }
    return 0;
}
```

{{< boite type="important" >}}
`break` permet de quitter le `switch`. Sans `break`, l'exécution peut continuer dans le cas suivant : c'est la *chute* (*fallthrough*). Il faut en tenir compte lors de la conception du programme. Le `break` final de `default` est facultatif dans cet exemple.
{{< /boite >}}

Plusieurs étiquettes peuvent partager le même traitement : il suffit de les placer l'une après l'autre, puisque l'exécution se poursuit jusqu'au prochain `break`. Par exemple, pour accepter une réponse en majuscule ou en minuscule :

```cpp {linenos=table}
switch (reponse)
{
case 'o':
case 'O':
    std::cout << "Oui\n";
    break;
case 'n':
case 'N':
    std::cout << "Non\n";
    break;
default:
    std::cout << "Reponse invalide\n";
}
```

{{< boite type="exemple" titre="Exemple guidé" >}}
**À essayer :** exécutez le menu avec 1, 2, puis 9. Ajoutez ensuite un troisième choix qui affiche `Quitter`. Prédisez chaque sortie avant de compiler.
{{< /boite >}}

## 6. Structures répétitives et instructions de contrôle {#structures-repetitives-et-instructions-de-controle}

Les boucles exécutent plusieurs fois un groupe d'instructions. Elles reposent sur des conditions déjà étudiées, et utilisent souvent l'affectation composée ou l'incrémentation. Le problème de référence consiste à calculer `1 + 2 + ... + 10`, dont le résultat attendu est 55.

{{< tableau >}}
| Boucle | Quand l'employer ? | Particularité |
|---|---|---|
| `while` | Répéter tant que la condition est vraie. | Test avant la première itération. |
| `do/while` | Exécuter le bloc au moins une fois. | Test après la première itération. |
| `for` | Réunir initialisation, test et progression. | Trois éléments dans l'en-tête. |
{{< /tableau >}}

### 6.1. La boucle while {#la-boucle-while}

{{< boite type="code" titre="Syntaxe" >}}

```cpp
while (condition)
{
    instructions;
}
```

{{< /boite >}}

```cpp {linenos=table}
#include <iostream>

int main()
{
    int somme = 0;
    int i = 1;
    while (i <= 10)
    {
        somme += i;
        i++;
    }
    std::cout << "Somme : " << somme << '\n';
    return 0;
}
```

Au départ, `somme` vaut 0 et `i` vaut 1. À chaque passage, on ajoute `i` à `somme`, puis on augmente `i`. Lorsque `i` atteint 11, la condition devient fausse et la boucle s'arrête. Sans `i++`, la condition resterait vraie dans cet exemple : la boucle ne se terminerait pas normalement.

La boucle `while` convient aussi lorsque le nombre de répétitions n'est pas connu à l'avance. Par exemple, on peut lire des valeurs jusqu'à une **valeur sentinelle**, une valeur convenue qui signale la fin de la saisie et qui n'est pas une donnée à traiter :

```cpp {linenos=table}
int note = 0;
int somme = 0;
std::cout << "Note (-1 pour terminer) : ";
std::cin >> note;
while (note != -1)
{
    somme += note;
    std::cout << "Note (-1 pour terminer) : ";
    std::cin >> note;
}
std::cout << "Somme : " << somme << '\n';
```

La première valeur est lue avant la boucle, et chacune des suivantes à la fin d'un tour : la sentinelle arrête la boucle sans jamais être ajoutée à la somme.

### 6.2. La boucle do/while {#la-boucle-do-while}

La boucle `do/while` exécute son corps une première fois *avant* d'évaluer la condition :

{{< boite type="code" titre="Syntaxe" >}}

```cpp
do
{
    instructions;
} while (condition);
```

{{< /boite >}}

```cpp {linenos=table}
#include <iostream>

int main()
{
    int somme = 0;
    int i = 1;
    do
    {
        somme += i;
        i++;
    } while (i <= 10);
    std::cout << "Somme : " << somme << '\n';
    return 0;
}
```

La sortie est encore 55. Si `i` valait initialement 11, la version `while` ne ferait aucune addition, tandis que la version `do/while` effectuerait une addition avant le test. Pensez au point-virgule final après `while (condition)`.

### 6.3. La boucle for {#la-boucle-for}

`for` regroupe l'initialisation, la condition et la progression dans une seule instruction :

{{< boite type="code" titre="Syntaxe" >}}

```cpp
for (initialisation; condition; progression)
{
    instructions;
}
```

{{< /boite >}}

```cpp {linenos=table}
#include <iostream>

int main()
{
    int somme = 0;
    for (int i = 1; i <= 10; i++)
    {
        somme += i;
    }
    std::cout << "Somme : " << somme << '\n';
    return 0;
}
```

{{< figure-cours src="figures/figure_boucle_for.svg" numero="4" legende="Principe général d'une boucle contrôlée par une variable." alt="Principe général d'une boucle contrôlée par une variable." largeur="63%" >}}

### 6.4. Suivre l'exécution pas à pas {#suivre-l-execution-pas-a-pas}

Pour comprendre le fonctionnement d'une boucle, il est utile de noter l'état des variables après chaque itération. Pour alléger la table suivante, on limite temporairement le calcul à `i <= 5`.

{{< tableau >}}
| Itération | `i` | `somme` après ajout | Calcul |
|:---:|:---:|:---:|---|
| 1 | 1 | 1 | `0 + 1` |
| 2 | 2 | 3 | `1 + 2` |
| 3 | 3 | 6 | `3 + 3` |
| 4 | 4 | 10 | `6 + 4` |
| 5 | 5 | 15 | `10 + 5` |
{{< /tableau >}}

{{< boite type="exemple" titre="Exemple guidé" >}}
**À faire :** prédisez la somme pour `i <= 3`, puis modifiez l'une des boucles et vérifiez votre prédiction. Comparez aussi `while` et `do/while` avec une condition fausse dès le départ.
{{< /boite >}}

### 6.5. Modifier le contrôle : break, continue, return {#modifier-le-controle-break-continue-return}

Ces instructions n'ont pas le même effet : `break` quitte la boucle (ou le `switch`) ; `continue` ignore la fin de l'itération courante et passe à la suivante ; `return` quitte la fonction en cours.

```cpp {linenos=table}
#include <iostream>

int main()
{
    for (int i = 0; i < 5; i++)
    {
        if (i == 3)
        {
            break;
        }
        std::cout << i << ' ';
    }
    std::cout << '\n'; // affiche : 0 1 2
    return 0;
}
```

```cpp {linenos=table}
#include <iostream>

int main()
{
    for (int i = 0; i < 5; i++)
    {
        if (i == 3)
        {
            continue;
        }
        std::cout << i << ' ';
    }
    std::cout << '\n'; // affiche : 0 1 2 4
    return 0;
}
```

Dans `main`, `return 0;` termine le programme en indiquant une exécution réussie. Dans une autre fonction, `return` peut également transmettre une valeur à l'appelant. Nous reviendrons sur ce mécanisme lors de l'étude des fonctions.

Dans des boucles imbriquées, `break` et `continue` ne concernent que la boucle la plus intérieure qui les contient : un `break` placé dans la boucle intérieure la termine, puis la boucle extérieure passe à son tour suivant.

{{< boite type="important" >}}
Pour éviter une boucle infinie, vérifiez toujours que sa condition pourra devenir fausse ou qu'une sortie adaptée est prévue. Pour comprendre une boucle, tracez quelques itérations sur papier avant de l'exécuter.
{{< /boite >}}

## 7. Activités de consolidation et synthèse {#activites-de-consolidation-et-synthese}

Ce module constitue une introduction pratique aux instructions qui serviront ensuite à construire les méthodes des classes C++. L'objectif n'est pas de produire une application complète, mais d'être capable de lire, modifier, compiler et expliquer de petits programmes.

### 7.1. Trois activités de difficulté progressive {#trois-activites-de-difficulte-progressive}

1. **Reproduire :** recréez le premier programme `main.cpp`, compilez-le et exécutez-le. Modifiez son message, puis provoquez et corrigez une erreur de syntaxe.
2. **Modifier :** reprenez le programme de calcul de stock. Demandez à l'utilisateur une quantité et un prix unitaire, puis affichez la valeur calculée. Testez les saisies 4 et 2.5 : le résultat attendu est 10.
3. **Construire :** écrivez un programme qui lit une note entière entre 0 et 100, affiche `Reussi` si elle est supérieure ou égale à 50 et `Echoue` sinon. Si la note est hors limites, affichez `Note invalide`. Reprenez ensuite une boucle pour permettre trois évaluations successives.

### 7.2. Étude de cas : premier menu de gestion d'inventaire {#etude-de-cas-premier-menu-de-gestion-d-inventaire}

On souhaite offrir deux actions à l'utilisateur : ajouter des articles au stock et consulter la quantité disponible. Dans ce premier exercice, le stock est représenté par une simple variable entière, sans classe. La définition d'une classe `Article`, comme dans le module 1, sera possible dans la suite du cours.

```cpp {linenos=table}
#include <iostream>

int main()
{
    int stock = 5;
    int choix = 0;

    do
    {
        std::cout << "1. Ajouter  2. Afficher  0. Quitter : ";
        std::cin >> choix;

        switch (choix)
        {
            case 1:
            {
                int ajout = 0;
                std::cout << "Quantite a ajouter : ";
                std::cin >> ajout;
                if (ajout > 0)
                {
                    stock += ajout;
                }
                else
                {
                    std::cout << "Quantite invalide\n";
                }
                break;
            }
            case 2:
                std::cout << "Stock : " << stock << '\n';
                break;
            case 0:
                std::cout << "Au revoir\n";
                break;
            default:
                std::cout << "Choix invalide\n";
        }
    } while (choix != 0);

    return 0;
}
```

{{< boite type="attention" >}}
Pour rester centré sur les notions du module, cet exemple suppose que l'utilisateur saisit des nombres entiers valides. Il protège contre une quantité ajoutée négative ou nulle, mais ne gère pas encore les saisies non numériques, qui demanderaient un traitement supplémentaire de `std::cin`.
{{< /boite >}}

{{< boite type="exemple" titre="Exemple guidé" >}}
**Pour aller plus loin :** ajoutez un choix 3 permettant de retirer une quantité d'articles, sans autoriser un stock négatif. Avant de coder, écrivez les deux conditions à vérifier. Puis testez un retrait valide et un retrait supérieur au stock.
{{< /boite >}}

{{< boite type="synthese" titre="Synthèse – lecture rapide" >}}
**Avant de passer au module suivant**, vous devriez pouvoir : (1) créer, compiler et exécuter un programme ; (2) reconnaître une erreur de compilation et corriger des fautes simples ; (3) déclarer et initialiser des variables ; (4) lire et afficher des données ; (5) distinguer affectation et comparaison ; (6) construire des conditions et des boucles ; (7) expliquer l'effet de `break`, `continue` et `return`. Ces compétences seront réinvesties lorsque nous programmerons les comportements des objets dans des classes C++.
{{< /boite >}}
