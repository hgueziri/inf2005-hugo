---
title: "Examen final"
weight: 60
# Examen d'entraînement affiché par le shortcode « qcm » (layouts/shortcodes/qcm.html).
# reponse : numéro du bon choix (1 = premier) ; revoir et page : section du cours à revoir.
qcm:
  - partie: "Partie A - Conception à partir d'un code"
    contexte: |
      Le menu d'un carnet de recettes accepte une lettre, en majuscule ou en minuscule. Voici le traitement actuel :
    code: |
      char choix;
      std::cin >> choix;
      if (choix == 'a' || choix == 'A') {
          ajouterRecette();
      } else if (choix == 'c' || choix == 'C') {
          chercherRecette();
      } else if (choix == 'l' || choix == 'L') {
          listerRecettes();
      } else if (choix == 'q' || choix == 'Q') {
          quitter();
      } else {
          std::cout << "Choix invalide\n";
      }
    question: "D'autres options s'ajouteront au menu. Quelle structure exprime le plus clairement ce choix parmi plusieurs valeurs d'un même caractère ?"
    choix:
      - "Une suite de `if` indépendants (sans `else`), un par option, pour pouvoir ajouter une option sans toucher aux autres."
      - "Une classe abstraite `OptionMenu` et une classe dérivée par option, retrouvée dans un tableau de 26 objets indexé par la lettre."
      - "Un `switch (choix)` où chaque option regroupe deux étiquettes (`case 'a':` et `case 'A':`), terminé par un `default` pour les choix invalides."
      - "La conversion du caractère en entier (`int code = choix;`), puis la comparaison de `code` avec le code numérique de chaque lettre."
    reponse: 3
    explication: "`switch` convient à un choix parmi plusieurs valeurs entières ou caractères : chaque option est un `case`, et deux étiquettes placées l'une après l'autre partagent le même traitement, puisque l'exécution se poursuit jusqu'au `break`. `default` traite tous les autres caractères. (A) évalue tous les tests et ne permet plus de reconnaître simplement un choix invalide. (B) fonctionne, mais une hiérarchie de classes est démesurée pour un menu de quelques options sans données propres. (D) rend le code plus obscur sans rien simplifier."
    revoir: "la-structure-switch"
    page: "/docs/modules/module-2"
  - partie: "Partie A - Conception à partir d'un code"
    contexte: |
      Un club de course gère les inscriptions à son demi-marathon annuel. Cette année, le programme a planté lorsque le nombre d'inscriptions a dépassé 200 :
    code: |
      class Inscriptions {
      private:
          Coureur coureurs[200];
          int nombre = 0;

      public:
          void ajouter(const Coureur& c) {
              coureurs[nombre] = c;
              ++nombre;
          }

          int taille() const { return nombre; }
      };
    question: "Le nombre de participants varie beaucoup d'une année à l'autre. Quelle modification est la plus appropriée ?"
    choix:
      - "Remplacer le tableau et le compteur par un attribut privé `std::vector<Coureur>`, alimenté par `push_back()`, et faire renvoyer `coureurs.size()` par `taille()`."
      - "Porter la taille du tableau à 10 000 places, ce qui devrait suffire pour toutes les éditions futures du demi-marathon."
      - "Ajouter dans `ajouter()` un test qui refuse les nouvelles inscriptions lorsque le tableau est plein, en affichant un message d'erreur."
      - "Créer un second tableau de 200 places dans une classe dérivée `InscriptionsEtendues`, utilisée lorsque le premier tableau est plein."
    reponse: 1
    explication: "Un `std::vector` gère lui-même sa mémoire : sa taille augmente au fil des `push_back()`, et `size()` donne toujours le nombre exact d'éléments, sans compteur à tenir à jour. Pour le code qui utilise la classe, rien ne change. (B) repousse la limite sans la supprimer et réserve de la mémoire inutile. (C) évite le débordement, mais refuse des participants alors que rien ne justifie cette limite. (D) complique la classe et ne fait que repousser le problème."
    revoir: "manipuler-std-vector-au-dela-du-premier-exemple"
    page: "/docs/modules/module-4/module-4-annexe"
  - partie: "Partie A - Conception à partir d'un code"
    contexte: |
      Un laboratoire a écrit sous Linux un programme qui lance deux calculs en parallèle avec l'interface POSIX. Le programme doit maintenant fonctionner aussi sous Windows, où `<pthread.h>` n'est pas offert par tous les compilateurs.
    code: |
      #include <pthread.h>

      void* calculerSerie(void* argument) {
          int numero = *static_cast<int*>(argument);
          // ... calcul de la série numero ...
          return nullptr;
      }

      int main() {
          pthread_t t1, t2;
          int un = 1, deux = 2;
          pthread_create(&t1, nullptr, calculerSerie, &un);
          pthread_create(&t2, nullptr, calculerSerie, &deux);
          pthread_join(t1, nullptr);
          pthread_join(t2, nullptr);
          return 0;
      }
    question: "Quelle modification est la plus appropriée ?"
    choix:
      - "Conserver l'interface POSIX sous Linux et écrire une seconde version avec l'interface des threads de Windows, choisie à la compilation par des directives `#ifdef`."
      - "Remplacer les deux threads par deux appels successifs à `calculerSerie()`, puisque le programme fonctionne alors sur tous les systèmes."
      - "Lancer chaque calcul dans un processus distinct, en démarrant deux fois le programme à l'aide d'un script propre à chaque système."
      - "Utiliser `std::thread`, qui fait partie de la bibliothèque standard : `std::thread t1(calculerSerie, 1);`, puis `t1.join();`."
    reponse: 4
    explication: "`std::thread` fait partie de la bibliothèque standard depuis C++11 : le même code compile sous Linux, Windows et macOS, et la fonction peut recevoir ses arguments avec leur vrai type (ici un `int`), sans conversion depuis `void*`. (A) fonctionne, mais oblige à maintenir deux versions du même code. (B) est portable, mais supprime le parallélisme. (C) déplace le problème vers des scripts propres à chaque système et complique la récupération des résultats."
    revoir: "approche-moderne-std-thread"
    page: "/docs/modules/module-5"
  - partie: "Partie A - Conception à partir d'un code"
    contexte: |
      Un cinéma vend des billets réguliers et des billets étudiants, à moitié prix. La fonction `encaisser()` reçoit n'importe quel billet, mais les étudiants paient toujours le plein tarif :
    code: |
      class Billet {
      public:
          virtual ~Billet() = default;
          double prix() const { return 14.0; }
      };

      class BilletEtudiant : public Billet {
      public:
          double prix() const { return 7.0; }
      };

      void encaisser(const Billet& billet) {
          std::cout << "Montant : " << billet.prix() << " $\n";
      }

      int main() {
          BilletEtudiant b;
          encaisser(b);   // affiche « Montant : 14 $ »
          return 0;
      }
    question: "Quelle modification fait payer à chaque billet son propre prix, sans modifier `encaisser()` ?"
    choix:
      - "Écrire une seconde fonction `encaisser()`, surchargée, qui reçoit un `const BilletEtudiant&` et affiche le prix réduit."
      - "Déclarer `prix()` virtuelle dans `Billet` (`virtual double prix() const`) et la redéfinir avec `override` dans `BilletEtudiant`."
      - "Ajouter dans `Billet` un attribut `bool etudiant`, testé dans `prix()` pour renvoyer le plein tarif ou le tarif réduit selon le cas."
      - "Faire hériter `Billet` de `BilletEtudiant`, afin que le prix réduit soit trouvé en premier lors de l'appel à `prix()`."
    reponse: 2
    explication: "Sans `virtual`, l'appel `billet.prix()` est résolu à la compilation, d'après le type de la référence (`const Billet&`) : c'est toujours la version de `Billet` qui s'exécute. Une fonction virtuelle est choisie à l'exécution, selon le type réel de l'objet, et `override` fait vérifier la redéfinition par le compilateur. (A) fonctionne pour ces deux types, mais chaque nouvelle catégorie de billet exigerait une nouvelle fonction. (C) remplace le polymorphisme par un test qu'il faudra modifier pour chaque nouvelle catégorie. (D) inverse la relation : un billet n'**est** pas un billet étudiant."
    revoir: "un-premier-appel-polymorphe"
    page: "/docs/modules/module-4"
  - partie: "Partie A - Conception à partir d'un code"
    contexte: |
      Le module de journalisation d'un serveur offre trois fonctions, qui écrivent chacune une ligne datée dans le journal. Les personnes qui l'utilisent oublient souvent le nom exact de la fonction à appeler.
    code: |
      void journaliserTexte(const std::string& message);
      void journaliserCode(int codeErreur);
      void journaliserMesure(double valeur, const std::string& unite);

      // Utilisation :
      // journaliserTexte("Demarrage");
      // journaliserCode(404);
      // journaliserMesure(73.5, "ms");
    question: "Quelle conception rend ce module plus simple à utiliser, sans perdre le traitement propre à chaque type de donnée ?"
    choix:
      - "Une seule fonction `journaliser(const std::string& message)` ; le code appelant convertit lui-même chaque code d'erreur ou chaque mesure en texte avant l'appel."
      - "Une classe abstraite `EntreeJournal` et une classe dérivée par type de donnée, que le code appelant crée puis transmet au journal."
      - "Une fonction `journaliser(double valeur)` qui reçoit les codes d'erreur comme les mesures, et la fonction `journaliserTexte()` pour les messages."
      - "Trois fonctions surchargées, toutes nommées `journaliser()`, qui se distinguent par la liste de leurs paramètres."
    reponse: 4
    explication: "La surcharge permet de donner le même nom à des fonctions qui réalisent la même opération sur des données différentes : le compilateur choisit la bonne version d'après les arguments, et chaque version garde son traitement propre. On écrit simplement `journaliser(404)` ou `journaliser(73.5, \"ms\")`. (A) reporte la conversion sur chaque appel et disperse le format du journal. (B) fonctionne, mais oblige à créer un objet pour chaque ligne écrite : c'est beaucoup de code pour un besoin simple. (C) perd l'unité de mesure et confond les codes d'erreur avec des mesures."
    revoir: "la-surcharge-des-fonctions"
    page: "/docs/modules/module-3"
  - partie: "Partie B - Mise en situation de conception"
    contexte: |
      Un festival de musique planifie ses concerts. Chaque artiste peut se produire sur plusieurs scènes pendant le festival, et chaque scène accueille plusieurs artistes. Pour chaque prestation, on doit connaître l'heure de début, la durée et le cachet versé à l'artiste ; un même artiste peut recevoir des cachets différents d'une prestation à l'autre.
    question: "Où placer l'heure, la durée et le cachet ?"
    choix:
      - "Dans la classe `Artiste`, sous forme de trois attributs (`heure`, `duree` et `cachet`) mis à jour avant chacune de ses prestations."
      - "Dans une classe `Prestation`, qui relie un artiste à une scène et porte l'heure, la durée et le cachet ; le festival conserve la liste des prestations."
      - "Dans la classe `Scene`, qui conserve, pour chaque artiste qu'elle accueille, un seul cachet et une seule heure de passage."
      - "Dans une classe `ArtisteSurScene`, qui hérite à la fois de `Artiste` et de `Scene` et ajoute les trois données."
    reponse: 2
    explication: "L'heure, la durée et le cachet ne décrivent ni l'artiste seul ni la scène seule : ils décrivent leur **rencontre**, à un moment donné. Une classe `Prestation` donne une place à ces données, et un artiste peut avoir autant de prestations que nécessaire. (A) ne conserve qu'une prestation par artiste : la suivante écrase la précédente. (C) ne permet pas deux prestations du même artiste sur une même scène. (D) est faux : une prestation n'**est** ni un artiste ni une scène, elle les relie."
    revoir: "heritage-et-relations-entre-classes"
    page: "/docs/modules/module-1"
  - partie: "Partie B - Mise en situation de conception"
    contexte: |
      Un logiciel de traitement d'images accepte des filtres écrits par d'autres entreprises. Certains filtres sont de mauvaise qualité : il leur arrive de planter ou d'écrire n'importe où en mémoire. L'éditeur veut qu'un filtre défaillant ne fasse jamais perdre le travail en cours de l'utilisateur.
    question: "Comment exécuter les filtres ?"
    choix:
      - "Dans un thread distinct, créé pour chaque filtre, afin qu'un plantage du filtre reste limité à ce thread."
      - "Directement dans le programme principal, après avoir soigneusement vérifié chaque filtre avant de l'accepter dans le catalogue."
      - "Dans un processus distinct, qui a son propre espace mémoire ; le logiciel lui transmet l'image, puis récupère le résultat."
      - "Dans un thread distinct, protégé par un `std::mutex` que le filtre doit verrouiller avant d'accéder à la mémoire du logiciel."
    reponse: 3
    explication: "Les threads d'un même processus partagent la même mémoire : un filtre qui écrit n'importe où peut corrompre les données du logiciel, et un plantage arrête tout le processus. Un processus distinct possède son propre espace mémoire : sa défaillance ne touche pas le logiciel, qui communique avec lui par un mécanisme prévu à cette fin et poursuit son travail. (A) et (D) offrent une fausse protection : un mutex n'empêche pas un code défaillant d'écrire en mémoire. (B) réduit le risque sans le supprimer."
    revoir: "processus-et-threads"
    page: "/docs/modules/module-5"
  - partie: "Partie B - Mise en situation de conception"
    contexte: |
      Une imprimante 3D partagée reçoit les travaux d'impression de plusieurs personnes. Les travaux doivent être réalisés dans leur ordre d'arrivée : on ajoute toujours un travail à la fin de la file d'attente, et on retire toujours le plus ancien.
    question: "Quel conteneur la classe `FileImpression` devrait-elle utiliser, dans un attribut privé, pour conserver les travaux en attente ?"
    choix:
      - "Un `std::queue<Travail>`, qui suit le principe « premier entré, premier sorti » : on ajoute à la fin et on retire au début."
      - "Un `std::stack<Travail>`, qui donne directement accès au travail ajouté le plus récemment à la file d'attente."
      - "Un `std::map<std::string, Travail>`, dont la clé est le nom de la personne qui a envoyé le travail d'impression."
      - "Un `std::vector<Travail>`, en insérant chaque nouveau travail au début du vecteur et en retirant le dernier élément."
    reponse: 1
    explication: "Une file (`queue`) suit le principe FIFO (*First In, First Out*) : le premier travail ajouté est le premier traité, et son interface n'offre que les opérations utiles à ce besoin. (B) est une pile (LIFO) : le dernier travail arrivé serait imprimé en premier. (C) range les travaux selon les noms, et non selon l'ordre d'arrivée, et une personne ne pourrait avoir qu'un travail à la fois. (D) respecte l'ordre, mais chaque insertion au début oblige à déplacer tous les éléments du vecteur, et rien n'empêche un accès au milieu de la file."
    revoir: "choisir-un-conteneur-adapte-au-probleme"
    page: "/docs/modules/module-4/module-4-annexe"
  - partie: "Partie B - Mise en situation de conception"
    contexte: |
      Un jeu d'échecs en ligne doit vérifier la validité de chaque coup. Toutes les pièces ont une couleur et une position, mais chaque type de pièce (roi, dame, tour, fou, cavalier, pion) se déplace selon sa propre règle. On souhaite aussi pouvoir ajouter des pièces propres à certaines variantes du jeu, comme le « chancelier ».
    question: "Comment organiser les classes des pièces ?"
    choix:
      - "Une seule classe `Piece`, avec un attribut `type` et une méthode `deplacementValide()` qui contient un `switch`, un cas par type de pièce."
      - "Une classe par type de pièce, sans classe de base commune ; l'échiquier conserve un tableau distinct pour chaque type de pièce."
      - "Une classe `Echiquier` qui hérite à la fois de `Roi`, de `Dame`, de `Tour`, de `Fou`, de `Cavalier` et de `Pion`."
      - "Une classe abstraite `Piece` (couleur, position) dotée d'une méthode virtuelle pure `deplacementValide()`, et une classe dérivée par type de pièce."
    reponse: 4
    explication: "Les pièces partagent des données (couleur, position) et une même question (« ce coup est-il valide ? »), mais chacune y répond à sa façon : c'est le cas du polymorphisme. L'échiquier manipule ses pièces au moyen de pointeurs vers `Piece` et appelle `deplacementValide()` sans connaître leur type ; une pièce de variante ne demande qu'une nouvelle classe dérivée. (A) concentre toutes les règles dans une méthode à modifier pour chaque nouvelle pièce. (B) oblige l'échiquier à traiter chaque type séparément. (C) est faux : un échiquier n'**est** pas une pièce, il **contient** des pièces."
    revoir: "fonctions-virtuelles-pures-et-classes-abstraites"
    page: "/docs/modules/module-4"
  - partie: "Partie B - Mise en situation de conception"
    contexte: |
      Une application de météo doit convertir des températures (Celsius, Fahrenheit, Kelvin) et des vitesses de vent (km/h, nœuds). Ces conversions sont de simples calculs : elles ne conservent aucune donnée d'un appel à l'autre et ne dépendent d'aucun état.
    question: "Comment les organiser ?"
    choix:
      - "Des fonctions libres, regroupées dans un module de conversion (par exemple `double celsiusVersFahrenheit(double c)`), que tout le programme peut appeler."
      - "Une classe `Convertisseur` sans attribut ; le code appelant crée un objet `Convertisseur` chaque fois qu'il doit faire une conversion."
      - "Une hiérarchie de classes, avec une classe abstraite `Conversion` et une classe dérivée par paire d'unités, instanciées au démarrage."
      - "Des variables globales qui contiennent le dernier résultat de chaque conversion, mises à jour par les fonctions de conversion."
    reponse: 1
    explication: "C++ est un langage multiparadigme : tout ne doit pas devenir une classe. Une classe se justifie lorsqu'elle regroupe des données et les opérations qui les protègent ; des calculs sans état s'expriment plus simplement par des fonctions, regroupées dans un module que tout le programme peut réutiliser. (B) crée des objets qui ne servent à rien. (C) multiplie les classes sans bénéfice, puisqu'aucune conversion n'a à être choisie à l'exécution. (D) ajoute un état partagé inutile, source d'erreurs."
    revoir: "les-langages-orientes-objet-et-la-place-de-c"
    page: "/docs/modules/module-1"
  - partie: "Partie C - Lecture de code"
    contexte: |
      Un formulaire d'inscription demande l'âge, puis le nom complet :
    code: |
      #include <iostream>
      #include <string>

      int main() {
          int age = 0;
          std::string nom;
          std::cout << "Age : ";
          std::cin >> age;
          std::cout << "Nom complet : ";
          std::getline(std::cin, nom);
          std::cout << "[" << nom << "] " << age << '\n';
          return 0;
      }
    question: "À l'invite « Age : », la personne tape `34` et appuie sur Entrée ; elle s'apprête ensuite à taper son nom, `Marie Curie`. Que se passe-t-il ?"
    choix:
      - "Le programme attend le nom, puis affiche `[Marie Curie] 34`."
      - "Le programme attend le nom, puis affiche `[Marie] 34`, car la lecture s'arrête au premier espace."
      - "Rien : le programme ne compile pas, car `>>` et `std::getline()` ne peuvent pas lire le même flot."
      - "Le programme n'attend pas le nom : il affiche aussitôt `[] 34`."
    reponse: 4
    explication: "`std::cin >> age` lit les chiffres `34`, mais laisse dans le flot la fin de ligne produite par la touche Entrée. `std::getline()` lit les caractères jusqu'à la prochaine fin de ligne : il la trouve aussitôt, et `nom` reste vide, sans que le programme attende la saisie. Lorsqu'on combine `>>` et `std::getline()`, il faut donc retirer cette fin de ligne du flot avant d'appeler `std::getline()`. (A) se produirait si le nom était lu en premier. (B) décrit le comportement de `std::cin >> nom` : `std::getline()` lit au contraire toute la ligne, espaces compris. (C) est faux : les deux lectures se combinent, à condition de tenir compte de la fin de ligne restante."
    revoir: "lire-du-texte-et-ses-limites"
    page: "/docs/modules/module-2"
  - partie: "Partie C - Lecture de code"
    question: "Qu'affiche ce programme ?"
    code: |
      #include <iostream>
      #include <vector>

      void effacerTableau(int t[], int taille) {
          for (int i = 0; i < taille; ++i) {
              t[i] = 0;
          }
      }

      void effacerVecteur(std::vector<int> v) {
          for (std::size_t i = 0; i < v.size(); ++i) {
              v[i] = 0;
          }
      }

      int main() {
          int tableau[3] = {12, 30, 25};
          std::vector<int> vecteur = {12, 30, 25};
          effacerTableau(tableau, 3);
          effacerVecteur(vecteur);
          std::cout << tableau[1] << ' ' << vecteur[1] << '\n';
          return 0;
      }
    choix:
      - "`30 30`"
      - "`0 30`"
      - "`0 0`"
      - "`30 0`"
    reponse: 2
    explication: "Un tableau C transmis à une fonction n'est pas copié : le paramètre `int t[]` se comporte comme un pointeur vers le premier élément du tableau de `main()`, et `effacerTableau()` modifie donc ce tableau. Un `std::vector` passé par valeur est au contraire copié, comme n'importe quelle variable : `effacerVecteur()` modifie sa copie, et `vecteur[1]` vaut toujours 30. Pour modifier le vecteur de l'appelant, il faudrait un paramètre `std::vector<int>& v`. (A) suppose que le tableau est copié, lui aussi. (C) suppose que le vecteur est transmis par référence. (D) inverse les deux comportements."
    revoir: "passer-un-tableau-a-une-fonction"
    page: "/docs/modules/module-3"
  - partie: "Partie C - Lecture de code"
    question: "Qu'affiche ce programme ?"
    code: |
      #include <iostream>

      class Montant {
      private:
          int cents;

      public:
          explicit Montant(int c) : cents(c) {}

          Montant operator+(const Montant& autre) const {
              return Montant(cents + autre.cents);
          }

          Montant operator*(int facteur) const {
              return Montant(cents * facteur);
          }

          int valeur() const { return cents; }
      };

      int main() {
          Montant a(500);
          Montant b(150);
          Montant total = a + b * 3;
          std::cout << total.valeur() << ' ' << a.valeur() << '\n';
          return 0;
      }
    choix:
      - "`1950 500`"
      - "`950 950`"
      - "`950 500`"
      - "`1950 1950`"
    reponse: 3
    explication: "Un opérateur surchargé garde la priorité de l'opérateur d'origine : `a + b * 3` se lit `a + (b * 3)`, soit 500 + 450 = 950. Les deux opérateurs sont des méthodes `const` qui renvoient un nouvel objet : `a` n'est pas modifié et vaut toujours 500. Pour calculer (a + b) × 3, il faudrait écrire des parenthèses."
    revoir: "limitations"
    page: "/docs/modules/module-4"
  - partie: "Partie C - Lecture de code"
    question: "Qu'affiche ce programme ?"
    code: |
      #include <iostream>

      class Minuterie {
      private:
          int minutes;
          int secondes;

      public:
          Minuterie() : minutes(0), secondes(0) {}
          explicit Minuterie(int s) : minutes(s / 60), secondes(s % 60) {}
          Minuterie(int m, int s) : minutes(m + s / 60), secondes(s % 60) {}

          void afficher() const {
              std::cout << minutes << ':' << secondes << ' ';
          }
      };

      int main() {
          Minuterie a;
          Minuterie b(135);
          Minuterie c(1, 75);
          a.afficher();
          b.afficher();
          c.afficher();
          std::cout << '\n';
          return 0;
      }
    choix:
      - "`0:0 2:15 2:15`"
      - "`0:0 135:0 1:75`"
      - "`0:0 2:15 1:75`"
      - "Rien : le compilateur ne sait pas quel constructeur appeler pour `b`."
    reponse: 1
    explication: "Le compilateur choisit le constructeur d'après le nombre et le type des arguments : aucun argument pour `a`, un `int` pour `b` et deux `int` pour `c`. Les deux derniers constructeurs ramènent les secondes entre 0 et 59 par une division entière et un modulo : 135 s donnent 2 min 15 s, et 1 min 75 s donnent aussi 2 min 15 s."
    revoir: "premiere-classe-l-exemple-d-un-article"
    page: "/docs/modules/module-4"
  - partie: "Partie C - Lecture de code"
    question: "Qu'affiche ce programme ?"
    code: |
      #include <iostream>

      template <typename T>
      T milieu(T a, T b) {
          return (a + b) / 2;
      }

      int main() {
          std::cout << milieu(7, 10) << ' '
                    << milieu(7.0, 10.0) << ' '
                    << milieu<double>(7, 10) << '\n';
          return 0;
      }
    choix:
      - "`8.5 8.5 8.5`"
      - "`8 8.5 8.5`"
      - "`8 8.5 8`"
      - "Rien : l'appel `milieu<double>(7, 10)` ne compile pas, car 7 et 10 sont des `int`."
    reponse: 2
    explication: "Sans indication, le compilateur déduit `T` du type des arguments : `int` pour `milieu(7, 10)`, d'où une division entière (17 / 2 donne 8), et `double` pour `milieu(7.0, 10.0)`. Avec `milieu<double>(7, 10)`, le type est imposé : les deux entiers sont convertis en `double`, et le résultat vaut 8.5."
    revoir: "patrons-de-fonctions-et-de-classes"
    page: "/docs/modules/module-5"
  - partie: "Partie D - Choix du code"
    question: "Dans un logiciel de caisse, le prix d'un article taxes comprises sert à plusieurs endroits : on l'affiche, on l'ajoute au total de la facture et on l'écrit dans le journal des ventes. Quelle fonction convient le mieux ?"
    choix_code: true
    choix:
      - |
        double prixTaxesComprises(double prix) {
            return prix * 1.14975;
        }
      - |
        void prixTaxesComprises(double prix) {
            std::cout << prix * 1.14975 << '\n';
        }
      - |
        double resultat = 0.0;

        void prixTaxesComprises(double prix) {
            resultat = prix * 1.14975;
        }
      - |
        double prixTaxesComprises() {
            double prix = 0.0;
            std::cin >> prix;
            return prix * 1.14975;
        }
    reponse: 1
    explication: "Une fonction qui **renvoie** son résultat laisse l'appelant décider de ce qu'il en fait : `total += prixTaxesComprises(p);`, l'affichage et l'écriture dans le journal utilisent la même fonction. (B) affiche le prix, mais ne le transmet pas : impossible de l'ajouter au total ou de l'écrire dans le journal. (C) fonctionne, mais passe par une variable globale que toute partie du programme peut modifier, et chaque appel écrase le résultat précédent. (D) lit le prix au clavier : la fonction ne peut pas servir pour un prix déjà connu, comme celui d'un article de la facture."
    revoir: "definition-et-valeur-de-retour"
    page: "/docs/modules/module-3"
  - partie: "Partie D - Choix du code"
    question: "Le `std::map<std::string, int> stock` associe le nom de chaque produit à sa quantité en stock. Quel fragment affiche la quantité de kiwis si ce produit existe, et « Produit inconnu » sinon, sans modifier `stock` ?"
    choix_code: true
    choix:
      - |
        if (stock["kiwi"] != 0) {
            std::cout << stock["kiwi"] << '\n';
        } else {
            std::cout << "Produit inconnu\n";
        }
      - |
        auto it = stock.find("kiwi");
        if (it->first == "kiwi") {
            std::cout << it->second << '\n';
        } else {
            std::cout << "Produit inconnu\n";
        }
      - |
        auto it = stock.find("kiwi");
        if (it != stock.end()) {
            std::cout << it->second << '\n';
        } else {
            std::cout << "Produit inconnu\n";
        }
      - |
        if (stock.find("kiwi")) {
            std::cout << stock.find("kiwi")->second << '\n';
        } else {
            std::cout << "Produit inconnu\n";
        }
    reponse: 3
    explication: "La méthode `find()` cherche une clé sans modifier le `map` : elle renvoie un itérateur vers l'élément trouvé, ou `end()` si la clé est absente, et `it->second` donne alors la quantité. (A) modifie `stock` : l'opérateur `[]` ajoute l'entrée « kiwi », avec la quantité 0, lorsque la clé est absente ; de plus, un produit dont le stock est épuisé serait déclaré inconnu. (B) déréférence `end()` lorsque la clé est absente, ce qu'il ne faut jamais faire : le comportement du programme est alors imprévisible. (D) ne compile pas : un itérateur ne s'utilise pas comme une condition, il doit être comparé à `end()`."
    revoir: "associer-des-cles-a-des-valeurs-avec-std-map"
    page: "/docs/modules/module-4/module-4-annexe"
  - partie: "Partie D - Choix du code"
    contexte: |
      Un gestionnaire de mises à jour compare des numéros de version, comme 2.4 et 2.5 :
    code: |
      class Version {
      private:
          int majeur;
          int mineur;

      public:
          Version(int ma, int mi) : majeur(ma), mineur(mi) {}
      };
    question: "Deux versions sont égales lorsque leurs numéros majeur et mineur sont égaux. Quelle méthode, ajoutée à la classe, permet d'écrire `if (installee == requise)` pour deux objets `Version` distincts ?"
    choix_code: true
    choix:
      - |
        bool operator==(const Version& autre) const {
            return this == &autre;
        }
      - |
        bool operator==(const Version& autre) const {
            return majeur == autre.majeur && mineur == autre.mineur;
        }
      - |
        bool operator==(const Version& a, const Version& b) const {
            return a.majeur == b.majeur && a.mineur == b.mineur;
        }
      - |
        bool estEgale(const Version& autre) const {
            return majeur == autre.majeur && mineur == autre.mineur;
        }
    reponse: 2
    explication: "Une méthode `operator==` donne un sens à `==` pour la classe : `installee == requise` équivaut à `installee.operator==(requise)`. L'objet de gauche est l'objet courant, et `autre` désigne celui de droite : comparer leurs attributs compare leurs **valeurs**. (A) compare les adresses des deux objets : il vérifie s'il s'agit du **même** objet, et deux objets distincts portant les mêmes numéros seraient déclarés différents. (C) ne compile pas : une méthode reçoit déjà l'opérande de gauche, l'objet courant, et `operator==` n'accepte donc qu'un seul paramètre. (D) compare correctement les numéros, mais il faut alors écrire `installee.estEgale(requise)` : l'expression `installee == requise` ne compile pas."
    revoir: "principes-de-base"
    page: "/docs/modules/module-4"
  - partie: "Partie D - Choix du code"
    question: "La fonction `void compresser(const std::string& dossier)` compresse un dossier de photos. On veut la lancer en arrière-plan sur le dossier « photos », pendant que `main()` affiche une barre de progression avec `afficherProgression()`, puis attendre la fin de la compression. Quel fragment convient ?"
    choix_code: true
    choix:
      - |
        std::thread t(compresser("photos"));
        afficherProgression();
        t.join();
      - |
        compresser("photos");
        std::thread t(afficherProgression);
        t.join();
      - |
        std::thread t("photos", compresser);
        afficherProgression();
        t.join();
      - |
        std::thread t(compresser, "photos");
        afficherProgression();
        t.join();
    reponse: 4
    explication: "Le constructeur de `std::thread` reçoit la fonction à exécuter, suivie de ses arguments : `compresser` s'exécute alors dans un nouveau thread, pendant que `main()` affiche la progression, puis `join()` attend la fin de la compression. (A) appelle `compresser(\"photos\")` immédiatement, dans `main()`, et tente de créer un thread à partir de son résultat, de type `void` : le fragment ne compile pas. (B) compresse d'abord tout le dossier, puis affiche la progression : il n'y a plus rien à suivre. (C) ne compile pas : la fonction doit précéder ses arguments."
    revoir: "approche-moderne-std-thread"
    page: "/docs/modules/module-5"
  - partie: "Partie D - Choix du code"
    contexte: |
      Une application de cartographie affiche des points d'intérêt. La classe de base affiche les informations communes à tous les points :
    code: |
      class PointInteret {
      private:
          std::string nom;

      public:
          explicit PointInteret(const std::string& n) : nom(n) {}
          virtual ~PointInteret() = default;

          virtual void afficher() const {
              std::cout << "Lieu : " << nom << '\n';
          }
      };
    question: "La classe dérivée `Restaurant` ajoute un attribut `cuisine`. Sa méthode `afficher()` doit afficher les informations communes, puis le type de cuisine. Quelle redéfinition convient ?"
    choix_code: true
    choix:
      - |
        void afficher() const override {
            afficher();
            std::cout << "Cuisine : " << cuisine << '\n';
        }
      - |
        void afficher() const override {
            std::cout << "Lieu : " << nom << '\n';
            std::cout << "Cuisine : " << cuisine << '\n';
        }
      - |
        void afficher() const override {
            PointInteret::afficher();
            std::cout << "Cuisine : " << cuisine << '\n';
        }
      - |
        void afficher() const override {
            std::cout << "Cuisine : " << cuisine << '\n';
            PointInteret::afficher();
        }
    reponse: 3
    explication: "L'opérateur de résolution de portée permet d'appeler explicitement la version de la classe de base, `PointInteret::afficher()`, depuis la redéfinition : on réutilise son code au lieu de le recopier. (A) appelle `afficher()` sur le même objet, c'est-à-dire la redéfinition elle-même : la fonction s'appelle sans fin. (B) ne compile pas, car `nom` est privé dans `PointInteret`. (D) affiche le type de cuisine avant les informations communes, contrairement à ce qui est demandé."
    revoir: "exemple-de-deux-classes-de-base"
    page: "/docs/modules/module-4"
