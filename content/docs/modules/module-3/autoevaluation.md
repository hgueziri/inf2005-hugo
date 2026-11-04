---
title: "Module 3 : questionnaire d'autoévaluation"
linkTitle: "Autoévaluation"
weight: 90
bookToC: false
# Questions affichées par le shortcode « qcm » (layouts/shortcodes/qcm.html).
# reponse : numéro du bon choix (1 = premier) ; revoir : identifiant de la section du module à revoir.
qcm:
  - question: "Pour la fonction `int somme(int a, int b)`, que sont `2` et `3` dans l'appel `somme(2, 3)` ?"
    choix:
      - "Des paramètres."
      - "Des arguments."
      - "Des variables globales."
      - "Des valeurs de retour."
    reponse: 2
    explication: "Les **paramètres** (`a` et `b`) sont déclarés dans l'en-tête de la fonction ; les **arguments** (`2` et `3`) sont les valeurs fournies lors de l'appel."
    revoir: "appel-arguments-et-parametres"
  - question: "La variable `resultat` est déclarée dans la fonction `calculerCarre`. Peut-on l'utiliser directement dans `main()` ?"
    choix:
      - "Non : c'est une variable locale, accessible seulement dans le bloc où elle est déclarée."
      - "Oui, toutes les variables d'un programme sont accessibles partout."
      - "Oui, à condition d'avoir appelé `calculerCarre` auparavant."
      - "Oui, si une variable de même nom existe dans `main()`."
    reponse: 1
    explication: "Une variable locale n'existe que dans la portée de son bloc. Pour transmettre un résultat à l'appelant, la fonction le renvoie avec `return`."
    revoir: "variables-locales-et-portee"
  - question: "Qu'affiche ce programme ?"
    code: |
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
          int a = 4;
          ajouterUnParValeur(a);
          std::cout << a << ' ';
          ajouterUnParReference(a);
          std::cout << a << '\n';
      }
    choix:
      - "`5 6`"
      - "`5 5`"
      - "`4 5`"
      - "`4 4`"
    reponse: 3
    explication: "Par valeur, la fonction travaille sur une copie : `a` reste à 4. Par référence (`int&`), le paramètre désigne la variable de l'appelant : `a` passe à 5."
    revoir: "passage-par-reference"
  - question: "Une fonction doit lire un `std::string` volumineux sans le copier ni le modifier. Quel paramètre convient le mieux ?"
    choix:
      - "`std::string texte`"
      - "`std::string& texte`"
      - "`void texte`"
      - "`const std::string& texte`"
    reponse: 4
    explication: "La référence évite la copie, et `const` garantit que la fonction ne modifie pas la chaîne. Une référence non constante (`std::string&`) servirait plutôt à modifier volontairement la variable de l'appelant."
    revoir: "passage-par-reference"
  - question: "Pourquoi écrit-on le prototype `int somme(int, int);` avant `main()` lorsque la définition de `somme` se trouve plus bas dans le fichier ?"
    choix:
      - "Pour que `somme` s'exécute avant `main()`."
      - "Parce que le compilateur doit connaître la déclaration d'une fonction avant son premier appel."
      - "Pour accélérer l'exécution de la fonction."
      - "Pour rendre la fonction accessible aux autres programmes."
    reponse: 2
    explication: "Le compilateur lit le fichier de haut en bas : il doit connaître le nom, les paramètres et le type de retour de `somme` avant de rencontrer l'appel. Le prototype décrit l'ordre d'écriture, pas l'ordre d'exécution."
    revoir: "la-declaration-d-une-fonction-prototype"
  - question: "Laquelle de ces paires de déclarations ne constitue **pas** une surcharge valide ?"
    choix:
      - "`int somme(int a, int b);` et `double somme(double a, double b);`"
      - "`int somme(int a, int b);` et `int somme(int a, int b, int c);`"
      - "`int calcul(int x);` et `double calcul(int x);`"
      - "`void afficher(int n);` et `void afficher(std::string s);`"
    reponse: 3
    explication: "Des surcharges doivent se distinguer par le type, le nombre ou l'ordre de leurs paramètres. Le seul type de retour ne suffit pas : les deux fonctions `calcul` ont la même liste de paramètres."
    revoir: "la-surcharge-des-fonctions"
  - question: "Pour le tableau `int notes[5];`, quels indices sont valides ?"
    choix:
      - "De `0` à `4`."
      - "De `1` à `5`."
      - "De `0` à `5`."
      - "Tout indice positif."
    reponse: 1
    explication: "Les indices commencent à 0. L'accès `notes[5]` est hors limites : c'est un **comportement indéfini**, que le compilateur ne détecte pas forcément."
    revoir: "declaration-initialisation-et-parcours"
  - question: "La fonction `void ajouterDeux(int notes[], int taille)` reçoit un tableau. Pourquoi faut-il lui transmettre aussi `taille` ?"
    choix:
      - "Pour qu'elle puisse copier le tableau."
      - "Parce qu'une fonction C++ doit toujours avoir au moins deux paramètres."
      - "Pour qu'elle puisse trier le tableau."
      - "Parce que le paramètre `int notes[]` se comporte comme un pointeur vers le premier élément : la fonction ne connaît pas la taille du tableau."
    reponse: 4
    explication: "Un tableau C transmis à une fonction ne transporte pas sa taille. Les modifications de ses éléments sont visibles dans l'appelant, et une taille trop grande provoquerait un accès hors limites."
    revoir: "passer-un-tableau-a-une-fonction"
  - question: "Quelle condition la **recherche binaire** exige-t-elle ?"
    choix:
      - "Le tableau doit être trié dans l'ordre utilisé pour les comparaisons."
      - "Le tableau doit contenir un nombre pair d'éléments."
      - "Le tableau ne doit contenir aucun doublon."
      - "Les éléments doivent être des nombres positifs."
    reponse: 1
    explication: "La recherche binaire compare la clé à l'élément central, puis poursuit dans la moitié où elle peut se trouver : cela n'a de sens que si le tableau est trié. La recherche linéaire, elle, fonctionne aussi sur des données non triées."
    revoir: "recherche-binaire"
  - question: "Que fait le **tri à bulle** ?"
    choix:
      - "Il cherche l'élément central, puis trie chaque moitié séparément."
      - "Il compare des éléments voisins et les échange s'ils sont dans le mauvais ordre ; à chaque passage, l'une des plus grandes valeurs restantes se place vers la fin."
      - "Il copie le tableau dans un nouveau tableau déjà trié."
      - "Il trie le tableau en une seule comparaison par élément."
    reponse: 2
    explication: "Le tri à bulle est simple à comprendre, mais il demande un nombre d'opérations proportionnel à *n*² : son intérêt est surtout pédagogique. Dans les programmes usuels, on utilise les algorithmes de la bibliothèque standard."
    revoir: "tri-a-bulle"
  - question: 'Que renvoie `texte.find("xyz")` lorsque la sous-chaîne est absente de `texte` (un objet `std::string`) ?'
    choix:
      - "`0`"
      - "La longueur de `texte`."
      - "La valeur spéciale `std::string::npos`."
      - "Rien : le programme s'arrête avec une erreur."
    reponse: 3
    explication: "`find()` renvoie la position de la première occurrence, en commençant à 0, ou `std::string::npos` en cas d'absence. Vérifiez ce résultat avant d'utiliser la position."
    revoir: "rechercher-dans-une-chaine-avec-find"
  - question: 'Combien de cases un tableau de `char` doit-il compter pour contenir la chaîne C `"Bonjour"` ?'
    choix:
      - "7"
      - "8"
      - "6"
      - "9"
    reponse: 2
    explication: "`Bonjour` compte sept lettres, mais une chaîne C se termine par le caractère nul `'\\0'`, qui occupe une case de plus. Pour du nouveau code C++, `std::string` est habituellement préférable."
    revoir: "chaines-c-tableaux-de-caracteres"
---

# Module 3 : questionnaire d'autoévaluation

Ce questionnaire n'est pas noté. Il vous permet de vérifier, à votre rythme, que les notions du module 3 sont bien comprises. Choisissez une réponse pour chaque question : la bonne réponse et une explication s'affichent aussitôt, avec un lien vers la section du module à revoir au besoin. Vos réponses ne sont ni enregistrées ni transmises, et vous pouvez recommencer autant de fois que vous le souhaitez.

{{< qcm >}}
