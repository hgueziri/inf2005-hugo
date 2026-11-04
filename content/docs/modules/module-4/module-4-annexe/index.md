---
title: "Annexes du module 4 : compléments techniques, codes détaillés et approfondissements"
linkTitle: "Annexes du module 4"
description: "INF 2005 – Programmation orientée objet avec C++"
weight: 45
---

{{< figure-cours src="figures/banner_4.png" alt="Bannière du cours INF 2005 – Programmation orientée objet avec C++" largeur="100%" >}}

# Annexes du module 4 : compléments techniques, codes détaillés et approfondissements

{{< boite type="objectif" >}}
Ces annexes complètent le module principal. Elles regroupent des exemples longs et des approfondissements, sans remplacer les notions fondamentales déjà étudiées.

Pour la partie consacrée à la bibliothèque standard, l'objectif est de pouvoir :

- choisir un conteneur adapté à un problème simple (`vector`, `map`, `stack`) ;
- ajouter, consulter et parcourir ses éléments ;
- expliquer le rôle d'un itérateur et l'intervalle `begin(), end()` ;
- utiliser les algorithmes `sort`, `find`, `count_if` et `accumulate` ;
- identifier quelques erreurs fréquentes liées aux indices, aux itérateurs et aux fichiers.

{{< /boite >}}

{{< boite type="contenu" >}}
**Contenu de l'annexe :** proposer des applications et compléments ciblés, sans répéter les exemples déjà étudiés dans le module principal.
{{< /boite >}}

## Table des matières {#table-des-matieres}