---

# Examen final

L'examen final compte pour 20 % de la note du cours. Il porte sur l'ensemble des modules et se passe après la remise du projet : la [feuille de route]({{< relref "/docs/a-propos/feuille-de-route" >}}) le prévoit à la semaine 15. Ici, vous trouverez quelques conseils ainsi qu'un examen d'entraînement pour vous préparer.

## Un examen surveillé

L’examen final se déroule **à distance, sous télésurveillance**. Il est réalisé sur la plateforme Web sécurisée. Pendant l’examen, le système enregistre votre image et votre voix, votre environnement ainsi que l’activité de votre écran afin d’assurer le respect des conditions d’examen. **Votre consentement à la télésurveillance est obligatoire** pour pouvoir passer l’examen.

En pratique :

- Vous recevez un avis de convocation **quatre semaines avant l'examen**. Il précise les dates et contient l'information utile pour vous préparer.
- L'examen est offert pendant une **période de disponibilité de quelques jours**. Sauf exception, vous choisissez le moment qui vous convient à l'intérieur de cette période.
- Préparez une **pièce d'identité officielle avec photo**, délivrée par un gouvernement (par exemple, un permis de conduire). Au moment de l'examen, vous devrez déclarer que vous êtes bien la personne autorisée à le faire.
- Préparation à l’examen : Vous devez être en mesure de lire, de comprendre et d’analyser du code C++, ainsi que de maîtriser les concepts abordés dans le cours.
- Au besoin, vous pouvez reporter la date de l'examen dans votre portail MaTÉLUQ ; des exceptions s'appliquent.
- Vérifiez votre ordinateur à l'avance, à l'aide de la page [Matériel informatique recommandé](https://www.teluq.ca/communaute/zone-etudiante/materiel-informatique-recommande) de la TÉLUQ.

{{< boite type="attention" titre="Matériel autorisé : ni IA ni documentation" >}}
L’utilisation d’outils d’intelligence artificielle et la consultation de documentation **ne sont pas autorisées** pendant l’examen.
{{< /boite >}}

Pour tous les détails, consultez la page [Évaluations](https://www.teluq.ca/services/evaluations) de l'Université TÉLUQ.

{{< boite type="important" titre="Ce qui vous attend" >}}
L'examen dure **3 heures** et compte **20 questions à choix multiple**, réparties en quatre parties de cinq questions : conception à partir d'un code, mise en situation de conception, lecture de code et choix du code. Chaque question n'a qu'une seule bonne réponse.
{{< /boite >}}

## Vous préparer à l'examen

- **Relisez le cours, module par module.** Commencez par l'encadré « Objectifs d'apprentissage » et terminez par la synthèse finale. Pour chaque objectif, demandez-vous si vous pourriez l'expliquer à une autre personne, exemple à l'appui.
- **Refaites les questionnaires d'autoévaluation** des modules [1]({{< relref "/docs/modules/module-1/autoevaluation" >}}), [2]({{< relref "/docs/modules/module-2/autoevaluation" >}}), [3]({{< relref "/docs/modules/module-3/autoevaluation" >}}), [4]({{< relref "/docs/modules/module-4/autoevaluation" >}}) et [5]({{< relref "/docs/modules/module-5/autoevaluation" >}}), puis relisez les sections indiquées sous les questions manquées.
- **Revoyez vos travaux pratiques** et la rétroaction reçue : les notions qu'ils exercent (classes, héritage, polymorphisme, conteneurs, fonctions et tableaux) sont au cœur de l'examen.
- **Lisez du code et prédisez son résultat.** Pour les questions de lecture de code, suivez l'exécution pas à pas en notant la valeur des variables, comme le montre le module 2. Compilez ensuite les exemples du cours pour vérifier vos prédictions.
- **Justifiez vos choix de conception.** Devant une situation, demandez-vous s'il s'agit d'une relation « est un » ou « a un », si les données sont bien protégées et si l'ajout d'un nouveau cas obligerait à modifier le code existant. Dans les questions de conception, plusieurs propositions peuvent fonctionner : la bonne réponse est la plus juste du point de vue orienté objet.
- **Faites l'examen d'entraînement ci-dessous** dans des conditions proches de celles de l'examen : d'une traite, sans compiler le code. Lisez ensuite chaque explication, même pour les questions réussies.

## Examen d'entraînement

Cet examen factice reprend la structure de l'examen final : 20 questions à choix multiple, en quatre parties. Il n'est pas noté. Choisissez une réponse pour chaque question : la bonne réponse et une explication s'affichent aussitôt, avec un lien vers la section du cours à revoir. Vos réponses ne sont ni enregistrées ni transmises. Les questions de l'examen final sont différentes, mais de même nature.

| Partie | Questions | Ce qui est demandé |
|---|---|---|
| A - Conception à partir d'un code | 1 à 5 | À partir d'un code et d'un contexte, choisir la conception, l'approche ou le concept à utiliser. |
| B - Mise en situation de conception | 6 à 10 | À partir d'un contexte, sans code, choisir l'organisation des classes. |
| C - Lecture de code | 11 à 15 | Déterminer ce que fait ou affiche un programme. |
| D - Choix du code | 16 à 20 | À partir d'un besoin, choisir le code qui y répond le mieux. |

{{< qcm bouton="Recommencer l'examen d'entraînement" >}}
