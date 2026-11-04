---
title: "Module 4 : questionnaire d'autoévaluation"
linkTitle: "Autoévaluation"
weight: 90
bookToC: false
# Questions affichées par le shortcode « qcm » (layouts/shortcodes/qcm.html), pour le module 4 et ses annexes.
# reponse : numéro du bon choix (1 = premier) ; revoir : identifiant de la section à revoir,
# dans le module, ou dans la page indiquée par « page » (annexes).
qcm:
  - question: "Quel est le rôle de `Article(std::string n, int q) : nom(n), quantite(q) {}` dans la classe `Article` ?"
    choix:
      - "C'est un destructeur : il libère l'objet."
      - "C'est un constructeur : il initialise les attributs d'un objet au moment de sa création."
      - "C'est une méthode qui affiche l'article."
      - "Il crée une copie de la classe `Article`."
    reponse: 2
    explication: "Le constructeur porte le nom de la classe et n'a pas de type de retour. La liste `: nom(n), quantite(q)` initialise les attributs. `Article livre(\"Livre C++\", 3);` crée un objet en appelant ce constructeur."
    revoir: "premiere-classe-l-exemple-d-un-article"
  - question: "Dans `main()`, le compilateur refuse l'instruction `livre.quantite = -3;`. Pourquoi ?"
    choix:
      - "`-3` n'est pas une valeur de type `int`."
      - "L'objet `livre` n'a pas encore été créé."
      - "`quantite` est un membre `private` : seuls les membres de la classe y ont accès directement."
      - "Il faudrait écrire `Article.quantite = -3;`."
    reponse: 3
    explication: "`private` réserve l'accès direct aux membres de la classe. De l'extérieur, on passe par les méthodes publiques, comme `ajouter()`, qui peuvent vérifier les valeurs reçues."
    revoir: "premiere-classe-l-exemple-d-un-article"
  - question: "Quelle déclaration définit une classe `Etudiant` qui dérive publiquement de `Personne` ?"
    choix:
      - "`class Etudiant : public Personne { /* ... */ };`"
      - "`class Personne : public Etudiant { /* ... */ };`"
      - "`class Etudiant extends Personne { /* ... */ };`"
      - "`class Etudiant(Personne) { /* ... */ };`"
    reponse: 1
    explication: "En C++, on indique après le nom de la classe dérivée le symbole `:`, le mode d'héritage, puis la classe de base. Le mot `extends` appartient à d'autres langages, comme Java."
    revoir: "la-declaration"
  - question: "Une classe dérivée peut-elle accéder directement aux membres `private` de sa classe de base ?"
    choix:
      - "Oui, toujours."
      - "Oui, à condition que l'héritage soit public."
      - "Non : ces membres n'existent pas dans l'objet dérivé."
      - "Non : ils existent bien dans l'objet dérivé, mais il faut passer par les méthodes publiques ou protégées de la base."
    reponse: 4
    explication: "Un membre `private` de la base fait partie de l'objet dérivé, mais il reste inaccessible directement depuis la classe dérivée. Un membre `protected`, lui, est accessible aux classes dérivées."
    revoir: "accessibilite-des-membres-herites"
  - question: "Dans quel ordre ce programme affiche-t-il ses messages ?"
    code: |
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
    choix:
      - "Constructeur Derivee, Constructeur Base, Destructeur Base, Destructeur Derivee"
      - "Constructeur Base, Constructeur Derivee, Destructeur Derivee, Destructeur Base"
      - "Constructeur Base, Constructeur Derivee, Destructeur Base, Destructeur Derivee"
      - "Constructeur Derivee, Destructeur Derivee"
    reponse: 2
    explication: "C++ construit d'abord la partie héritée de la base, puis la partie dérivée. La destruction se fait dans l'ordre inverse : d'abord la partie dérivée, puis la base."
    revoir: "les-constructeurs-et-les-destructeurs"
  - question: "Qu'affiche ce programme ?"
    code: |
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
    choix:
      - "`Cercle`"
      - "`Figure`"
      - "`Figure`, puis `Cercle`"
      - "Rien : le compilateur signale une erreur."
    reponse: 1
    explication: "La référence est de type `Figure&`, mais elle désigne un objet `Cercle`. Comme `dessiner()` est `virtual`, la version de l'objet réel est appelée : c'est le polymorphisme dynamique. Sans `virtual`, le programme afficherait `Figure`."
    revoir: "un-premier-appel-polymorphe"
  - question: "À quoi sert le mot clé `override` dans `void dessiner() const override` ?"
    choix:
      - "À rendre la méthode virtuelle dans la classe de base."
      - "À empêcher toute redéfinition future de la méthode."
      - "À demander au compilateur de vérifier que la méthode redéfinit bien une méthode virtuelle existante."
      - "À accélérer l'appel de la méthode."
    reponse: 3
    explication: "`override` évite des erreurs de signature : si la méthode ne redéfinit aucune méthode virtuelle de la base (nom, paramètres ou `const` différents), le compilateur le signale."
    revoir: "un-premier-appel-polymorphe"
  - question: "La classe `Figure` déclare `virtual double aire() const = 0;`. Qu'en déduit-on ?"
    choix:
      - "`aire()` renvoie toujours 0."
      - "`Figure` ne peut pas avoir de classes dérivées."
      - "La méthode `aire()` est privée."
      - "`aire()` est une fonction virtuelle pure : `Figure` est abstraite, et on ne peut pas créer d'objet `Figure` directement."
    reponse: 4
    explication: "Le `= 0` déclare une fonction virtuelle pure. Une classe qui en possède au moins une est abstraite ; ses classes dérivées doivent fournir `aire()` pour pouvoir être instanciées."
    revoir: "fonctions-virtuelles-pures-et-classes-abstraites"
  - question: "Si `operator+` est une méthode de la classe `Complexe`, à quel appel correspond l'expression `c1 + c2` ?"
    choix:
      - "`c2.operator+(c1)`"
      - "`c1.operator+(c2)`"
      - "`Complexe::operator+()`"
      - "`operator+(c1)`"
    reponse: 2
    explication: "La méthode est appelée sur l'objet de gauche (`c1`) et reçoit l'objet de droite (`c2`) en paramètre. Elle crée un nouvel objet `Complexe` sans modifier les deux objets initiaux."
    revoir: "principes-de-base"
  - question: "Que ne permet **pas** la surcharge d'opérateurs ?"
    choix:
      - "Changer la priorité d'un opérateur."
      - "Additionner deux objets `Complexe` avec `+`."
      - "Afficher un objet avec `<<`."
      - "Comparer deux objets avec `==`."
    reponse: 1
    explication: "On ne peut changer ni la priorité, ni l'associativité, ni le nombre d'opérandes d'un opérateur. La surcharge doit aussi rester cohérente avec le sens habituel de l'opérateur."
    revoir: "limitations"
  - question: "Qu'est-ce qu'une fonction amie (`friend`) d'une classe ?"
    choix:
      - "Une méthode héritée de la classe de base."
      - "Une fonction virtuelle redéfinie dans une classe dérivée."
      - "Une fonction qui n'est pas membre de la classe, mais qui est autorisée à accéder à ses membres privés ou protégés."
      - "Une fonction que seule la classe elle-même peut appeler."
    reponse: 3
    explication: "L'amitié est utile pour certains opérateurs, comme `<<`, mais elle affaiblit l'encapsulation si on l'utilise trop largement."
    revoir: "fonctions-et-classes-amies"
  - question: "Dans une méthode non statique, que désigne `this` ?"
    choix:
      - "La classe elle-même."
      - "Le premier attribut de la classe."
      - "La classe de base."
      - "Un pointeur vers l'objet sur lequel la méthode est appelée."
    reponse: 4
    explication: "`this` pointe vers l'objet courant, et `*this` désigne cet objet lui-même. C'est utile pour lever une ambiguïté entre un attribut et un paramètre, ou pour renvoyer l'objet courant."
    revoir: "l-utilisation-du-pointeur-this"
  - question: "Une pile `std::stack<int>` reçoit `push(1)`, puis `push(2)`, puis `push(3)`. Que renvoie `top()` ?"
    choix:
      - "`1`"
      - "`3`"
      - "`2`"
      - "`6`"
    reponse: 2
    explication: "Une pile suit le principe LIFO (*Last In, First Out*) : le dernier élément ajouté est le premier accessible et le premier retiré."
    revoir: "les-piles"
  - question: "Pour `std::vector<int> notes = {70, 82, 91};`, quelle est la différence entre `notes[3]` et `notes.at(3)` ?"
    choix:
      - "`notes[3]` est un accès hors limites au comportement indéfini, tandis que `notes.at(3)` détecte l'erreur et lance une exception."
      - "Aucune : les deux renvoient la dernière note."
      - "`notes.at(3)` ajoute une quatrième note au vecteur."
      - "`notes[3]` renvoie toujours `0`."
    reponse: 1
    explication: "Les indices valides vont de 0 à 2. L'opérateur `[]` ne vérifie pas l'indice ; la méthode `at()` le vérifie et signale l'erreur par une exception."
    revoir: "manipuler-std-vector-au-dela-du-premier-exemple"
    page: "/docs/modules/module-4/module-4-annexe"
  - question: "Quel conteneur choisir pour associer à chaque nom d'étudiant, unique, la note obtenue ?"
    choix:
      - "`std::stack<int>`"
      - "`std::vector<int>`"
      - "`std::queue<int>`"
      - "`std::map<std::string, int>`"
    reponse: 4
    explication: "Un `map` relie des clés uniques à des valeurs et se parcourt dans l'ordre des clés. Un `vector` convient à une suite de valeurs repérées par leur position, une `stack` à un traitement de type pile."
    revoir: "associer-des-cles-a-des-valeurs-avec-std-map"
    page: "/docs/modules/module-4/module-4-annexe"
  - question: "Vous compilez le projet multifichier avec `g++ -std=c++17 -Wall -Wextra Boisson.cpp main.cpp -o programme`, en oubliant `Article.cpp`. Que se passe-t-il ?"
    choix:
      - "Une erreur de syntaxe est signalée dans `Article.h`."
      - "Le programme s'exécute, mais sans les articles."
      - "L'éditeur de liens signale une *référence indéfinie* (*undefined reference*) vers des fonctions déclarées dans `Article.h`, mais non fournies."
      - "Aucune erreur : `g++` retrouve `Article.cpp` automatiquement."
    reponse: 3
    explication: "Les déclarations de `Article.h` suffisent au compilateur, mais l'éditeur de liens doit trouver les définitions, qui se trouvent dans `Article.cpp`. Il faut compiler tous les fichiers `.cpp` du projet."
    revoir: "exemple-compilation-dans-vs-code-ou-terminal"
    page: "/docs/modules/module-4/module-4-annexe"
  - question: "Dans un héritage en losange, `Document` et `Ressource` héritent toutes deux de `Identifiable`, et `FichierNumerique` hérite des deux. À quoi sert l'héritage virtuel (`virtual public Identifiable`) ?"
    choix:
      - "À rendre toutes les méthodes de `Identifiable` virtuelles."
      - "À faire partager par les deux branches un seul sous-objet `Identifiable` dans l'objet final."
      - "À empêcher la création d'objets `Identifiable`."
      - "À accélérer les appels de méthodes."
    reponse: 2
    explication: "Sans héritage virtuel, l'objet final contiendrait deux sous-objets `Identifiable`. Attention : `virtual` appliqué à une **base** et `virtual` appliqué à une **méthode** ont deux rôles différents."
    revoir: "heritage-virtuel-une-seule-base-dans-un-losange"
    page: "/docs/modules/module-4/module-4-annexe"
---

# Module 4 : questionnaire d'autoévaluation

Ce questionnaire n'est pas noté. Il vous permet de vérifier, à votre rythme, que les notions du module 4 et de ses annexes sont bien comprises. Choisissez une réponse pour chaque question : la bonne réponse et une explication s'affichent aussitôt, avec un lien vers la section à revoir au besoin. Vos réponses ne sont ni enregistrées ni transmises, et vous pouvez recommencer autant de fois que vous le souhaitez.

{{< qcm >}}
