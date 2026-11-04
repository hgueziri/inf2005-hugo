---
title: "Travail pratique 4 : Héritage, polymorphisme, surcharge, fichiers et STL"
linkTitle: "Travail pratique 4"
description: "INF 2005 – Programmation orientée objet avec C++"
weight: 40
---

{{< figure-cours src="figures/banner_4.png" page="/docs/modules/module-4" alt="Bannière du cours INF 2005 – Programmation orientée objet avec C++" largeur="100%" >}}

# Travail pratique 4 : Héritage, polymorphisme, surcharge, fichiers et STL

{{< boite type="consigne" titre="Consignes de remise" >}}
- Utilisez le [gabarit Travail pratique 4](../../a-propos/ressources/gabarits/INF2005_Travail-Pratique-4.docx) (format .docx) pour consigner certaines informations relatives à la résolution des exercices.
- Insérez des commentaires (lignes précédées de `//` ou paragraphes délimités par `/*` et `*/`) dans vos programmes pour en décrire les différents éléments ou étapes.
- Faites la preuve du bon fonctionnement de votre programme en fournissant dans le gabarit une ou plusieurs copie-écrans témoignant de l’exécution du programme, et des résultats obtenus.
- Quand vous avez fini les exercices, finissez de remplir le gabarit, compressez (.zip) l’ensemble des fichiers sources C++ (un pour chacun des quatre exercices) ainsi que le fichier `inventaire.txt` généré à l’exercice 4 et déposez le tout sur le site de la TÉLUQ. Pour accéder au dépôt, rejoignez MaTÉLUQ puis En cours > INF 2005 > tableau présentant les différentes activités du cours.
{{< /boite >}}

{{< boite type="contenu" >}}
**Objectif du travail :** écrire des programmes C++ orientés objet plus complets en utilisant l'héritage, les fonctions virtuelles, le polymorphisme, la surcharge d'opérateurs, les fichiers et quelques éléments de la bibliothèque STL.
{{< /boite >}}

## Table des matières {#table-des-matieres}

