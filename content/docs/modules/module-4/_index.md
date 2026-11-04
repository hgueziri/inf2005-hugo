---
title: "Module 4 : Héritage, polymorphisme et notions avancées essentielles"
linkTitle: "Module 4"
description: "INF 2005 – Programmation orientée objet avec C++"
weight: 40
bookCollapseSection: true
---

{{< figure-cours src="figures/banner_4.png" alt="Bannière du cours INF 2005 – Programmation orientée objet avec C++" largeur="100%" >}}

# Module 4 : Héritage, polymorphisme et notions avancées essentielles

{{< boite type="objectif" >}}
À la fin de ce module, l'étudiante ou l'étudiant devrait être capable de :

- définir une classe C++ simple, créer des objets et utiliser ses constructeurs et ses méthodes ;
- expliquer le principe de l'héritage et le rôle des classes dérivées ;
- distinguer l'héritage `public`, `protected` et `private` ;
- comprendre l'ordre d'appel des constructeurs et des destructeurs ;
- utiliser les fonctions virtuelles pour réaliser le polymorphisme ;
- reconnaître les cas d'héritage simple, multiple et d'héritage d'interface ;
- reconnaître les situations où une surcharge d'opérateur, une fonction amie ou le pointeur `this` sont utiles ;
- lire et écrire un fichier simple, utiliser un conteneur standard et reconnaître les piles et les arbres.

{{< /boite >}}

{{< boite type="contenu" >}}
**Contenu du module :** mettre en pratique les classes, les relations d'héritage et le polymorphisme, puis découvrir des mécanismes C++ complémentaires.
{{< /boite >}}

## Table des matières {#table-des-matieres}