- [Comment utiliser cette annexe](#comment-utiliser-cette-annexe)
- [1 Héritage virtuel : une seule base dans un losange](#heritage-virtuel-une-seule-base-dans-un-losange)
- [2 Surcharge d'opérateurs : compléments](#surcharge-d-operateurs-complements)
  - [2.1 Classe `Complexe` avec `operator+`, `operator<<` et `operator>>`](#classe-complexe-avec-operator-operator-et-operator)
- [3 Fichiers texte : lecture fiable et formatage](#fichiers-texte-lecture-fiable-et-formatage)
  - [3.1 Écriture et lecture d'un fichier texte](#ecriture-et-lecture-d-un-fichier-texte)
  - [3.2 Formatage de la sortie](#formatage-de-la-sortie)
- [4 Arbre binaire de recherche : implémentation guidée (approfondissement)](#arbre-binaire-de-recherche-implementation-guidee-approfondissement)
- [5 STL : manipuler des données et choisir un conteneur](#stl-manipuler-des-donnees-et-choisir-un-conteneur)
  - [5.1 Manipuler `std::vector` au-delà du premier exemple](#manipuler-std-vector-au-dela-du-premier-exemple)
  - [5.2 Choisir un conteneur adapté au problème](#choisir-un-conteneur-adapte-au-probleme)
  - [5.3 Comprendre les itérateurs](#comprendre-les-iterateurs)
  - [5.4 Associer des clés à des valeurs avec `std::map`](#associer-des-cles-a-des-valeurs-avec-std-map)
  - [5.5 Autoévaluation : choisir un conteneur](#autoevaluation-choisir-un-conteneur)
- [6 STL : algorithmes génériques et parcours](#stl-algorithmes-generiques-et-parcours)
  - [6.1 Trier, rechercher et calculer une moyenne](#trier-rechercher-et-calculer-une-moyenne)
  - [6.2 Exercice guidé : manipuler les notes](#exercice-guide-manipuler-les-notes)
- [7 Projet multifichier : séparer déclarations et définitions](#projet-multifichier-separer-declarations-et-definitions)
  - [7.1 Exemple : `Article.h`](#exemple-article-h)
  - [7.2 Exemple : `Article.cpp`](#exemple-article-cpp)
  - [7.3 Exemple : `Boisson.h`](#exemple-boisson-h)
  - [7.4 Exemple : `Boisson.cpp`](#exemple-boisson-cpp)
  - [7.5 Exemple : `main.cpp`](#exemple-main-cpp)
  - [7.6 Exemple : compilation dans VS Code ou terminal](#exemple-compilation-dans-vs-code-ou-terminal)
- [8 Erreurs caractéristiques des approfondissements](#erreurs-caracteristiques-des-approfondissements)
- [9 Exercices de consolidation propres à l'annexe](#exercices-de-consolidation-propres-a-l-annexe)

{{< boite type="remarque" titre="Remarque" >}}
**Parcours conseillé.** Lisez d'abord les annexes relatives aux notions que vous souhaitez approfondir. Pour découvrir la STL, commencez par la section « STL : conteneurs et itérateurs », puis poursuivez avec « STL : algorithmes utiles ». Les listes chaînées et les arbres écrits manuellement illustrent les mécanismes internes de certaines structures ; leur implémentation n'est pas un préalable à l'utilisation de `std::vector` ou de `std::map`.

Dans cet document, « STL » désigne les conteneurs, itérateurs et algorithmes traditionnellement associés à la *Standard Template Library*, aujourd'hui intégrés à la bibliothèque standard C++.
{{< /boite >}}

{{< boite type="remarque" titre="Remarque" >}}
Les étapes de création, de compilation et d'exécution dans VS Code ou Google Colab sont décrites au module 2. Tous les programmes présentés ici ciblent C++17. Les extraits avec plusieurs fichiers doivent être enregistrés sous les noms indiqués avant la compilation.
{{< /boite >}}

## Comment utiliser cette annexe {#comment-utiliser-cette-annexe}

Le **module 4 principal** introduit l'héritage simple, la redéfinition des méthodes, le polymorphisme, la surcharge d'opérateurs et une première utilisation des conteneurs. Pour éviter de réexpliquer ces notions, nous nous concentrons ici sur des cas où il faut aller plus loin : résoudre un héritage en losange, construire une interface de lecture/écriture pour une classe, fiabiliser les fichiers, implémenter un arbre et utiliser les algorithmes de la STL.

La partie **STL** est recommandée pour les exercices pratiques. L'héritage virtuel et l'implémentation d'un arbre sont des **approfondissements facultatifs**. Le projet multifichier est particulièrement utile avant d'aborder des applications plus importantes.

## Annexe 1. Héritage virtuel : une seule base dans un losange {#heritage-virtuel-une-seule-base-dans-un-losange}

Le module principal a présenté le risque d'un *losange* dans une hiérarchie d'héritage. Nous allons maintenant examiner sa solution technique : `virtual public` permet de partager un même sous-objet de base entre deux branches. Cet exemple illustre un mécanisme avancé ; l'héritage d'interfaces ou la composition restent souvent plus simples.

{{< figure-cours src="figures/fig05_heritage_losange.png" numero="1" legende="Situation générale d'un héritage en losange." largeur="70%" >}}

```cpp {linenos=table}
#include <iostream>

class Identifiable {
protected:
    int id{};
public:
    explicit Identifiable(int i = 0) : id(i) {}
};

class Document : virtual public Identifiable {
public:
    Document() : Identifiable(1) {}
};

class Ressource : virtual public Identifiable {
public:
    Ressource() : Identifiable(2) {}
};

class FichierNumerique : public Document, public Ressource {
public:
    FichierNumerique() : Identifiable(99), Document(), Ressource() {}
    void afficher() const { std::cout << "id = " << id << std::endl; }
};

int main() {
    FichierNumerique f;
    f.afficher();
    return 0;
}
```

{{< boite type="remarque" titre="Remarque" >}}
L'héritage virtuel règle certains cas d'ambiguïté, mais il complexifie la conception. Dans un cours d'introduction à la POO avec C++, il est suffisant de comprendre le risque et de privilégier les interfaces abstraites ou la composition lorsque c'est plus simple.
{{< /boite >}}

{{< boite type="exemple" titre="Résultat attendu :" >}}
`id = 99`. Les deux branches `Document` et `Ressource` partagent le même sous-objet `Identifiable`. Il est initialisé par le constructeur de `FichierNumerique`, la classe la plus dérivée. Les initialisations de `Identifiable` écrites dans les constructeurs des deux branches sont alors ignorées pour cet objet final.
{{< /boite >}}

{{< boite type="important" >}}
L'héritage virtuel ne rend pas toutes les méthodes automatiquement virtuelles : le mot `virtual` appliqué à une **base** et celui appliqué à une **méthode** ont ici deux rôles différents.
{{< /boite >}}

## Annexe 2. Surcharge d'opérateurs : compléments {#surcharge-d-operateurs-complements}

Le module principal a présenté l'opérateur `+` sur une classe `Complexe`. Cette version ajoute `+=`, l'affichage avec `<<` et la lecture avec `>>`. Le but est de comprendre les valeurs de retour, les fonctions amies et le comportement en cas de saisie invalide.

{{< figure-cours src="figures/fig06_surcharge_operateur.png" numero="2" legende="Surcharge de l'opérateur `+` pour additionner deux objets." alt="Surcharge de l'opérateur + pour additionner deux objets." largeur="70%" >}}

### 2.1. Classe `Complexe` avec `operator+`, `operator<<` et `operator>>` {#classe-complexe-avec-operator-operator-et-operator}

```cpp {linenos=table}
#include <iostream>

class Complexe {
private:
    double reel{};
    double imaginaire{};

public:
    Complexe(double r = 0.0, double i = 0.0)
        : reel(r), imaginaire(i) {}

    Complexe operator+(const Complexe& autre) const {
        return Complexe(reel + autre.reel, imaginaire + autre.imaginaire);
    }

    Complexe& operator+=(const Complexe& autre) {
        reel += autre.reel;
        imaginaire += autre.imaginaire;
        return *this;
    }

    friend std::ostream& operator<<(std::ostream& os, const Complexe& c) {
        os << c.reel;
        if (c.imaginaire < 0) {
            os << " - " << -c.imaginaire << "i";
        } else {
            os << " + " << c.imaginaire << "i";
        }
        return os;
    }

    friend std::istream& operator>>(std::istream& is, Complexe& c) {
        double r, i;
        if (is >> r >> i) {
            c.reel = r;
            c.imaginaire = i;
        }
        return is;
    }
};

int main() {
    Complexe a(1.5, 2.0);
    Complexe b(3.0, 4.5);
    Complexe c = a + b;
    std::cout << "a + b = " << c << std::endl;

    c += Complexe(1, 1);
    std::cout << "apres += : " << c << std::endl;

    // Le format de lecture est : partie_reelle partie_imaginaire.
    // Ex. : -2 3 (deux nombres separes par un espace).
    std::cout << "Saisir un complexe (reel imaginaire) : ";
    Complexe lu;
    if (std::cin >> lu) {
        std::cout << "Vous avez saisi : " << lu << '\n';
    } else {
        std::cerr << "Saisie invalide.\n";
    }
    return 0;
}
```

{{< boite type="attention" >}}
Les opérateurs `.`, `.*`, `::`, `?:` et `sizeof` ne peuvent pas être surchargés. La surcharge ne change pas non plus la priorité ni l'associativité de l'opérateur.
{{< /boite >}}

{{< boite type="remarque" titre="Remarque" >}}
Contrairement à l'affichage `2 + 3i`, l'opérateur d'extraction de cet exemple attend **deux nombres séparés par un espace**, par exemple `2 3`. L'usage de variables temporaires empêche de modifier partiellement l'objet si une des lectures échoue. La fonction renvoie le flot afin que l'on puisse écrire `if (std::cin >> c)` ou chaîner plusieurs lectures.
{{< /boite >}}

## Annexe 3. Fichiers texte : lecture fiable et formatage {#fichiers-texte-lecture-fiable-et-formatage}

{{< figure-cours src="figures/fig08_flots_fichiers.png" numero="3" legende="Lecture, écriture et fichiers avec les flots C++." largeur="88%" >}}

### 3.1. Écriture et lecture d'un fichier texte {#ecriture-et-lecture-d-un-fichier-texte}

Contrairement au court exemple du module principal, ce programme traite plusieurs enregistrements et distingue une fin de fichier normale d'une erreur de format. Il crée d'abord un fichier `etudiants.txt`, puis le rouvre pour lire les noms et les notes. Les fichiers sont créés dans le **répertoire de travail** du programme : ce n'est pas nécessairement le dossier visible dans l'éditeur. Les opérateurs `<<` et `>>` fonctionnent ici sur des flots de fichiers, comme ils fonctionnent avec `std::cout` et `std::cin`.

```cpp {linenos=table}
#include <fstream>
#include <iostream>
#include <string>

int main() {
    {
        std::ofstream sortie("etudiants.txt");
        if (!sortie) {
            std::cerr << "Impossible de creer le fichier." << std::endl;
            return 1;
        }
        sortie << "Amina 87\n";
        sortie << "Karim 74\n";
        sortie << "Lea 92\n";
        sortie.flush();
        if (!sortie) {
            std::cerr << "Erreur pendant l'ecriture du fichier." << std::endl;
            return 1;
        }
    }

    std::ifstream entree("etudiants.txt");
    if (!entree) {
        std::cerr << "Impossible d'ouvrir le fichier." << std::endl;
        return 1;
    }

    std::string nom;
    int note;
    while (entree >> nom >> note) {
        std::cout << nom << " : " << note << std::endl;
    }

    if (!entree.eof()) {
        std::cerr << "Erreur de format dans le fichier." << std::endl;
        return 1;
    }
    return 0;
}
```

{{< boite type="important" >}}
Vérifier l'ouverture d'un fichier n'est pas suffisant : il faut aussi contrôler les erreurs de lecture et, pour les données importantes, les erreurs d'écriture. La condition `while (entree >> nom >> note)` cesse notamment lorsque l'on arrive à la fin du fichier ou lorsque la lecture échoue. Le test qui suit distingue la fin normale d'un problème de format.
{{< /boite >}}

### 3.2. Formatage de la sortie {#formatage-de-la-sortie}

```cpp {linenos=table}
#include <iomanip>
#include <iostream>

int main() {
    double prix = 12.5;
    double taxe = 1.14975;

    std::cout << std::fixed << std::setprecision(2);
    std::cout << "Prix avec taxe : " << prix * taxe << " $" << std::endl;

    std::cout << std::setw(12) << std::left << "Article" << std::setw(8) << std::right << "Prix" << std::endl;
    std::cout << std::setw(12) << std::left << "Livre"   << std::setw(8) << std::right << prix << std::endl;
    return 0;
}
```

{{< boite type="exemple" titre="Sortie attendue :" >}}
Les lignes `Amina : 87`, `Karim : 74` et `Lea : 92`. Pour tester la gestion des erreurs, modifiez volontairement une ligne du fichier en remplaçant une note numérique par un texte, puis relancez uniquement la partie lecture dans un programme séparé : l'exécution doit signaler un format invalide.
{{< /boite >}}

{{< boite type="important" >}}
Les manipulateurs n'ont pas tous la même durée d'effet. `std::setw()` ne s'applique qu'à la prochaine valeur écrite : il faut le répéter devant chaque colonne, comme dans l'exemple. `std::fixed`, `std::setprecision()`, `std::left` et `std::right` restent au contraire en vigueur pour toutes les écritures suivantes du flot. Enfin, sans `std::fixed`, `std::setprecision(2)` fixe le nombre de chiffres significatifs, et non le nombre de décimales.
{{< /boite >}}

## Annexe 4. Arbre binaire de recherche : implémentation guidée (approfondissement) {#arbre-binaire-de-recherche-implementation-guidee-approfondissement}

Le module principal présente la structure d'un arbre binaire et ses liens gauche/droit. Nous construisons ici un **arbre binaire de recherche**, dans lequel les valeurs plus petites vont à gauche et les plus grandes à droite. La recherche, l'insertion et le parcours infixe sont montrés ensemble.

Cet exemple utilise `std::unique_ptr` pour que les nœuds soient libérés automatiquement à la fin du programme, sans appeler `delete`. Il suppose que les valeurs sont distinctes : les doublons sont ignorés.

{{< figure-cours src="figures/fig11_arbre_binaire.png" numero="4" legende="Structure d'un arbre binaire de recherche ; le parcours infixe visite gauche, nœud, puis droite." largeur="78%" >}}

```cpp {linenos=table}
#include <iostream>
#include <memory>

struct Noeud {
    int valeur;
    std::unique_ptr<Noeud> gauche;
    std::unique_ptr<Noeud> droite;

    explicit Noeud(int valeur) : valeur(valeur) {}
};

void inserer(std::unique_ptr<Noeud>& racine, int valeur) {
    if (!racine) {
        racine = std::make_unique<Noeud>(valeur);
    } else if (valeur < racine->valeur) {
        inserer(racine->gauche, valeur);
    } else if (valeur > racine->valeur) {
        inserer(racine->droite, valeur);
    }
}

bool contient(const Noeud* racine, int valeur) {
    if (!racine) return false;
    if (racine->valeur == valeur) return true;
    if (valeur < racine->valeur)
        return contient(racine->gauche.get(), valeur);
    return contient(racine->droite.get(), valeur);
}

void afficherCroissant(const Noeud* racine) {
    if (!racine) return;
    afficherCroissant(racine->gauche.get());
    std::cout << racine->valeur << ' ';
    afficherCroissant(racine->droite.get());
}

int main() {
    std::unique_ptr<Noeud> racine;
    for (int n : {8, 3, 10, 1, 6}) inserer(racine, n);
    afficherCroissant(racine.get());
    std::cout << "\n6 present : " << contient(racine.get(), 6) << '\n';
    return 0;
}
```

{{< boite type="exemple" titre="Résultat attendu :" >}}
`1 3 6 8 10`, puis `6 present : 1` (la valeur `1` représente `true` lors de cet affichage). Le pointeur `racine` est propriétaire des autres nœuds par l'intermédiaire des liens `gauche` et `droite`.
{{< /boite >}}

{{< boite type="attention" >}}
Cette structure **n'est pas autoéquilibrée**. Si l'on insère des valeurs déjà triées, l'arbre peut devenir une chaîne et la recherche peut nécessiter de parcourir tous ses nœuds. Pour une collection triée dans une application réelle, des conteneurs comme `std::set` et `std::map` évitent d'écrire soi-même une structure arborescente.
{{< /boite >}}

Le parcours infixe utilisé par `afficherCroissant()` visite le sous-arbre gauche, puis le nœud, puis le sous-arbre droit : dans un arbre binaire de recherche, il donne les valeurs en ordre croissant. Deux autres ordres de parcours sont courants. Le parcours **préfixe** visite le nœud avant ses deux sous-arbres : il commence par la racine. Le parcours **postfixe** visite les deux sous-arbres avant le nœud : la racine vient en dernier. D'un parcours à l'autre, seule la position de l'affichage par rapport aux deux appels récursifs change.

## Annexe 5. STL : manipuler des données et choisir un conteneur {#stl-manipuler-des-donnees-et-choisir-un-conteneur}

Le module 4 donne une vue d'ensemble de la STL. Nous détaillons ici les opérations courantes d'un `vector`, puis les différences de choix entre conteneurs. Le même exemple de notes sert à introduire ensuite les itérateurs et les algorithmes génériques.

### 5.1. Manipuler `std::vector` au-delà du premier exemple {#manipuler-std-vector-au-dela-du-premier-exemple}

Un `vector<int>` contient une séquence d'entiers, rangés de manière contiguë en mémoire. À la différence d'un tableau C de taille fixe, il peut grandir au cours de l'exécution. Le tableau ci-dessous présente les opérations utilisées dans le premier exemple.

{{< tableau >}}
| Expression | Effet |
|---|---|
| `std::vector<int> notes = {70, 82};` | Créer un vecteur contenant deux entiers. |
| `notes.push_back(91);` | Ajouter 91 à la fin du vecteur. |
| `notes.size()` | Obtenir le nombre d'éléments. |
| `notes[0]` | Accéder au premier élément, sans vérification des bornes. |
| `notes.at(0)` | Accéder au premier élément avec vérification des bornes. |
| `notes.empty()` | Tester si le vecteur ne contient aucun élément. |
{{< /tableau >}}

**Programme complet :**

```cpp {linenos=table}
#include <iostream>
#include <vector>

int main() {
    std::vector<int> notes = {70, 82};
    notes.push_back(91);

    std::cout << "Nombre de notes : " << notes.size() << '\n';
    std::cout << "Premiere note : " << notes.at(0) << '\n';

    for (int note : notes) {
        std::cout << note << " ";
    }
    std::cout << '\n';
    return 0;
}
```

{{< boite type="exemple" titre="Résultat attendu :" >}}

```cpp
Nombre de notes : 3
Premiere note : 70
70 82 91
```

{{< /boite >}}

{{< boite type="important" >}}
Les indices commencent à 0. Pour un vecteur de trois éléments, les indices valides sont 0, 1 et 2. L'accès `notes[3]` est hors limites et provoque un comportement indéfini ; `notes.at(3)` détecte cette erreur en lançant une exception. Pour débuter, privilégiez `at()` quand la validité de l'indice n'est pas certaine.
{{< /boite >}}

Un `std::vector` est un objet : passé par valeur à une fonction, il est copié en entier, et la fonction ne modifie que sa copie. Un tableau C, au contraire, n'est pas copié, et la fonction modifie le tableau de l'appelant (module 3). Pour qu'une fonction modifie le vecteur de l'appelant, on le passe par référence (`std::vector<int>& notes`) ; pour le consulter sans le copier, par référence constante (`const std::vector<int>& notes`).

### 5.2. Choisir un conteneur adapté au problème {#choisir-un-conteneur-adapte-au-probleme}

Les conteneurs n'offrent pas tous les mêmes opérations ni les mêmes garanties. Pour les premiers exercices, `vector` convient à la plupart des collections ordonnées par position ; `map` convient aux associations clé–valeur ; `stack` convient à une pile d'actions.

{{< tableau >}}
| Type | Organisation | Exemple d'utilisation |
|---|---|---|
| `vector` | Séquence dynamique contiguë ; accès rapide par indice. | Liste de notes dont la taille change. |
| `array` | Séquence de taille fixe connue à la compilation. | Mesures prises par un ensemble fixe de capteurs. |
| `deque` | Séquence avec ajouts efficaces aux deux extrémités. | File d'événements avec ajout en tête et en queue. |
| `list` | Liste doublement chaînée ; pas d'accès direct par indice. | Insertions ou suppressions à partir d'itérateurs déjà disponibles. |
| `set` | Valeurs uniques, maintenues triées. | Ensemble des identifiants enregistrés. |
| `map` | Associations clé–valeur, triées selon la clé. | Note associée au nom d'un étudiant. |
| `unordered_map` | Associations clé–valeur organisées par hachage, sans ordre de parcours garanti. | Recherche par identifiant lorsque l'ordre importe peu. |
| `stack` | Adaptateur LIFO : dernier élément ajouté, premier retiré. | Historique d'annulation. |
| `queue` | Adaptateur FIFO : premier élément ajouté, premier retiré. | File de tâches à traiter. |
{{< /tableau >}}

{{< boite type="remarque" titre="Remarque" >}}
Le conteneur `std::list` n'est pas nécessairement plus rapide qu'un `vector` pour des ajouts fréquents : localiser l'emplacement d'insertion dans une liste peut coûter du temps. `stack` et `queue` sont des *adaptateurs* : ils ne proposent pas d'itérateurs pour parcourir tous leurs éléments. On privilégie donc un choix fondé sur les opérations nécessaires, plutôt que sur le seul nom du conteneur.
{{< /boite >}}

### 5.3. Comprendre les itérateurs {#comprendre-les-iterateurs}

Un **itérateur** permet de désigner un élément et de passer au suivant. Pour un `vector`, `begin()` désigne le premier élément et `end()` désigne la position **après le dernier élément**. L'intervalle noté `[begin(), end())` inclut le début, mais exclut la fin. Il ne faut jamais déréférencer `end()` avec `*`.

```cpp {linenos=table}
#include <iostream>
#include <vector>

int main() {
    std::vector<int> notes = {82, 91, 70};

    for (auto it = notes.begin(); it != notes.end(); ++it) {
        std::cout << *it << " ";
    }
    std::cout << '\n';

    // Écriture plus concise lorsque l'indice n'est pas utile.
    for (int note : notes) {
        std::cout << note << " ";
    }
    std::cout << '\n';
    return 0;
}
```

Dans cette boucle, `auto` laisse le compilateur déduire le type de l'itérateur ; `*it` accède à l'élément courant ; `++it` avance à l'élément suivant. La seconde boucle, dite *for fondée sur un intervalle*, est souvent plus lisible lorsque l'on souhaite simplement consulter les éléments.

{{< boite type="attention" >}}
**Validité des itérateurs.** Certaines modifications du conteneur peuvent invalider les itérateurs ou références obtenus auparavant. Par exemple, un `push_back()` dans un `vector` peut déclencher une réallocation et rendre ces itérateurs inutilisables. Évitez de conserver un itérateur pendant que vous modifiez un vecteur sans connaître les règles d'invalidation.
{{< /boite >}}

### 5.4. Associer des clés à des valeurs avec `std::map` {#associer-des-cles-a-des-valeurs-avec-std-map}

Un `map<string,int>` relie chaque nom d'étudiant à une note. Chaque **clé est unique** et le parcours d'un `std::map` se fait dans l'ordre des clés (ici, l'ordre lexicographique des chaînes). L'opérateur `notes["Amina"]` ajoute une entrée si la clé est absente ; pour seulement chercher une clé sans l'ajouter, utilisez `find()`.

```cpp {linenos=table}
#include <iostream>
#include <map>
#include <string>

int main() {
    std::map<std::string, int> notes;
    notes["Karim"] = 74;
    notes["Amina"] = 87;
    notes["Lea"] = 92;

    for (const auto& [nom, note] : notes) {
        std::cout << nom << " : " << note << '\n';
    }

    auto it = notes.find("Lea");
    if (it != notes.end()) {
        std::cout << "Note de Lea : " << it->second << '\n';
    }
    return 0;
}
```

{{< boite type="exemple" titre="Résultat attendu (ordre des clés) :" >}}

```cpp
Amina : 87
Karim : 74
Lea : 92
Note de Lea : 92
```

{{< /boite >}}

L'expression `it->second` accède à la valeur associée à la clé trouvée (la clé elle-même est `it->first`). La syntaxe `[nom, note]` est une **décomposition structurée**, disponible à partir de C++17. La recherche avec `notes.find()` est une méthode du conteneur, à distinguer de l'algorithme générique `std::find()` présenté dans la section suivante.

### 5.5. Autoévaluation : choisir un conteneur {#autoevaluation-choisir-un-conteneur}

1. Vous devez mémoriser une série de notes et les trier : quel conteneur choisiriez-vous en premier ?
2. Vous devez retrouver une note à partir du nom de l'étudiant, sans créer d'entrée si le nom n'existe pas : quelle opération utiliser ?
3. Pour un système « annuler la dernière action », quel conteneur ou adaptateur est approprié ?

{{< boite type="remarque" titre="Remarque" >}}
**Éléments de réponse :** (1) `vector` ; (2) `map::find()` ; (3) `stack`. L'objectif est d'associer le besoin à une propriété du conteneur, plutôt que de mémoriser tous les noms de la bibliothèque.
{{< /boite >}}

## Annexe 6. STL : algorithmes génériques et parcours {#stl-algorithmes-generiques-et-parcours}

Après avoir choisi un conteneur, on peut lui appliquer des algorithmes génériques plutôt que de programmer systématiquement une nouvelle boucle. Beaucoup d'algorithmes travaillent sur l'intervalle `[debut, fin)` décrit par deux itérateurs. Les fonctions `sort`, `find` et `count_if` sont déclarées dans `<algorithm>` ; `accumulate` se trouve dans `<numeric>`.

### 6.1. Trier, rechercher et calculer une moyenne {#trier-rechercher-et-calculer-une-moyenne}

Le programme suivant reprend le même vecteur de notes pour illustrer quatre algorithmes. Lisez chaque instruction, prédisez la sortie, puis compilez le programme.

```cpp {linenos=table}
#include <algorithm>
#include <iostream>
#include <iterator>
#include <numeric>
#include <vector>

int main() {
    std::vector<int> notes = {70, 82, 91, 65, 88, 95};

    std::sort(notes.begin(), notes.end());

    auto position = std::find(notes.begin(), notes.end(), 88);
    if (position != notes.end()) {
        std::cout << "88 a l'indice "
                  << std::distance(notes.begin(), position) << '\n';
    }

    int somme = std::accumulate(notes.begin(), notes.end(), 0);
    if (!notes.empty()) {
        std::cout << "Moyenne = "
                  << static_cast<double>(somme) / notes.size() << '\n';
    }

    int nbReussites = std::count_if(notes.begin(), notes.end(),
        [](int note) { return note >= 60; });
    std::cout << "Reussites = " << nbReussites << '\n';
    return 0;
}
```

{{< boite type="exemple" titre="Résultat attendu :" >}}

```text
88 a l'indice 3
Moyenne = 81.8333
Reussites = 6
```

{{< /boite >}}

{{< tableau >}}
| Algorithme | Ce qu'il fait ici |
|---|---|
| `sort` | Réorganise les éléments du vecteur en ordre croissant. |
| `find` | Renvoie un itérateur vers 88, ou `end()` si 88 n'est pas présent. |
| `accumulate` | Additionne les notes en partant de la valeur initiale 0. |
| `count_if` | Compte les notes qui satisfont le critère donné. |
{{< /tableau >}}

L'expression `[](int note) { return note >= 60; }` définit une **fonction lambda** : une petite fonction écrite sur place qui indique la condition à tester. Le `static_cast<double>` évite d'effectuer une division entière au moment de calculer la moyenne. Une vérification avec `empty()` évite de diviser par zéro.

{{< boite type="attention" >}}
`std::sort()` nécessite des itérateurs à accès aléatoire, fournis notamment par `vector` et `deque`. Il ne s'applique pas directement à un `std::list`, qui possède sa propre méthode `list.sort()`. Attention également : après le tri, les **positions des valeurs ont changé**. L'indice retourné par la recherche correspond au vecteur *trié*.
{{< /boite >}}

La valeur initiale de `std::accumulate` détermine le type du calcul : avec `0`, de type `int`, chaque somme partielle est convertie en entier, et les décimales des éléments d'un `std::vector<double>` sont perdues. Il faut alors écrire `0.0`. Par ailleurs, `std::sort` compare les éléments avec l'opérateur `<` : pour trier les objets d'une classe, celle-ci doit définir cet opérateur (module 4, section 5.1).

### 6.2. Exercice guidé : manipuler les notes {#exercice-guide-manipuler-les-notes}

À partir du programme précédent, réalisez successivement les modifications suivantes :

1. Ajoutez la note `50` au vecteur avec `push_back()`, puis prédisez la nouvelle moyenne.
2. Modifiez `count_if` pour compter les notes supérieures ou égales à `80`.
3. Remplacez la recherche de `88` par celle de `100`. Vérifiez que le programme n'affiche plus d'indice pour une valeur absente.

{{< boite type="remarque" titre="Remarque" >}}
**Pour vérifier :** après ajout de 50, la somme est 541 pour 7 notes et la moyenne vaut environ 77,29. Parmi les 7 valeurs, quatre notes sont supérieures ou égales à 80 (82, 88, 91 et 95). Une recherche infructueuse renvoie `end()` ; il ne faut donc pas déréférencer l'itérateur obtenu.
{{< /boite >}}

{{< boite type="important" >}}
La STL permet d'éviter de nombreux algorithmes écrits à la main. Par exemple, un exercice de tri à bulle reste utile pour comprendre les comparaisons et permutations, mais dans une application courante on utilise généralement `std::sort()` lorsque le type d'itérateurs le permet.
{{< /boite >}}

## Annexe 7. Projet multifichier : séparer déclarations et définitions {#projet-multifichier-separer-declarations-et-definitions}

Les classes `Article` et `Boisson` ont déjà été étudiées dans le module principal. L'objectif n'est donc pas de réexpliquer l'héritage, mais de montrer comment répartir une même application en **cinq fichiers** et compiler plusieurs unités de traduction. Les déclarations sont placées dans les en-têtes et les définitions des fonctions dans les fichiers `.cpp`.

{{< tableau >}}
| Fichier | Contenu | Rôle pédagogique |
|---|---|---|
| `Article.h` | Déclaration de la classe `Article`. | Comprendre l'interface d'une classe. |
| `Article.cpp` | Définition des méthodes de `Article`. | Séparer interface et implémentation. |
| `Boisson.h` | Déclaration de la classe dérivée `Boisson`. | Observer la syntaxe de l'héritage. |
| `main.cpp` | Programme principal. | Créer les objets et tester les méthodes. |
{{< /tableau >}}

{{< boite type="remarque" titre="Remarque" >}}
Un en-tête est inclus dans chaque fichier `.cpp` qui en a besoin. S'il contenait la définition d'une fonction non membre, ou celle d'une méthode écrite hors de sa classe, chacun de ces fichiers en recevrait une copie, et l'éditeur de liens signalerait une définition multiple. Les gardes d'inclusion (`#ifndef ARTICLE_H` ou `#pragma once`) évitent seulement qu'un même fichier `.cpp` inclue deux fois l'en-tête : elles ne remplacent pas la séparation entre déclarations et définitions.
{{< /boite >}}

### 7.1. Exemple : `Article.h` {#exemple-article-h}

```cpp {linenos=table}
#ifndef ARTICLE_H
#define ARTICLE_H

#include <string>

class Article {
protected:
    std::string nom;
    double prix;
    int quantite;
    double taxe;

public:
    Article(std::string nomArticle, double prixArticle,
            int quantiteArticle = 0, double tauxTaxe = 1.15);

    virtual ~Article() = default;
    virtual double prixAvecTaxe() const;
    virtual void afficher() const;
};

#endif
```

### 7.2. Exemple : `Article.cpp` {#exemple-article-cpp}

```cpp {linenos=table}
#include "Article.h"
#include <iostream>

Article::Article(std::string nomArticle, double prixArticle,
                 int quantiteArticle, double tauxTaxe)
    : nom(nomArticle), prix(prixArticle),
      quantite(quantiteArticle), taxe(tauxTaxe) {}

double Article::prixAvecTaxe() const {
    return prix * taxe * quantite;
}

void Article::afficher() const {
    std::cout << nom << " : " << prixAvecTaxe() << " $" << std::endl;
}
```

### 7.3. Exemple : `Boisson.h` {#exemple-boisson-h}

```cpp {linenos=table}
#ifndef BOISSON_H
#define BOISSON_H

#include "Article.h"

class Boisson : public Article {
private:
    int volumeMl;

public:
    Boisson(std::string nom, double prix, int volume,
            int quantite = 0);

    int getVolume() const;
    void afficher() const override;
};

#endif
```

### 7.4. Exemple : `Boisson.cpp` {#exemple-boisson-cpp}

```cpp {linenos=table}
#include "Boisson.h"
#include <iostream>

Boisson::Boisson(std::string nom, double prix, int volume, int quantite)
    : Article(nom, prix, quantite), volumeMl(volume) {}

int Boisson::getVolume() const {
    return volumeMl;
}

void Boisson::afficher() const {
    Article::afficher();
    std::cout << "Volume : " << volumeMl << " ml" << std::endl;
}
```

### 7.5. Exemple : `main.cpp` {#exemple-main-cpp}

Pour rendre cet exemple réellement reproductible, le projet doit aussi contenir le fichier principal suivant. Les quatre autres fichiers sont ceux présentés plus haut.

```cpp {linenos=table}
#include "Article.h"
#include "Boisson.h"
#include <iostream>

int main() {
    Article livre("Livre de C++", 20.0, 2);
    Boisson eau("Eau", 2.5, 500, 3);
    livre.afficher();
    eau.afficher();
    std::cout << "Test getVolume() : " << eau.getVolume() << " ml\n";
    return 0;
}
```

### 7.6. Exemple : compilation dans VS Code ou terminal {#exemple-compilation-dans-vs-code-ou-terminal}

Enregistrez `Article.h`, `Article.cpp`, `Boisson.h`, `Boisson.cpp` et `main.cpp` **dans le même dossier**. Ouvrez le terminal dans ce dossier, puis lancez :

```bash
g++ -std=c++17 -Wall -Wextra Article.cpp Boisson.cpp main.cpp -o programme
./programme
```

Sous Windows PowerShell, l'exécutable peut être lancé avec `.\programme.exe`. La compilation doit inclure les trois fichiers `.cpp` ; les fichiers `.h` sont inclus depuis ces sources et ne sont pas compilés séparément dans cette commande.

{{< boite type="exemple" titre="Résultat attendu :" >}}
Un livre et une boisson sont affichés avec leur prix calculé, puis la ligne `Test getVolume() : 500 ml`. Les coefficients de taxe sont **fictifs** et servent uniquement à illustrer l'héritage et la séparation du code.
{{< /boite >}}

{{< boite type="attention" >}}
Si la compilation oublie `Article.cpp` ou `Boisson.cpp`, le compilateur peut accepter les déclarations, mais l'éditeur de liens signalera ensuite une *référence indéfinie* (*undefined reference*) vers une fonction déclarée mais non fournie lors de l'édition des liens.
{{< /boite >}}

## Annexe 8. Erreurs caractéristiques des approfondissements {#erreurs-caracteristiques-des-approfondissements}

{{< tableau >}}
| Difficulté | Vérification ou correction |
|---|---|
| Confondre méthode virtuelle et base virtuelle. | Dans `virtual void f()`, le dispatch peut être dynamique ; dans `virtual public Base`, une base commune est partagée. |
| Lire directement des valeurs dans un objet avec `operator>>`. | Lire dans des variables temporaires et modifier l'objet seulement après validation de la saisie. |
| Supposer qu'une ouverture de fichier suffit. | Vérifier aussi les écritures, la lecture et la fin normale du fichier. |
| Confondre un arbre avec une liste chaînée. | Un nœud d'arbre binaire possède deux liens vers des enfants ; une liste simple ne possède qu'un lien vers le suivant. |
| Déréférencer `end()` ou réutiliser un itérateur invalide. | Tester l'itérateur et tenir compte des réallocations dans `vector`. |
| Appeler `std::sort` sur une `std::list`. | Employer `liste.sort()` (`std::sort` exige des itérateurs à accès aléatoire). |
| Omettre un fichier `.cpp` lors de la compilation. | Compiler toutes les unités de traduction nécessaires, puis vérifier les messages de l'éditeur de liens. |
{{< /tableau >}}

## Annexe 9. Exercices de consolidation propres à l'annexe {#exercices-de-consolidation-propres-a-l-annexe}

1. **Surcharge et validation.** Ajoutez à `Complexe` un opérateur `==` comparant les deux composantes. Modifiez ensuite la lecture pour vérifier qu'une saisie non numérique ne change pas la valeur déjà mémorisée.
2. **Rapport de notes.** Lisez un fichier contenant une note entière par ligne, stockez les valeurs dans un `vector<int>`, triez-les avec `std::sort`, puis affichez la moyenne et le nombre de notes supérieures ou égales à 60. Traitez les erreurs de fichier.
3. **Projet multifichier.** Ajoutez une méthode `changerPrix(double)` à `Article` ; déclarez-la dans `Article.h`, définissez-la dans `Article.cpp`, puis vérifiez son effet depuis `main.cpp`.
4. **Approfondissement facultatif.** Dans l'arbre binaire, affichez le nombre de valeurs visitées lors d'une recherche. Comparez l'insertion de nombres déjà triés et celle d'une série plus équilibrée.

{{< boite type="synthese" >}}
Cette annexe sert à **compléter** le module 4, non à le remplacer. Les acquis à retenir sont les suivants :

1. l'héritage virtuel peut partager une base commune dans un losange (cas avancé) ;
2. une surcharge d'opérateur doit être cohérente et valider correctement ses entrées ;
3. les programmes qui lisent des fichiers doivent vérifier les erreurs ;
4. les conteneurs et algorithmes de la STL évitent beaucoup de code manuel ;
5. un projet multifichier requiert la compilation des différentes implémentations.

Pour l'étude principale, donnez la priorité à la STL, aux fichiers et au projet multifichier. L'arbre et l'héritage virtuel peuvent être consultés comme approfondissements.
{{< /boite >}}
