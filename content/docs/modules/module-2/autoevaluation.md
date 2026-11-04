---
title: "Module 2 : questionnaire d'autoévaluation"
linkTitle: "Autoévaluation"
weight: 90
bookToC: false
# Questions affichées par le shortcode « qcm » (layouts/shortcodes/qcm.html).
# reponse : numéro du bon choix (1 = premier) ; revoir : identifiant de la section du module à revoir.
qcm:
  - question: "Vous modifiez le message affiché dans `main.cpp` et vous enregistrez le fichier, puis vous relancez `./main` sans recompiler. Que se passe-t-il ?"
    choix:
      - "Le nouveau message s'affiche."
      - "L'ancien message s'affiche : l'exécutable n'a pas changé."
      - "Le compilateur signale une erreur."
      - "Le fichier `main.cpp` est exécuté directement."
    reponse: 2
    explication: "Modifier le fichier source ne change pas l'exécutable déjà produit. Le cycle à retenir : écrire → enregistrer → **compiler** → exécuter → observer."
    revoir: "comprendre-le-role-des-outils"
  - question: "Quelle commande compile `main.cpp` selon la norme C++17 et produit un exécutable nommé `main` ?"
    choix:
      - "`./main main.cpp`"
      - "`g++ -o main.cpp main`"
      - "`g++ -std=c++17 main.cpp -o main`"
      - "`main.cpp -std=c++17`"
    reponse: 3
    explication: "`g++` compile le fichier source, `-std=c++17` choisit la norme et `-o main` donne son nom à l'exécutable. Cette commande se tape dans le terminal, pas dans le fichier C++."
    revoir: "etape-2-compiler-le-programme"
  - question: "Après l'instruction `int age;`, déclarée dans le corps d'une fonction, que vaut `age` ?"
    choix:
      - "Sa valeur n'est pas déterminée : il faut lui donner une valeur avant de la lire."
      - "Elle vaut `0`."
      - "Elle vaut `-1`."
      - "Le compilateur refuse cette déclaration."
    reponse: 1
    explication: "Une variable locale de type fondamental ne reçoit pas automatiquement une valeur déterminée. Prenez l'habitude d'initialiser explicitement : `int age = 0;`."
    revoir: "declarer-et-initialiser-une-variable"
  - question: "Qu'affiche ce fragment ?"
    code: |
      int a = 7;
      int b = 2;
      double r = a / b;
      std::cout << r << '\n';
    choix:
      - "`3.5`"
      - "`4`"
      - "Rien : le compilateur signale une erreur."
      - "`3`"
    reponse: 4
    explication: "`a / b` est une division entière entre deux `int` : elle donne `3`, et c'est cette valeur qui est ensuite placée dans `r`. Pour obtenir `3.5`, au moins un opérande doit être de type `double`, par exemple `7.0 / 2`."
    revoir: "calculs-arithmetiques-et-conversions"
  - question: "Qu'affiche ce fragment ?"
    code: |
      int x = 5;
      std::cout << x++ << ' ';
      std::cout << ++x << '\n';
    choix:
      - "`6 7`"
      - "`5 7`"
      - "`5 6`"
      - "`6 6`"
    reponse: 2
    explication: "`x++` fournit la valeur actuelle (`5`), puis `x` devient `6`. `++x` augmente d'abord `x` (qui devient `7`), puis fournit cette nouvelle valeur."
    revoir: "incrementation-et-decrementation"
  - question: "Que fait l'instruction `note = 50` ?"
    choix:
      - "Elle vérifie si `note` vaut 50."
      - "Elle déclare une constante nommée `note`."
      - "Elle donne la valeur 50 à la variable `note`."
      - "Elle affiche 50."
    reponse: 3
    explication: "`=` est l'affectation : elle remplace la valeur de la variable. La comparaison s'écrit `==` : `note == 50` vaut `true` ou `false` sans rien modifier."
    revoir: "comparer-des-valeurs"
  - question: "Quelle expression est vraie seulement lorsque `note` est comprise entre 0 et 100 inclusivement ?"
    choix:
      - "`note >= 0 && note <= 100`"
      - "`note >= 0 || note <= 100`"
      - "`0 <= note <= 100`"
      - "`!(note >= 0)`"
    reponse: 1
    explication: "Les deux conditions doivent être vraies : on les combine avec `&&` (ET). Avec `||`, l'expression serait vraie pour toute note. L'écriture mathématique `0 <= note <= 100` compile, mais elle ne fait pas ce qu'on attend en C++."
    revoir: "combiner-les-conditions-operateurs-logiques"
  - question: "Que vaut l'expression `7 + 2 * 3` ?"
    choix:
      - "`27`"
      - "`12`"
      - "`23`"
      - "`13`"
    reponse: 4
    explication: "La multiplication est prioritaire sur l'addition : `2 * 3` vaut 6, puis `7 + 6` vaut 13. Pour obtenir 27, il faut écrire `(7 + 2) * 3`."
    revoir: "priorite-des-operateurs"
  - question: "Qu'affiche ce fragment ?"
    code: |
      int choix = 1;
      switch (choix)
      {
      case 1:
          std::cout << "A";
      case 2:
          std::cout << "B";
          break;
      default:
          std::cout << "C";
      }
    choix:
      - "`A`"
      - "`B`"
      - "`AB`"
      - "`ABC`"
    reponse: 3
    explication: "Le `case 1` n'a pas de `break` : l'exécution continue dans le cas suivant (la *chute*, ou *fallthrough*) et affiche aussi `B`, puis le `break` quitte le `switch`."
    revoir: "la-structure-switch"
  - question: "Quelle est la particularité de la boucle `do/while` par rapport à la boucle `while` ?"
    choix:
      - "Son corps est exécuté au moins une fois, car la condition est évaluée après."
      - "Elle ne peut pas devenir une boucle infinie."
      - "Elle augmente automatiquement son compteur."
      - "Elle ne s'utilise qu'avec des nombres entiers."
    reponse: 1
    explication: "La boucle `do/while` exécute son corps une première fois **avant** d'évaluer la condition. Avec une condition fausse dès le départ, `while` n'exécute rien, alors que `do/while` exécute le corps une fois."
    revoir: "la-boucle-do-while"
  - question: "Qu'affiche ce fragment ?"
    code: |
      for (int i = 0; i < 5; i++)
      {
          if (i == 2)
          {
              continue;
          }
          std::cout << i << ' ';
      }
    choix:
      - "`0 1`"
      - "`0 1 2 3 4`"
      - "`2`"
      - "`0 1 3 4`"
    reponse: 4
    explication: "`continue` ignore la fin de l'itération courante et passe à la suivante : seule la valeur 2 n'est pas affichée. Avec `break`, la boucle s'arrêterait et le fragment afficherait `0 1`."
    revoir: "modifier-le-controle-break-continue-return"
  - question: "Avec `std::string ville;` puis `std::cin >> ville;`, l'utilisateur tape `Quebec City`. Que contient `ville` ?"
    choix:
      - "`Quebec City`"
      - "`Quebec`"
      - "`City`"
      - "Une chaîne vide."
    reponse: 2
    explication: "L'extraction avec `>>` s'arrête au premier espace. Pour lire une ligne complète, utilisez `std::getline(std::cin, ville);`."
    revoir: "lire-du-texte-et-ses-limites"
---

# Module 2 : questionnaire d'autoévaluation

Ce questionnaire n'est pas noté. Il vous permet de vérifier, à votre rythme, que les notions du module 2 sont bien comprises. Choisissez une réponse pour chaque question : la bonne réponse et une explication s'affichent aussitôt, avec un lien vers la section du module à revoir au besoin. Vos réponses ne sont ni enregistrées ni transmises, et vous pouvez recommencer autant de fois que vous le souhaitez.

{{< qcm >}}