- [1 Des objets aux classes C++ : première mise en pratique](#des-objets-aux-classes-c-premiere-mise-en-pratique)
  - [1.1 Pourquoi créer une classe ?](#pourquoi-creer-une-classe)
  - [1.2 Première classe : l'exemple d'un article](#premiere-classe-l-exemple-d-un-article)
  - [1.3 Exercice guidé : modifier puis vérifier](#exercice-guide-modifier-puis-verifier)
- [2 Héritage simple et classe dérivée](#heritage-simple-et-classe-derivee)
  - [2.1 La déclaration](#la-declaration)
  - [2.2 Accessibilité des membres hérités](#accessibilite-des-membres-herites)
  - [2.3 Les propriétés de l'héritage](#les-proprietes-de-l-heritage)
  - [2.4 Les constructeurs et les destructeurs](#les-constructeurs-et-les-destructeurs)
- [3 Polymorphisme et fonctions virtuelles](#polymorphisme-et-fonctions-virtuelles)
  - [3.1 Un premier appel polymorphe](#un-premier-appel-polymorphe)
  - [3.2 Fonctions virtuelles pures et classes abstraites](#fonctions-virtuelles-pures-et-classes-abstraites)
  - [3.3 Plusieurs objets à travers une interface commune](#plusieurs-objets-a-travers-une-interface-commune)
  - [3.4 Application : spécialisation des articles](#application-specialisation-des-articles)
- [4 Héritage multiple et interfaces (approfondissement)](#heritage-multiple-et-interfaces-approfondissement)
  - [4.1 Exemple de deux classes de base](#exemple-de-deux-classes-de-base)
  - [4.2 L'héritage multiple et le problème du losange](#l-heritage-multiple-et-le-probleme-du-losange)
  - [4.3 Étude de cas : héritage d'interface et d'implémentation](#etude-de-cas-heritage-d-interface-et-d-implementation)
- [5 Surcharge d'opérateurs](#surcharge-d-operateurs)
  - [5.1 Principes de base](#principes-de-base)
  - [5.2 Limitations](#limitations)
  - [5.3 Opérateurs d'insertion et d'extraction](#operateurs-d-insertion-et-d-extraction)
- [6 Fonctions et classes amies](#fonctions-et-classes-amies)
  - [6.1 Les fonctions amies](#les-fonctions-amies)
  - [6.2 Les classes amies](#les-classes-amies)
  - [6.3 L'utilisation du pointeur `this`](#l-utilisation-du-pointeur-this)
- [7 Lecture et écriture de fichiers](#lecture-et-ecriture-de-fichiers)
  - [7.1 Quelques classes de flots](#quelques-classes-de-flots)
  - [7.2 Lecture et écriture de fichiers](#lecture-et-ecriture-de-fichiers-2)
- [8 Structures de données : listes, piles et arbres (aperçu)](#structures-de-donnees-listes-piles-et-arbres-apercu)
  - [8.1 Les listes](#les-listes)
  - [8.2 Les piles](#les-piles)
  - [8.3 Les arbres](#les-arbres)
- [9 Bibliothèque standard et STL (aperçu)](#bibliotheque-standard-et-stl-apercu)
  - [9.1 Les conteneurs](#les-conteneurs)
  - [9.2 Les itérateurs](#les-iterateurs)
- [Synthèse finale du module](#synthese-finale-du-module)
- [Exercices de consolidation](#exercices-de-consolidation)

## 1. Des objets aux classes C++ : première mise en pratique {#des-objets-aux-classes-c-premiere-mise-en-pratique}

Dans le module 1, nous avons étudié les notions d'objet, de classe, d'attribut, de méthode et d'encapsulation. Les modules 2 et 3 ont permis de programmer des conditions, des boucles, des fonctions et des tableaux. Nous pouvons maintenant réunir ces connaissances pour écrire une classe C++ et créer des objets.

### 1.1. Pourquoi créer une classe ? {#pourquoi-creer-une-classe}

Considérons un inventaire contenant plusieurs articles. Chaque article possède un nom et une quantité en stock. Les opérations de consultation et d'ajout doivent s'appliquer à un article précis. Une classe permet de regrouper ces données et les opérations qui les manipulent.

{{< boite type="definition" >}}
Une **classe** décrit les attributs et les opérations communs à une famille d'objets. Un **objet**, aussi appelé **instance**, possède ses propres valeurs d'attributs. En C++, les données et les fonctions définies dans une classe sont appelées **membres**.
{{< /boite >}}

### 1.2. Première classe : l'exemple d'un article {#premiere-classe-l-exemple-d-un-article}

Voici un programme complet. Lisez d'abord les commentaires, puis compilez-le de la même manière que les programmes du module 2.

```cpp {linenos=table}
#include <iostream>
#include <string>

class Article {
private:
    std::string nom;
    int quantite;

public:
    Article(std::string n, int q) : nom(n), quantite(q) {}

    void ajouter(int nombre) {
        if (nombre > 0) {
            quantite += nombre;
        }
    }

    void afficher() const {
        std::cout << nom << " : " << quantite << " en stock\n";
    }
};

int main() {
    Article livre("Livre C++", 3);
    Article cahier("Cahier", 5);
    livre.ajouter(2);
    livre.afficher();
    cahier.afficher();
    return 0;
}
```

{{< boite type="exemple" titre="Résultat attendu :" >}}

```cpp
Livre C++ : 5 en stock
Cahier : 5 en stock
```

{{< /boite >}}

- `class Article` définit le modèle commun. Le point-virgule après l'accolade fermante est obligatoire pour terminer la définition de la classe.
- `private` réserve l'accès direct aux données `nom` et `quantite` aux membres autorisés de la classe. Un appel comme `livre.quantite = -3;` n'est donc pas permis depuis `main()`.
- `public` présente les opérations accessibles de l'extérieur : le constructeur et les méthodes `ajouter()` et `afficher()`.
- `Article(std::string n, int q)` est un **constructeur** : il initialise un objet au moment de sa création. La liste `: nom(n), quantite(q)` initialise ses attributs.
- `Article livre("Livre C++", 3);` crée un objet, alors que `Article cahier("Cahier", 5);` en crée un deuxième, indépendant du premier.
- L'appel `livre.ajouter(2);` exécute une méthode sur l'objet `livre`. L'écriture `const` après `afficher()` indique que cette méthode ne modifie pas l'état observable de l'objet.

{{< boite type="important" >}}
Le mot clé `class` décrit le type; la déclaration `Article livre(...);` crée un objet de ce type. Les valeurs des attributs appartiennent à chaque objet, mais les comportements sont définis par la classe.
{{< /boite >}}

{{< boite type="remarque" titre="Remarque" >}}

- Une classe peut offrir plusieurs constructeurs, qui se distinguent par leurs paramètres, comme des fonctions surchargées (module 3) : le compilateur choisit celui qui correspond aux arguments donnés à la création de l'objet.
- Seules les méthodes déclarées `const` peuvent être appelées sur un objet constant ou au moyen d'une référence constante, comme `const Article& a` : déclarez donc `const` toute méthode qui ne modifie pas l'objet.
- Un accesseur qui renvoie une référence non constante vers un attribut privé, par exemple `std::string& getNom()`, permet de modifier cet attribut de l'extérieur, comme s'il était public. Un accesseur renvoie plutôt une copie ou une référence constante, par exemple `const std::string& getNom() const`.

{{< /boite >}}

### 1.3. Exercice guidé : modifier puis vérifier {#exercice-guide-modifier-puis-verifier}

1. Créez un fichier `article.cpp`, copiez le programme et compilez-le avec `g++ -std=c++17 article.cpp -o article`. Exécutez-le.
2. Remplacez `livre.ajouter(2)` par `livre.ajouter(4)`. Prévoyez le résultat de l'affichage avant de recompiler.
3. Essayez `livre.ajouter(-2)`. Pourquoi la quantité ne diminue-t-elle pas ? Repérez la condition qui protège l'état de l'objet.
4. Essayez temporairement `livre.quantite = 10;` dans `main()`. Observez l'erreur de compilation, puis retirez cette instruction.

Nous avons maintenant une première classe fonctionnelle. L'**héritage**, présenté dans la section suivante, permet de définir des classes plus spécialisées à partir d'une classe existante.

## 2. Héritage simple et classe dérivée {#heritage-simple-et-classe-derivee}

L'héritage est l'un des mécanismes centraux de la programmation orientée objet. Il permet de définir une nouvelle classe à partir d'une classe existante. La classe existante est appelée **classe de base**, **classe mère** ou **superclasse**. La nouvelle classe est appelée **classe dérivée** ou **classe fille**.

L'idée principale est de factoriser les éléments communs dans la classe de base, puis d'ajouter ou de redéfinir des éléments dans les classes dérivées. On utilise normalement l'héritage public lorsqu'un objet dérivé peut également être considéré comme un objet de sa classe de base (relation « est un »). Par exemple, dans un système de gestion du personnel, les classes `PersonnelInformatique` et `PersonnelComptable` peuvent hériter d'une classe `Personne` qui contient les attributs communs comme le nom, le prénom ou la date de naissance.

{{< figure-cours src="figures/fig01_heritage_relation.png" numero="1" legende="Principe général d'une relation d'héritage." largeur="88%" >}}

{{< boite type="important" >}}
Une classe dérivée hérite des membres de sa classe de base selon le mode d'héritage utilisé. Elle peut aussi ajouter ses propres attributs et méthodes, ou redéfinir certaines méthodes de la classe de base.
{{< /boite >}}

### 2.1. La déclaration {#la-declaration}

La déclaration d'un héritage en C++ se fait avec le symbole ":" (deux-points) après le nom de la classe dérivée. On indique ensuite le mode d'accès et le nom de la classe de base.

```cpp {linenos=table}
class ClasseDerivee : public ClasseBase {
    // membres propres a la classe derivee
};
```

Exemple complet : la classe spécialisée réutilise le constructeur et la méthode publique de sa classe de base. Il suffit de copier le programme dans un fichier `.cpp` pour l'exécuter :

```cpp {linenos=table}
#include <iostream>
#include <string>

class Personne {
protected:
    std::string nom;
    std::string prenom;

public:
    Personne(std::string n, std::string p) : nom(n), prenom(p) {}

    void afficherIdentite() const {
        std::cout << prenom << " " << nom << std::endl;
    }
};

class PersonnelInformatique : public Personne {
private:
    std::string specialite;

public:
    PersonnelInformatique(std::string n, std::string p, std::string s)
        : Personne(n, p), specialite(s) {}

    void afficherProfil() const {
        afficherIdentite();
        std::cout << "Specialite : " << specialite << std::endl;
    }
};

int main() {
    PersonnelInformatique p("Durand", "Alice", "Reseaux");
    p.afficherProfil();
    return 0;
}
```

{{< boite type="remarque" titre="Remarque" >}}
Dans une classe, les membres sont `private` par défaut. Dans une structure `struct`, ils sont `public` par défaut. Le mode d'héritage par défaut est également différent : `private` pour une `class` et `public` pour une `struct`. Pour un héritage destiné à représenter une relation « est-un », le mode `public` est généralement le plus approprié.
{{< /boite >}}

### 2.2. Accessibilité des membres hérités {#accessibilite-des-membres-herites}

Le mode d'héritage influence l'accessibilité des membres de la classe de base lorsqu'ils sont utilisés à travers une classe dérivée. Ce mode ne modifie pas la déclaration originale de la classe de base.

{{< tableau >}}
| Membre dans la base | Héritage public | Héritage protected | Héritage private |
|---|---|---|---|
| `public` | reste `public` | devient `protected` | devient `private` |
| `protected` | reste `protected` | reste `protected` | devient `private` |
| `private` | inaccessible directement dans la dérivée | inaccessible directement dans la dérivée | inaccessible directement dans la dérivée |
{{< /tableau >}}

{{< boite type="attention" >}}
Un membre `private` de la classe de base existe bien dans l'objet dérivé, mais il n'est pas accessible directement depuis la classe dérivée. Il faut passer par les méthodes publiques ou protégées prévues par la classe de base.
{{< /boite >}}

### 2.3. Les propriétés de l'héritage {#les-proprietes-de-l-heritage}

L'héritage possède plusieurs propriétés importantes. L'exemple précédent illustre déjà l'héritage simple, où une classe ne possède qu'une seule classe de base directe :

- une classe dérivée peut devenir à son tour une classe de base ;
- une classe dérivée peut ajouter des attributs et des méthodes ;
- une classe dérivée peut redéfinir des méthodes héritées ;
- les constructeurs et les destructeurs ne sont pas hérités comme des méthodes ordinaires (C++ permet toutefois l'héritage explicite de constructeurs avec une déclaration `using`) ;

L'héritage multiple, qui permet plusieurs classes de base directes, sera présenté plus loin comme mécanisme complémentaire.

### 2.4. Les constructeurs et les destructeurs {#les-constructeurs-et-les-destructeurs}

Lorsqu'un objet dérivé est construit, C++ construit d'abord les sous-objets correspondant à ses classes de base, puis les membres et le corps de son constructeur. La liste d'initialisation d'un constructeur dérivé peut appeler explicitement un constructeur de la base, comme `: Personne(n, p)` dans notre exemple. Lors de la destruction, l'ordre est inversé : le destructeur de la classe dérivée est exécuté avant celui de la classe de base.

{{< figure-cours src="figures/fig02_ordre_constructeurs_destructeurs.png" numero="2" legende="Ordre d'appel des constructeurs et destructeurs dans une hiérarchie." largeur="92%" >}}

Exemple :

```cpp {linenos=table}
#include <iostream>

class Base {
public:
    Base()  { std::cout << "Constructeur Base" << std::endl; }
    ~Base() { std::cout << "Destructeur Base" << std::endl; }
};

class Derivee : public Base {
public:
    Derivee()  { std::cout << "Constructeur Derivee" << std::endl; }
    ~Derivee() { std::cout << "Destructeur Derivee" << std::endl; }
};

int main() {
    Derivee objet;
    return 0;
}
```

{{< boite type="exemple" titre="Résultat attendu :" >}}

```cpp
Constructeur Base
Constructeur Derivee
Destructeur Derivee
Destructeur Base
```

{{< /boite >}}

{{< boite type="remarque" titre="Remarque" >}}
Pour une classe de base dont le constructeur attend des paramètres, la classe dérivée doit initialiser cette partie de l'objet, comme dans l'appel `Personne(n, p)`. Le destructeur d'une base destinée à être supprimée via un pointeur sur cette base sera normalement virtuel, un point approfondi dans la section sur le polymorphisme.
{{< /boite >}}

Le destructeur est appelé automatiquement lorsque l'objet cesse d'exister, par exemple à la sortie du bloc où il a été déclaré, que l'on en sorte normalement ou par un `return`. C'est donc l'endroit approprié pour libérer une ressource acquise par le constructeur, comme un fichier ou une connexion : sa libération ne peut plus être oubliée. Les flots de fichiers (section 7) se ferment ainsi automatiquement, et `std::lock_guard` (module 5) libère son mutex de la même manière.

## 3. Polymorphisme et fonctions virtuelles {#polymorphisme-et-fonctions-virtuelles}

Une relation d'héritage peut fournir une interface commune à plusieurs classes, mais cela ne suffit pas à obtenir un appel polymorphe. Pour réaliser le **polymorphisme dynamique**, on déclare une méthode `virtual` dans la classe de base et on la redéfinit dans les classes dérivées.

### 3.1. Un premier appel polymorphe {#un-premier-appel-polymorphe}

L'exemple suivant utilise une référence de type `Figure` qui désigne un objet de type `Cercle`. Le compilateur reconnaît l'interface `dessiner()`, mais la méthode réellement appelée dépend de l'objet désigné.

```cpp {linenos=table}
#include <iostream>

class Figure {
public:
    virtual ~Figure() = default;
    virtual void dessiner() const {
        std::cout << "Figure\n";
    }
};

class Cercle : public Figure {
public:
    void dessiner() const override {
        std::cout << "Cercle\n";
    }
};

int main() {
    Cercle cercle;
    Figure& figure = cercle;
    figure.dessiner();
    return 0;
}
```

{{< boite type="exemple" titre="Résultat attendu :" >}}
`Cercle`. La référence `figure` est déclarée avec le type `Figure`, mais elle désigne réellement un objet `Cercle`. Grâce à `virtual`, la version redéfinie est exécutée.
{{< /boite >}}

- `virtual` rend possible la sélection dynamique de la méthode lors d'un appel via un pointeur ou une référence de base.
- `override` demande au compilateur de vérifier que la méthode redéfinit bien une méthode virtuelle existante ; son utilisation évite plusieurs erreurs de signature.
- `Figure&` est une référence vers un objet de type `Figure` ou d'un type dérivé compatible.
- Un destructeur `virtual` est nécessaire lorsqu'on détruit un objet dérivé par un pointeur vers une base polymorphe, pour garantir la destruction complète.

{{< figure-cours src="figures/fig04_liaison_dynamique.png" numero="3" legende="Liaison dynamique avec une fonction virtuelle." largeur="88%" >}}

{{< boite type="attention" >}}
Si la méthode `dessiner()` de la classe de base n'était pas virtuelle, l'appel via la référence `Figure&` sélectionnerait la version de `Figure`, même lorsque l'objet réel est un `Cercle`. Le polymorphisme n'est donc pas simplement le fait de donner le même nom à deux méthodes.
{{< /boite >}}

Pour redéfinir une fonction virtuelle, la méthode de la classe dérivée doit avoir exactement la même signature, qualificatif `const` compris. Dans `Cercle`, une méthode `void dessiner()` sans `const` serait une nouvelle méthode, qui ne redéfinit pas celle de `Figure` : l'appel au moyen de `Figure&` exécuterait toujours la version de `Figure`. Avec `override`, le compilateur signale cette erreur.

### 3.2. Fonctions virtuelles pures et classes abstraites {#fonctions-virtuelles-pures-et-classes-abstraites}

Il arrive qu'une classe de base définisse une opération commune sans pouvoir en fournir une implémentation adaptée. Une **fonction virtuelle pure** est déclarée avec `= 0`. Une classe qui possède au moins une fonction virtuelle pure est **abstraite** : on ne peut pas en créer directement d'objet.

```cpp {linenos=table}
class Figure {
public:
    virtual ~Figure() = default;
    virtual double aire() const = 0;
};
```

Une classe dérivée concrète doit fournir les redéfinitions nécessaires des fonctions virtuelles pures héritées. La classe abstraite joue ainsi le rôle de **contrat commun**.

### 3.3. Plusieurs objets à travers une interface commune {#plusieurs-objets-a-travers-une-interface-commune}

Nous pouvons conserver différents types de figures dans un même conteneur en utilisant des pointeurs vers la classe de base. L'exemple suivant introduit deux outils de la bibliothèque standard : `std::vector` (une collection extensible) et `std::unique_ptr` (un pointeur qui gère automatiquement la durée de vie de l'objet).

```cpp {linenos=table}
#include <iostream>
#include <memory>
#include <vector>

class Figure {
public:
    virtual ~Figure() = default;
    virtual void dessiner() const = 0;
};

class Cercle : public Figure {
public:
    void dessiner() const override { std::cout << "Cercle\n"; }
};

class Rectangle : public Figure {
public:
    void dessiner() const override { std::cout << "Rectangle\n"; }
};

int main() {
    std::vector<std::unique_ptr<Figure>> figures;
    figures.push_back(std::make_unique<Cercle>());
    figures.push_back(std::make_unique<Rectangle>());

    for (const auto& figure : figures) {
        figure->dessiner();
    }
    return 0;
}
```

{{< boite type="exemple" titre="Résultat attendu :" >}}
`Cercle` sur la première ligne, puis `Rectangle` sur la deuxième. La même instruction `figure->dessiner()` produit deux comportements distincts.
{{< /boite >}}

{{< boite type="important" >}}
Pour les premiers exercices, retenez surtout la combinaison `virtual` dans la base, `override` dans les classes dérivées et un appel via une référence ou un pointeur de type base. `vector` et `unique_ptr` sont des outils complémentaires ; leur fonctionnement détaillé n'est pas nécessaire pour comprendre l'appel polymorphe.
{{< /boite >}}

{{< boite type="attention" >}}
Le polymorphisme exige de manipuler les objets dérivés au moyen de pointeurs ou de références vers la classe de base. Si `Figure` n'était pas abstraite, un `std::vector<Figure>` ne contiendrait que des objets `Figure` : en y copiant un `Cercle`, on ne conserverait que sa partie `Figure`. C'est le **découpage** de l'objet (*slicing*), et `dessiner()` exécuterait alors la version de `Figure`. Le même découpage se produit lorsqu'un objet dérivé est passé par valeur à un paramètre de type `Figure`.
{{< /boite >}}

### 3.4. Application : spécialisation des articles {#application-specialisation-des-articles}

La dérivation permet de créer une classe plus spécifique. La redéfinition permet à une classe dérivée de fournir sa propre version d'une méthode héritée. Le polymorphisme permet ensuite d'appeler la bonne méthode à partir d'une référence ou d'un pointeur de la classe de base.

Reprenons l'exemple d'inventaire du module 1. Une boisson est un article ; une boisson spécialisée peut redéfinir la méthode de calcul du prix. Cet extrait illustre une hiérarchie à trois niveaux. Il sera complété par un appel en fin d'exemple.

```cpp {linenos=table}
#include <iostream>
#include <string>

class Article {
protected:
    std::string nom;
    double prix;
    int quantite;
    double coefficientTaxe;

public:
    Article(std::string n, double p, int q = 0, double t = 1.15)
        : nom(n), prix(p), quantite(q), coefficientTaxe(t) {}

    virtual ~Article() = default;

    virtual double prixAvecTaxe() const {
        return prix * coefficientTaxe * quantite;
    }

    virtual void afficher() const {
        std::cout << nom << " : " << prixAvecTaxe() << std::endl;
    }
};

class Boisson : public Article {
protected:
    int volume;

public:
    Boisson(std::string n, double p, int v, int q = 0)
        : Article(n, p, q), volume(v) {}

    int getVolume() const { return volume; }
};

class BoissonAlcoolisee : public Boisson {
private:
    double majoration;

public:
    BoissonAlcoolisee(std::string n, double p, int v, double tA, int q = 0)
        : Boisson(n, p, v, q), majoration(tA) {}

    double prixAvecTaxe() const override {
        return prix * (coefficientTaxe + majoration) * quantite;
    }
};

int main() {
    Boisson eau("Eau", 2.0, 500, 2);
    BoissonAlcoolisee speciale("Boisson", 4.0, 330, 0.10, 1);
    const Article& article = speciale;
    eau.afficher();
    article.afficher(); // liaison dynamique : prixAvecTaxe()
    return 0;
}
```

{{< boite type="remarque" titre="Remarque" >}}
Le constructeur initialise la quantité à `0` lorsqu'elle n'est pas fournie ; ici, nous précisons explicitement une quantité pour afficher des prix non nuls. Le coefficient `1.15` est un facteur multiplicatif fictif choisi pour l'exercice : il ne s'agit pas d'une règle fiscale générale. La majoration supplémentaire est également illustrative.
{{< /boite >}}

## 4. Héritage multiple et interfaces (approfondissement) {#heritage-multiple-et-interfaces-approfondissement}

L'héritage simple étudié jusqu'ici suffit à de nombreux programmes. C++ permet aussi de dériver une classe de plusieurs bases. Cette possibilité est utile dans certaines conceptions, mais elle peut rendre le code plus difficile à comprendre. Les exemples de cette section servent surtout à reconnaître le mécanisme et ses limites.

```cpp {linenos=table}
class ClasseDerivee : public Base1, public Base2 {
    // membres propres a la classe derivee
};
```

### 4.1. Exemple de deux classes de base {#exemple-de-deux-classes-de-base}

L'héritage simple relie une classe dérivée à une seule classe de base. L'héritage multiple relie une classe dérivée à plusieurs classes de base. L'héritage multiple peut être utile, mais il demande une conception plus prudente. L'exemple du point coloré ci-dessous illustre surtout la syntaxe et la résolution des noms : en conception réelle, une relation de composition peut être plus naturelle pour représenter la couleur d'un point.

{{< figure-cours src="figures/fig03_heritage_multiple_point_couleur.png" numero="4" legende="Exemple d'héritage multiple : un point coloré hérite de `Point` et de `Couleur`." alt="Exemple d'héritage multiple : un point coloré hérite de Point et de Couleur." largeur="80%" >}}

```cpp {linenos=table}
#include <iostream>

class Point {
protected:
    double x{}, y{};
public:
    void init(double abs, double ord) {
        x = abs;
        y = ord;
    }
    void afficher() const {
        std::cout << "(" << x << ", " << y << ")";
    }
};

class Couleur {
protected:
    int codeCouleur{};
public:
    void init(int c) {
        codeCouleur = c;
    }
    void afficher() const {
        std::cout << "couleur " << codeCouleur;
    }
};

class PointEnCouleur : public Point, public Couleur {
public:
    void init(double abs, double ord, int c) {
        Point::init(abs, ord);
        Couleur::init(c);
    }

    void afficher() const {
        Point::afficher();
        std::cout << " avec ";
        Couleur::afficher();
        std::cout << std::endl;
    }
};

int main() {
    PointEnCouleur p;
    p.init(2.0, 3.0, 4);
    p.afficher();
    return 0;
}
```

{{< boite type="attention" >}}
Quand deux classes de base contiennent une méthode portant le même nom, l'appel peut devenir ambigu. On utilise alors l'opérateur de résolution de portée `::`, par exemple `Point::afficher()` ou `Couleur::afficher()`.
{{< /boite >}}

### 4.2. L'héritage multiple et le problème du losange {#l-heritage-multiple-et-le-probleme-du-losange}

L'héritage multiple peut parfois créer une situation appelée « héritage en losange ». Elle apparaît lorsqu'une classe hérite de deux classes qui héritent elles-mêmes d'une même classe de base. Sans héritage virtuel des bases, l'objet final contient alors deux sous-objets de cette base commune ; l'accès à leurs membres peut devenir ambigu. L'héritage virtuel permet de partager un seul sous-objet de base commune, mais ce mécanisme dépasse les objectifs pratiques du présent module.

{{< figure-cours src="figures/fig05_heritage_losange.png" numero="5" legende="Exemple d'héritage en losange." largeur="78%" >}}

{{< boite type="remarque" titre="Remarque" >}}
Dans les conceptions modernes, l'héritage multiple est souvent réservé aux interfaces abstraites. Pour partager du comportement ou de l'état, la composition est souvent plus simple à maintenir.
{{< /boite >}}

### 4.3. Étude de cas : héritage d'interface et d'implémentation {#etude-de-cas-heritage-d-interface-et-d-implementation}

Une classe abstraite peut définir une interface commune sans imposer toute l'implémentation. Les classes dérivées choisissent ensuite comment réaliser les opérations. Dans l'exemple suivant, la navette sait à la fois se dessiner et se déplacer : elle implémente deux interfaces. Il s'agit d'un extrait qui sera utilisé par d'autres parties d'une application, et non d'un programme complet contenant `main()`.

```cpp {linenos=table}
#include <iostream>
#include <vector>
#include <memory>

class Dessinable {
public:
    virtual ~Dessinable() = default;
    virtual void dessiner() const = 0;
};

class Deplacable {
public:
    virtual ~Deplacable() = default;
    virtual void deplacer(int dx, int dy) = 0;
};

class Navette : public Dessinable, public Deplacable {
private:
    int x{}, y{};

public:
    void dessiner() const override {
        std::cout << "Dessiner la navette en (" << x << ", " << y << ")" << std::endl;
    }

    void deplacer(int dx, int dy) override {
        x += dx;
        y += dy;
    }
};
```

## 5. Surcharge d'opérateurs {#surcharge-d-operateurs}

La surcharge d'opérateurs permet de donner un comportement spécifique à certains opérateurs lorsqu'ils sont appliqués à des objets. L'objectif n'est pas de modifier le langage de manière arbitraire, mais de rendre le code plus naturel et plus lisible.

### 5.1. Principes de base {#principes-de-base}

La surcharge se fait avec le mot clé `operator`. Par exemple, pour additionner deux nombres complexes, on peut redéfinir l'opérateur `+`. La méthode `operator+` reçoit l'objet de droite en paramètre ; l'objet de gauche correspond à celui sur lequel la méthode est appelée.

{{< figure-cours src="figures/fig06_surcharge_operateur.png" numero="6" legende="Idée de la surcharge de l'opérateur `+`." alt="Idée de la surcharge de l'opérateur +." largeur="78%" >}}

```cpp {linenos=table}
#include <iostream>

class Complexe {
private:
    double reel;
    double imaginaire;

public:
    Complexe(double r = 0, double i = 0) : reel(r), imaginaire(i) {}

    Complexe operator+(const Complexe& autre) const {
        return Complexe(reel + autre.reel, imaginaire + autre.imaginaire);
    }

    void afficher() const {
        std::cout << reel << " + " << imaginaire << "i" << std::endl;
    }
};

int main() {
    Complexe c1(3, 2), c2(1, 5);
    Complexe c3 = c1 + c2;
    c3.afficher(); // affiche 4 + 7i
    return 0;
}
```

{{< boite type="exemple" titre="Résultat attendu :" >}}
La notation `c1 + c2` appelle ici `c1.operator+(c2)`. L'opération crée un nouvel objet `Complexe` sans modifier les deux objets initiaux.
{{< /boite >}}

Les opérateurs de comparaison se surchargent de la même manière et renvoient un `bool`. L'opérateur `==` compare les valeurs des attributs : deux objets distincts peuvent être égaux. L'opérateur `<` définit un ordre entre les objets ; c'est lui que `std::sort` utilise pour trier les objets d'une classe (annexe du module 4).

```cpp {linenos=table}
class Date {
private:
    int annee;
    int mois;
    int jour;

public:
    Date(int a, int m, int j) : annee(a), mois(m), jour(j) {}

    bool operator==(const Date& autre) const {
        return annee == autre.annee && mois == autre.mois && jour == autre.jour;
    }

    bool operator<(const Date& autre) const {
        if (annee != autre.annee) {
            return annee < autre.annee;
        }
        if (mois != autre.mois) {
            return mois < autre.mois;
        }
        return jour < autre.jour;
    }
};
```

Avec ces deux opérateurs, on peut écrire `if (echeance == aujourdhui)` ou trier un `std::vector<Date>` avec `std::sort`.

### 5.2. Limitations {#limitations}

Tous les opérateurs ne peuvent pas être surchargés. Il est notamment impossible de changer la priorité, l'associativité ou le nombre d'opérandes d'un opérateur. La surcharge doit rester cohérente avec le sens habituel de l'opérateur.

{{< boite type="attention" >}}
Évitez de donner à un opérateur un sens surprenant. Par exemple, `+` devrait généralement représenter une addition ou une combinaison naturelle, pas une suppression ou une comparaison.
{{< /boite >}}

### 5.3. Opérateurs d'insertion et d'extraction {#operateurs-d-insertion-et-d-extraction}

Les opérateurs `<<` et `>>` peuvent être surchargés pour afficher ou lire des objets. L'exemple ci-dessous montre seulement l'affichage avec `<<` ; la lecture avec `>>` suit le même principe général, mais nécessite aussi de valider les données saisies.

```cpp {linenos=table}
#include <iostream>

class Point {
private:
    double x{}, y{};

public:
    Point(double abs = 0, double ord = 0) : x(abs), y(ord) {}

    friend std::ostream& operator<<(std::ostream& os, const Point& p) {
        os << "(" << p.x << ", " << p.y << ")";
        return os;
    }
};

int main() {
    Point p(2.5, 4.0);
    std::cout << p << std::endl;
    return 0;
}
```

L'opérateur `<<` ne peut pas être une méthode de `Point` : dans `std::cout << p`, l'opérande de gauche est le flot, et non l'objet. On le définit donc comme une fonction non membre, qui reçoit le flot et l'objet ; elle est déclarée amie (`friend`, section suivante) pour accéder aux attributs privés. Elle renvoie le flot par référence, ce qui permet d'enchaîner les écritures, comme dans `std::cout << p << std::endl;`.

## 6. Fonctions et classes amies {#fonctions-et-classes-amies}

Une fonction amie est une fonction qui n'est pas membre d'une classe, mais qui est autorisée à accéder à ses membres privés ou protégés. Une classe amie fonctionne de manière similaire : tous ses membres peuvent accéder aux membres privés ou protégés de la classe qui lui accorde cette autorisation. L'amitié n'est ni réciproque ni transitive : elle doit être déclarée explicitement.

{{< figure-cours src="figures/fig07_friend_this.png" numero="7" legende="Fonction amie et pointeur `this`." alt="Fonction amie et pointeur this." largeur="88%" >}}

### 6.1. Les fonctions amies {#les-fonctions-amies}

```cpp {linenos=table}
#include <iostream>

class Compte {
private:
    double solde;

public:
    Compte(double s) : solde(s) {}

    friend void afficherSolde(const Compte& c);
};

void afficherSolde(const Compte& c) {
    std::cout << "Solde : " << c.solde << std::endl;
}

int main() {
    Compte compte(100.0);
    afficherSolde(compte);
    return 0;
}
```

{{< boite type="remarque" titre="Remarque" >}}
L'amitié doit être utilisée avec prudence. Elle peut être utile pour certains opérateurs, mais elle affaiblit l'encapsulation si elle est utilisée trop largement.
{{< /boite >}}

### 6.2. Les classes amies {#les-classes-amies}

```cpp {linenos=table}
class Mesure {
private:
    double valeur = 12.5;
    friend class Rapport;
};

class Rapport {
public:
    void afficher(const Mesure& mesure) const {
        std::cout << "Mesure : " << mesure.valeur << '\n';
    }
};
```

### 6.3. L'utilisation du pointeur `this` {#l-utilisation-du-pointeur-this}

Dans une méthode non statique, le pointeur `this` désigne l'objet sur lequel la méthode est appelée. L'expression `*this` représente cet objet lui-même. Ce mécanisme est notamment utile pour lever une ambiguïté entre un attribut et un paramètre, ou pour retourner une référence à l'objet et enchaîner des appels de méthodes.

```cpp {linenos=table}
class Compteur {
private:
    int valeur = 0;

public:
    Compteur& incrementer() {
        ++valeur;
        return *this;
    }

    int getValeur() const {
        return valeur;
    }
};

int main() {
    Compteur compteur;
    compteur.incrementer().incrementer();
    return compteur.getValeur() == 2 ? 0 : 1;
}
```

## 7. Lecture et écriture de fichiers {#lecture-et-ecriture-de-fichiers}

{{< boite type="remarque" titre="Remarque" >}}
Les entrées-sorties au terminal ont déjà été étudiées au module 2. Nous nous concentrons ici sur la création et la lecture de fichiers. Les options avancées de formatage ne sont pas nécessaires pour cet exemple.
{{< /boite >}}

Comme nous l'avons vu au module 2, les entrées-sorties en C++ reposent sur la notion de flot. Les principaux flots standard sont `cin`, `cout`, `cerr` et `clog`. Les fichiers sont manipulés avec les classes `ifstream`, `ofstream` et `fstream`.

{{< figure-cours src="figures/fig08_flots_fichiers.png" numero="8" legende="Vue d'ensemble des flots et fichiers en C++." largeur="92%" >}}

### 7.1. Quelques classes de flots {#quelques-classes-de-flots}

{{< tableau >}}
| Flot / classe | Rôle | Exemple |
|---|---|---|
| `cin` | Lecture depuis l'entrée standard. | clavier |
| `cout` | Écriture vers la sortie standard. | écran |
| `cerr` | Messages d'erreur non tamponnés. | erreurs immédiates |
| `clog` | Messages de journalisation tamponnés. | diagnostic |
| `ifstream` | Lecture depuis un fichier. | ouvrir un fichier texte |
| `ofstream` | Écriture dans un fichier. | créer un fichier de sortie |
{{< /tableau >}}

### 7.2. Lecture et écriture de fichiers {#lecture-et-ecriture-de-fichiers-2}

```cpp {linenos=table}
#include <fstream>
#include <iostream>
#include <string>

int main() {
    std::ofstream sortie("notes.txt");
    if (!sortie) {
        std::cerr << "Impossible de creer notes.txt" << std::endl;
        return 1;
    }
    sortie << "INF2005 90" << std::endl;
    sortie.close();

    std::ifstream entree("notes.txt");
    if (!entree) {
        std::cerr << "Impossible d'ouvrir notes.txt" << std::endl;
        return 1;
    }
    std::string cours;
    int note;

    if (entree >> cours >> note) {
        std::cout << cours << " : " << note << std::endl;
    } else {
        std::cerr << "Erreur de lecture du fichier" << std::endl;
    }
    return 0;
}
```

{{< boite type="important" >}}
Toujours vérifier qu'un fichier est bien ouvert ou qu'une lecture a réussi avant d'utiliser les données lues. Le fichier `notes.txt` est créé dans le répertoire de travail du programme : son emplacement peut donc varier selon la configuration de VS Code ou de Google Colab. L'exemple utilise un fichier fictif et peut écraser un fichier existant du même nom.
{{< /boite >}}

{{< boite type="exemple" titre="À essayer :" >}}
Changez la note écrite dans le fichier, exécutez de nouveau le programme et vérifiez la valeur lue. Vous pouvez également renommer le fichier pour observer la nécessité d'utiliser le même chemin en écriture et en lecture.
{{< /boite >}}

## 8. Structures de données : listes, piles et arbres (aperçu) {#structures-de-donnees-listes-piles-et-arbres-apercu}

{{< boite type="remarque" titre="Remarque" >}}
Cette section fournit une vue conceptuelle. Ces notions complètent les objectifs principaux sur l'héritage et le polymorphisme. Elles sont présentées pour reconnaître les structures ; leur implémentation complète relève d'un approfondissement.
{{< /boite >}}

Les structures de données permettent d'organiser l'information pour faciliter son accès, sa recherche, sa modification ou sa suppression. Le module présente notamment les listes, les piles et les arbres.

### 8.1. Les listes {#les-listes}

Une liste chaînée est composée de nœuds. Chaque nœud contient une donnée et un lien vers le nœud suivant. Le fragment suivant sert uniquement à illustrer la structure : il n'est pas un programme autonome.

{{< figure-cours src="figures/fig09_liste_chainee.png" numero="9" legende="Principe d'une liste chaînée simple." largeur="92%" >}}

```cpp {linenos=table}
#include <iostream>

struct Noeud {
    int valeur;
    Noeud* suivant;
};

void afficher(Noeud* tete) {
    for (Noeud* courant = tete; courant != nullptr; courant = courant->suivant) {
        std::cout << courant->valeur << " ";
    }
    std::cout << std::endl;
}
```

### 8.2. Les piles {#les-piles}

Une pile suit le principe LIFO : le dernier élément ajouté est le premier retiré.

{{< figure-cours src="figures/fig10_pile.png" numero="10" legende="Structure de pile : dernier entré, premier sorti." largeur="45%" >}}

```cpp {linenos=table}
#include <iostream>
#include <stack>

int main() {
    std::stack<int> pile;
    pile.push(-1);
    pile.push(-2);
    pile.push(-3);

    while (!pile.empty()) {
        std::cout << pile.top() << std::endl;
        pile.pop();
    }
    return 0;
}
```

### 8.3. Les arbres {#les-arbres}

Un arbre binaire de recherche organise les valeurs de façon à faciliter certaines recherches : en général, les valeurs inférieures sont placées à gauche et les valeurs supérieures à droite (sous réserve d'une convention pour les doublons). La recherche peut être rapide dans un arbre équilibré, mais elle peut devenir linéaire dans un arbre très déséquilibré.

{{< figure-cours src="figures/fig11_arbre_binaire.png" numero="11" legende="Exemple d'arbre binaire de recherche." largeur="85%" >}}

```cpp {linenos=table}
// Representation conceptuelle d'un noeud d'arbre binaire.
// Les liens doivent etre geres correctement dans un vrai programme.
struct Noeud {
    int valeur;
    Noeud* gauche = nullptr;
    Noeud* droite = nullptr;
};
```

{{< boite type="attention" >}}
L'extrait qui représente un nœud illustre uniquement les liens gauche et droit. Un programme complet doit également définir la création et la destruction des nœuds ; on privilégiera alors des techniques sûres de gestion de la mémoire, comme les pointeurs intelligents. Il n'est pas nécessaire de programmer un arbre complet dans ce module.
{{< /boite >}}

## 9. Bibliothèque standard et STL (aperçu) {#bibliotheque-standard-et-stl-apercu}

{{< boite type="remarque" titre="Remarque" >}}
La STL est introduite ici comme outil standard à connaître. Les conteneurs, les adaptateurs et les itérateurs sont détaillés dans le document d'annexes.
{{< /boite >}}

La STL (*Standard Template Library*) désigne historiquement un ensemble générique de conteneurs, d'itérateurs et d'algorithmes, aujourd'hui intégré à la bibliothèque standard C++. Des composants courants de cette bibliothèque, tels que `std::vector` et `std::unique_ptr`, ont déjà été rencontrés dans l'exemple de polymorphisme.

{{< figure-cours src="figures/fig12_stl_vue_ensemble.png" numero="12" legende="Vue d'ensemble des composants de la STL." largeur="92%" >}}

### 9.1. Les conteneurs {#les-conteneurs}

Les conteneurs permettent de stocker des objets. Les plus courants comprennent `vector`, `list`, `deque`, `set` et `map`. Les types `stack`, `queue` et `priority_queue` sont plus précisément des **adaptateurs de conteneur** : ils fournissent une interface particulière à partir d'un conteneur sous-jacent.

{{< tableau >}}
| Conteneur | Utilisation typique | En-tête |
|---|---|---|
| `vector` | Tableau dynamique avec accès rapide par indice. | `<vector>` |
| `list` | Liste doublement chaînée. | `<list>` |
| `map` | Association clé-valeur triée par clé. | `<map>` |
| `set` | Ensemble de valeurs uniques triées. | `<set>` |
| `stack` | Adaptateur de pile. | `<stack>` |
| `queue` | Adaptateur de file. | `<queue>` |
| `priority_queue` | File où l'élément prioritaire sort en premier. | `<queue>` |
{{< /tableau >}}

{{< boite type="exemple" >}}
Pour conserver une suite de valeurs sans fixer sa taille lors de la compilation, on peut utiliser `std::vector<int>`. La méthode `push_back()` ajoute un élément : `std::vector<int> notes = {70, 80};` puis `notes.push_back(90);`. Un tel conteneur simplifie plusieurs situations où l'on aurait autrement utilisé un tableau de taille fixe.
{{< /boite >}}

### 9.2. Les itérateurs {#les-iterateurs}

Un itérateur est un objet qui permet de parcourir un conteneur. Il joue un rôle de lien entre les conteneurs et les algorithmes.

```cpp {linenos=table}
#include <iostream>
#include <list>

int main() {
    std::list<int> entiers = {10, 20, 30};

    for (std::list<int>::iterator it = entiers.begin(); it != entiers.end(); ++it) {
        std::cout << *it << std::endl;
    }

    // Version moderne plus simple
    for (int valeur : entiers) {
        std::cout << valeur << std::endl;
    }
    return 0;
}
```

{{< boite type="remarque" titre="Remarque" >}}
Lorsque le type de l'itérateur est long, on peut utiliser `auto`. Par exemple : `for (auto it = v.begin(); it != v.end(); ++it)`. Quand on veut simplement lire toutes les valeurs, la boucle `for` basée sur l'intervalle est souvent plus claire.
{{< /boite >}}

## Synthèse finale du module {#synthese-finale-du-module}

{{< tableau >}}
| Notion | Ce qu'il faut retenir |
|---|---|
| Héritage | Permet de créer une classe dérivée à partir d'une classe de base afin de réutiliser et spécialiser le code. |
| Constructeurs et destructeurs | Les constructeurs sont appelés de la base vers la dérivée ; les destructeurs sont appelés dans l'ordre inverse. |
| Fonctions virtuelles | Permettent la liaison dynamique et l'appel de la bonne méthode selon le type réel de l'objet. |
| Polymorphisme | Permet de manipuler plusieurs objets dérivés à travers une interface commune. |
| Héritage multiple | Permet d'hériter de plusieurs classes, mais demande une conception prudente pour éviter les ambiguïtés. |
| Surcharge d'opérateurs | Permet de donner un comportement naturel à certains opérateurs pour des objets définis par le programmeur. |
| Fonctions et classes amies | Autorisent un accès contrôlé aux membres privés ou protégés d'une classe. |
| Flots, fichiers et STL | Fournissent des outils standards pour manipuler les entrées-sorties, les fichiers et les structures de données. |
{{< /tableau >}}

{{< boite type="synthese" >}}
Le module 4 a présenté les mécanismes avancés de la programmation orientée objet en C++ : héritage, classes dérivées, fonctions virtuelles, polymorphisme, héritage simple et multiple, surcharge d'opérateurs, fonctions amies, classes amies et pointeur `this`. Il a aussi introduit des notions complémentaires importantes comme les flots, les fichiers, les piles, les arbres et la bibliothèque STL. Ces notions permettent d'écrire des programmes C++ plus structurés, plus réutilisables et plus adaptés à des projets orientés objet de taille plus importante.
{{< /boite >}}

## Exercices de consolidation {#exercices-de-consolidation}

1. Créer une classe `Personne`, puis deux classes dérivées `Etudiant` et `Employe`. Ajouter une méthode `afficher()` dans chaque classe.
2. Transformer la méthode `afficher()` en méthode virtuelle et tester le polymorphisme d'abord avec une référence de type `Personne&`, puis, en approfondissement, avec un conteneur de pointeurs vers `Personne`.
3. Créer une classe abstraite `Forme` avec une fonction virtuelle pure `aire()`. Implémenter deux classes dérivées : `Rectangle` et `Cercle`.
4. Écrire une classe `Complexe` et surcharger les opérateurs `+` et `<<`.
5. Écrire un programme qui lit des valeurs depuis un fichier texte, les stocke dans un `vector<int>`, puis affiche la somme et la moyenne.
6. Utiliser `stack<int>` pour inverser l'ordre d'une suite de nombres (approfondissement).

{{< boite type="important" >}}
**Autoévaluation :** pour les exercices 1 à 4, vérifiez que vous pouvez expliquer le rôle des membres privés, les arguments du constructeur, le rôle de `virtual`/`override` et la différence entre appel de méthode et création d'objet. Les exercices sur les fichiers et les conteneurs prolongent les apprentissages et peuvent être réalisés après les exercices sur les classes.
{{< /boite >}}