- [1 Présentation du travail pratique](#presentation-du-travail-pratique)
- [2 Rappel : compiler et exécuter un fichier C++](#rappel-compiler-et-executer-un-fichier-c)
  - [2.1 Dans VS Code](#dans-vs-code)
  - [2.2 Dans Jupyter Notebook ou Google Colab](#dans-jupyter-notebook-ou-google-colab)
- [3 Exercice 1 – Héritage et classes dérivées (3 pts)](#exercice-1-heritage-et-classes-derivees-3-pts)
- [4 Exercice 2 – Fonctions virtuelles et polymorphisme (3 pts)](#exercice-2-fonctions-virtuelles-et-polymorphisme-3-pts)
- [5 Exercice 3 – Surcharge d'opérateurs et fonctions amies (3 pts)](#exercice-3-surcharge-d-operateurs-et-fonctions-amies-3-pts)
- [6 Exercice 4 – Système d'inventaire (6 pts)](#exercice-4-systeme-d-inventaire-6-pts)
- [7 Barème récapitulatif](#bareme-recapitulatif)
- [8 Critères généraux d'évaluation](#criteres-generaux-d-evaluation)

## 1. Présentation du travail pratique {#presentation-du-travail-pratique}

{{< boite type="synthese" titre="Synthèse – lecture rapide" >}}
Ce travail pratique est le plus avancé avant le projet final. Il demande de concevoir des classes, de justifier les relations d'héritage, de manipuler des objets avec polymorphisme, de surcharger des opérateurs et d'utiliser des fichiers ou des conteneurs STL pour organiser les données.
{{< /boite >}}

{{< boite type="consigne" >}}

- Remettez un fichier source C++ par exercice : `TP4_exercice1.cpp`, `TP4_exercice2.cpp`, `TP4_exercice3.cpp` et `TP4_exercice4.cpp`.
- Chaque programme doit compiler avec la commande `g++ -std=c++17 -Wall -Wextra`.
- Chaque programme doit utiliser au moins deux classes, sauf indication contraire.
- Les attributs doivent être privés ou protégés lorsque cela est pertinent.
- Les méthodes doivent être nommées clairement.
- Ajoutez des commentaires utiles pour expliquer les choix importants.
- Fournissez des captures d'écran montrant la compilation, l'exécution et les résultats obtenus.

{{< /boite >}}

{{< boite type="attention" >}}
Les exercices ne doivent pas être résolus uniquement avec des fonctions globales. Le but est de pratiquer réellement la programmation orientée objet avancée : classes, héritage, polymorphisme, surcharge et organisation du code.
{{< /boite >}}

## 2. Rappel : compiler et exécuter un fichier C++ {#rappel-compiler-et-executer-un-fichier-c}

### 2.1. Dans VS Code {#dans-vs-code}

Créer un fichier source, par exemple `TP4_exercice1.cpp`, puis exécuter dans le terminal :

```bash
g++ -std=c++17 -Wall -Wextra TP4_exercice1.cpp -o exercice1
./exercice1
```

Sous Windows, l'exécution peut aussi se faire avec :

```bash
exercice1.exe
```

### 2.2. Dans Jupyter Notebook ou Google Colab {#dans-jupyter-notebook-ou-google-colab}

Première cellule : créer le fichier source.

```bash
%%writefile TP4_exercice1.cpp
#include <iostream>

int main() {
    std::cout << "Test du TP4" << std::endl;
    return 0;
}
```

Deuxième cellule : compiler et exécuter.

```bash
%%bash
g++ -std=c++17 -Wall -Wextra TP4_exercice1.cpp -o exercice1
./exercice1
```

## 3. Exercice 1 – Héritage et classes dérivées (3 pts) {#exercice-1-heritage-et-classes-derivees-3-pts}

On souhaite modéliser une application de gestion de personnes dans une université.

Le système doit gérer des personnes, des étudiantes et étudiants, ainsi que des membres du personnel. Une personne possède un nom, un identifiant et une adresse courriel. Un étudiant possède en plus un programme d'études et une moyenne ; quant au membre du personnel, il possède en plus un poste et un salaire annuel.

### Travail demandé {#travail-demande}

Écrire un programme C++ qui :

1. définit une classe de base `Personne` ;
2. définit deux classes dérivées : `Etudiant` et `Employe` ;
3. utilise des constructeurs pour initialiser correctement les objets ;
4. utilise des méthodes d'affichage adaptées à chaque classe ;
5. crée au moins deux étudiants et deux employés ;
6. affiche toutes les informations sous forme de rapport ;
7. calcule et affiche la moyenne générale des étudiants ;
8. calcule et affiche le salaire annuel moyen des employés.

### Contraintes obligatoires {#contraintes-obligatoires}

- Les attributs ne doivent pas être publics.
- La classe `Personne` doit contenir les informations communes.
- Les classes dérivées doivent réutiliser le constructeur de la classe de base.
- Le programme doit montrer clairement ce qui est commun et ce qui est spécialisé.

### Structure minimale attendue {#structure-minimale-attendue}

```cpp
class Personne {
protected:
    std::string nom;
    std::string identifiant;
    std::string courriel;
public:
    Personne(std::string n, std::string id, std::string c);
    void afficherBase() const;
};

class Etudiant : public Personne {
    // attributs et methodes propres a un etudiant
};

class Employe : public Personne {
    // attributs et methodes propres a un employe
};
```

{{< boite type="livrable" >}}
Fichier attendu : `TP4_exercice1.cpp`. Inclure une capture d'écran de l'exécution et une courte justification expliquant pourquoi l'héritage est pertinent dans cet exercice.
{{< /boite >}}

## 4. Exercice 2 – Fonctions virtuelles et polymorphisme (3 pts) {#exercice-2-fonctions-virtuelles-et-polymorphisme-3-pts}

On souhaite estimer le coût des déplacements effectués en ville au cours d'une journée. Chaque trajet peut afficher son mode de transport et calculer son prix. Les modes de transport considérés sont l'autobus, le taxi et le vélo en libre-service, avec les tarifs (fictifs) suivants :

- autobus : 3,75 $ par trajet, quelle que soit la distance parcourue ;
- taxi : 4,10 $ de prise en charge, plus 2,05 $ par kilomètre parcouru ;
- vélo en libre-service : 1,25 $ pour déverrouiller le vélo, plus 0,15 $ par minute d'utilisation.

### Travail demandé {#travail-demande-2}

Écrire un programme C++ qui :

1. définit une classe de base `Trajet` ;
2. définit trois classes dérivées : `TrajetAutobus`, `TrajetTaxi` et `TrajetVelo` ;
3. déclare une méthode virtuelle `prix()` dans la classe de base ;
4. redéfinit la méthode `prix()` dans chaque classe dérivée ;
5. utilise un tableau ou un `vector` de pointeurs vers `Trajet` ;
6. parcourt les trajets et affiche pour chacun son mode de transport et son prix ;
7. calcule le prix total de tous les trajets ;
8. libère correctement la mémoire si des objets sont créés avec `new`.

### Contraintes obligatoires {#contraintes-obligatoires-2}

- Utiliser au moins une fonction virtuelle.
- Utiliser le polymorphisme par pointeur ou par référence.
- Ajouter un destructeur virtuel dans la classe de base.
- Ne pas utiliser une longue série de `if` pour distinguer les types de trajets.

### Exemple d'affichage attendu {#exemple-d-affichage-attendu}

```text
+-----------------+------------+
| Trajet          | Prix ($)   |
+-----------------+------------+
| Autobus         | 3.75       |
| Taxi (8 km)     | 20.50      |
| Velo (20 min)   | 4.25       |
+-----------------+------------+

Prix total : 28.50 $
```

{{< boite type="important" >}}
Cet exercice vérifie la compréhension de la liaison dynamique. Le même appel, par exemple `trajet->prix()`, doit produire un comportement différent selon le type réel de l'objet.
{{< /boite >}}

{{< boite type="livrable" >}}
Fichier attendu : `TP4_exercice2.cpp`. Inclure une capture d'écran de l'exécution et une courte explication du rôle du mot clé `virtual`.
{{< /boite >}}

## 5. Exercice 3 – Surcharge d'opérateurs et fonctions amies (3 pts) {#exercice-3-surcharge-d-operateurs-et-fonctions-amies-3-pts}

On souhaite créer une classe `Fraction` permettant de manipuler des nombres rationnels.

Une fraction possède un numérateur et un dénominateur. Le dénominateur ne doit jamais être nul. Les fractions doivent être simplifiées automatiquement.

### Travail demandé {#travail-demande-3}

Écrire un programme C++ qui :

1. définit une classe `Fraction` ;
2. protège les attributs `numerateur` et `denominateur` ;
3. vérifie qu'une fraction ne possède jamais un dénominateur nul ;
4. simplifie les fractions automatiquement ;
5. surcharge l'opérateur `+` pour additionner deux fractions ;
6. surcharge l'opérateur `==` pour comparer deux fractions ;
7. surcharge l'opérateur `<<` pour afficher une fraction ;
8. utilise au moins une fonction amie lorsque cela est justifié ;
9. teste le programme avec au moins quatre fractions différentes.

### Contraintes obligatoires {#contraintes-obligatoires-3}

- Utiliser une méthode privée pour simplifier une fraction.
- Utiliser le pointeur `this` dans au moins une méthode.
- Gérer le cas d'un dénominateur nul.
- Afficher clairement les opérations effectuées.

### Structure minimale attendue {#structure-minimale-attendue-2}

```cpp
class Fraction {
private:
    int numerateur;
    int denominateur;

    void simplifier();

public:
    Fraction(int n, int d);
    ...
};
```

### Exemple d'affichage attendu {#exemple-d-affichage-attendu-2}

```text
f1 = 1/2
f2 = 1/3
f3 = f1 + f2 = 5/6

f4 = 2/4
f4 apres simplification = 1/2

Comparaison f1 == f4 : vrai
```

{{< boite type="livrable" >}}
Fichier attendu : `TP4_exercice3.cpp`. Inclure une capture d'écran de l'exécution et une courte explication de l'utilité de la surcharge d'opérateurs dans ce cas.
{{< /boite >}}

## 6. Exercice 4 – Système d'inventaire (6 pts) {#exercice-4-systeme-d-inventaire-6-pts}

On souhaite gérer un inventaire de produits à l'aide d'objets C++ et de la bibliothèque STL.

Chaque produit possède un code, un nom, une quantité et un prix unitaire. Les produits doivent être stockés dans un `vector`. Le programme doit pouvoir afficher l'inventaire, rechercher un produit, trier les produits et sauvegarder les résultats dans un fichier.

### Travail demandé {#travail-demande-4}

Écrire un programme C++ qui :

1. définit une classe `Produit` ;
2. crée un `vector` contenant au moins huit produits ;
3. affiche tous les produits sous forme de tableau ;
4. calcule la valeur totale de chaque produit : *quantité* × *prix*;
5. calcule la valeur totale de l'inventaire ;
6. trie les produits par prix unitaire croissant ;
7. recherche un produit à partir de son code ;
8. sauvegarde l'inventaire trié dans un fichier nommé `inventaire.txt`, où chaque ligne contient les informations d'un produit et affiche un message confirmant sa création ;
9. relit le fichier et affiche le contenu.

### Contraintes obligatoires {#contraintes-obligatoires-4}

- Utiliser `std::vector`.
- Utiliser au moins un itérateur ou une boucle basée sur les intervalles.
- Utiliser `std::sort` avec une fonction ou une expression lambda.
- Utiliser `ofstream` pour écrire dans un fichier.
- Le code doit être organisé en fonctions.

### Structure minimale attendue {#structure-minimale-attendue-3}

```cpp
class Produit {
private:
    std::string code;
    std::string nom;
    int quantite;
    double prix;

public:
    Produit(std::string c, std::string n, int q, double p);
    double valeurTotale() const;
    std::string getCode() const;
    void afficher() const;
};

void afficherInventaire(const std::vector<Produit>& produits);
void trierParPrix(std::vector<Produit>& produits);
int rechercherParCode(const std::vector<Produit>& produits, const std::string& code);
void sauvegarderInventaire(const std::vector<Produit>& produits, const std::string& nomFichier);
```

### Exemple d'affichage attendu {#exemple-d-affichage-attendu-3}

```text
Inventaire initial

+--------+----------------+----------+----------+----------+
| Code   | Nom            | Quantite | Prix     | Valeur   |
+--------+----------------+----------+----------+----------+
| P001   | Clavier        | 10       | 29.99    | 299.90   |
| P002   | Souris         | 25       | 14.50    | 362.50   |
...

Valeur totale de l'inventaire : 1840.35

Recherche du code P002 : produit trouve.
Inventaire trie et sauvegarde dans inventaire.txt.
```

{{< boite type="livrable" >}}
Fichier attendu : `TP4_exercice4.cpp`. Inclure une capture d'écran de l'exécution et le fichier généré `inventaire.txt`.
{{< /boite >}}

## 7. Barème récapitulatif {#bareme-recapitulatif}

{{< boite type="bareme" >}}

| Élément évalué | Points |
|---|---|
| Exercice 1 – Héritage et classes dérivées | 3 |
| Exercice 2 – Fonctions virtuelles et polymorphisme | 3 |
| Exercice 3 – Surcharge d'opérateurs et fonctions amies | 3 |
| Exercice 4 – Système d'inventaire | 6 |
| **Total** | **15** |

{{< /boite >}}

## 8. Critères généraux d'évaluation {#criteres-generaux-d-evaluation}

{{< tableau >}}
| Critère | Attentes |
|---|---|
| Compilation | Le programme compile sans erreur avec `g++ -std=c++17 -Wall -Wextra`. |
| Conception orientée objet | Les classes sont cohérentes, les attributs sont protégés et les méthodes sont pertinentes. |
| Héritage et polymorphisme | L'héritage est utilisé correctement et les fonctions virtuelles produisent un comportement polymorphique réel. |
| Surcharge et fonctions amies | Les opérateurs surchargés sont utiles, lisibles et correctement définis. |
| Fichiers et STL | Les conteneurs, le tri, la recherche et l'écriture dans un fichier sont utilisés correctement. |
| Lisibilité | Le code est indenté, organisé et contient des commentaires utiles. |
| Preuves d'exécution | Les captures d'écran et les fichiers générés montrent clairement que le programme fonctionne. |
{{< /tableau >}}

{{< boite type="attention" >}}
Un programme qui utilise seulement des variables et des fonctions globales, sans véritable conception orientée objet, ne répond pas aux attentes de ce travail pratique.
{{< /boite >}}
