---
title: "Module 5 : questionnaire d'autoévaluation"
linkTitle: "Autoévaluation"
weight: 90
bookToC: false
# Questions affichées par le shortcode « qcm » (layouts/shortcodes/qcm.html).
# reponse : numéro du bon choix (1 = premier) ; revoir : identifiant de la section du module à revoir.
qcm:
  - question: "Une application continue de répondre à l'utilisateur pendant qu'elle télécharge un fichier. De quoi s'agit-il surtout ?"
    choix:
      - "D'un calcul de type SIMD."
      - "D'un système distribué."
      - "De tâches concurrentes."
      - "D'un programme strictement séquentiel."
    reponse: 3
    explication: "La concurrence désigne la progression de plusieurs tâches pendant une même période, même si elles s'alternent sur un seul cœur. Calculer simultanément deux parties d'une image sur deux cœurs relèverait plutôt du parallélisme."
    revoir: "programmes-paralleles-et-ordinateurs-paralleles"
  - question: "Ajouter des cœurs à un ordinateur rend-il automatiquement un programme plus rapide ?"
    choix:
      - "Oui, le temps d'exécution diminue toujours."
      - "Non : le programme doit être conçu pour exploiter le parallélisme."
      - "Oui, mais seulement pour les programmes écrits en C++."
      - "Non, car un programme ne peut utiliser qu'un seul cœur."
    reponse: 2
    explication: "Pour en profiter, il faut découper le travail en tâches, synchroniser correctement ces tâches et limiter les parties strictement séquentielles."
    revoir: "interet-de-la-programmation-parallele"
  - question: "Dans la classification de Flynn, quel modèle correspond à une même instruction appliquée à plusieurs données, comme dans les calculs vectoriels ?"
    choix:
      - "SIMD"
      - "SISD"
      - "MISD"
      - "MIMD"
    reponse: 1
    explication: "SIMD : *Single Instruction, Multiple Data*. SISD est le modèle séquentiel classique ; MIMD, courant dans les systèmes multicœurs et les grappes, exécute plusieurs instructions sur plusieurs données."
    revoir: "programmes-paralleles-et-ordinateurs-paralleles"
  - question: "Qu'est-ce qu'un **système distribué** ?"
    choix:
      - "Un programme qui utilise plusieurs threads."
      - "Un serveur unique qui centralise toutes les ressources."
      - "Un processeur qui possède plusieurs cœurs."
      - "Un ensemble de composants autonomes reliés par un réseau, qui coopèrent et se présentent à l'utilisateur comme un système cohérent."
    reponse: 4
    explication: "Dans un système distribué, les ressources sont réparties entre plusieurs machines, services ou composants, parfois hétérogènes et éloignés."
    revoir: "definition-d-un-systeme-distribue"
  - question: "Quelle affirmation sur le modèle client-serveur et l'intergiciel (*middleware*) est juste ?"
    choix:
      - "Ce sont deux modèles concurrents : il faut choisir l'un ou l'autre."
      - "Le modèle client-serveur décrit une interaction (un client demande un service à un serveur) ; l'intergiciel est une couche logicielle qui facilite la communication."
      - "L'intergiciel est le nom du serveur dans le modèle client-serveur."
      - "Le modèle client-serveur ne fonctionne que sur une seule machine."
    reponse: 2
    explication: "Les deux notions sont complémentaires : une application client-serveur peut s'appuyer sur un intergiciel pour communiquer."
    revoir: "environnements-distribues-et-intergiciels"
  - question: "Quelle est la différence entre un processus et un thread ?"
    choix:
      - "Un processus possède son propre espace mémoire ; les threads d'un même processus partagent la même mémoire."
      - "Chaque thread possède son propre espace mémoire, séparé de celui des autres threads."
      - "Il n'y a aucune différence : ce sont deux noms pour la même notion."
      - "Un processus s'exécute toujours plus vite qu'un thread."
    reponse: 1
    explication: "Un thread est un fil d'exécution à l'intérieur d'un processus. Comme les threads partagent la mémoire, leurs accès aux données communes doivent être synchronisés."
    revoir: "processus-et-threads"
  - question: "À quoi sert l'appel `join()` sur un objet `std::thread` ?"
    choix:
      - "À démarrer le thread."
      - "À fusionner deux threads en un seul."
      - "À attendre la fin du thread avant de poursuivre."
      - "À verrouiller un mutex."
    reponse: 3
    explication: "Le thread démarre dès sa création ; `join()` attend sa fin. Les appels à `join()` garantissent ici que les threads sont terminés avant la sortie de `main()`."
    revoir: "approche-moderne-std-thread"
  - question: "Deux threads affichent chacun un message. Dans quel ordre les messages apparaissent-ils ?"
    choix:
      - "Toujours dans l'ordre de création des threads."
      - "Toujours dans l'ordre inverse de création."
      - "Dans l'ordre alphabétique des messages."
      - "L'ordre peut varier d'une exécution à l'autre, et les caractères peuvent même s'entrelacer."
    reponse: 4
    explication: "L'ordonnancement des threads n'est pas garanti : ne supposez jamais que le premier thread créé affichera son message en premier."
    revoir: "approche-moderne-std-thread"
  - question: "Deux threads incrémentent mille fois la même variable `compteur`, sans aucune synchronisation. Que risque-t-on ?"
    choix:
      - "Rien : le résultat est toujours 2000."
      - "Une course aux données (*data race*) : c'est un comportement indéfini en C++."
      - "Une erreur de compilation."
      - "Le compilateur ajoute automatiquement un mutex."
    reponse: 2
    explication: "Quand plusieurs threads modifient la même variable sans synchronisation, le comportement est indéfini, et pas seulement un résultat qui varie. Un mutex protège la section critique."
    revoir: "mutex-et-zones-critiques"
  - question: "Que fait l'instruction `std::lock_guard<std::mutex> garde(verrou);` ?"
    choix:
      - "Elle verrouille le mutex à sa construction et le libère automatiquement à la fin du bloc."
      - "Elle crée un nouveau thread nommé `garde`."
      - "Elle attend la fin de tous les threads."
      - "Elle libère le mutex `verrou` immédiatement."
    reponse: 1
    explication: "Le verrou est libéré automatiquement à la sortie du bloc, même en cas de sortie anticipée : on ne risque pas d'oublier de le déverrouiller."
    revoir: "mutex-et-zones-critiques"
  - question: "Quel type de socket utilise-t-on habituellement avec TCP pour transporter un flux ordonné et fiable d'octets ?"
    choix:
      - "`SOCK_DGRAM`"
      - "`AF_UNIX`"
      - "`SOCK_STREAM`"
      - "`AF_INET6`"
    reponse: 3
    explication: "`SOCK_STREAM` est habituellement associé à TCP, `SOCK_DGRAM` à UDP (un datagramme par envoi). `AF_UNIX` et `AF_INET6` sont des **domaines** de socket : communication locale et IPv6."
    revoir: "modes-de-communication-tcp-et-udp"
  - question: "Que permet le patron de fonction suivant ?"
    code: |
      template <typename T>
      T maximum(T a, T b) {
          return (a > b) ? a : b;
      }
    choix:
      - "Il ne fonctionne qu'avec des valeurs de type `int`."
      - "Il crée un thread pour comparer deux valeurs."
      - "Il surcharge l'opérateur `>`."
      - "Il fournit une seule définition, utilisable avec plusieurs types (`int`, `double`…), dont le type concret est déterminé à la compilation."
    reponse: 4
    explication: "Un patron (*template*) définit un modèle générique : `maximum(3, 7)` et `maximum(2.5, 1.5)` utilisent la même définition, tout en conservant la vérification des types par le compilateur."
    revoir: "patrons-de-fonctions-et-de-classes"
  - question: "Dans un serveur TCP, quelle primitive attend la connexion d'un client, puis l'accepte ?"
    choix:
      - "`connect()`"
      - "`accept()`"
      - "`send()`"
      - "`socket()`"
    reponse: 2
    explication: "Le serveur enchaîne `socket()`, `bind()`, `listen()`, puis `accept()`. C'est le client qui appelle `connect()` pour joindre le serveur."
    revoir: "annexe-e-client-et-serveur-sequence-conceptuelle"
---

# Module 5 : questionnaire d'autoévaluation

Ce questionnaire n'est pas noté. Il vous permet de vérifier, à votre rythme, que les notions du module 5 sont bien comprises. Choisissez une réponse pour chaque question : la bonne réponse et une explication s'affichent aussitôt, avec un lien vers la section du module à revoir au besoin. Vos réponses ne sont ni enregistrées ni transmises, et vous pouvez recommencer autant de fois que vous le souhaitez.

{{< qcm >}}
