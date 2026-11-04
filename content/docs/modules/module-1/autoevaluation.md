---
title: "Module 1 : questionnaire d'autoévaluation"
linkTitle: "Autoévaluation"
weight: 90
bookToC: false
# Questions affichées par le shortcode « qcm » (layouts/shortcodes/qcm.html).
# reponse : numéro du bon choix (1 = premier) ; revoir : identifiant de la section du module à revoir.
qcm:
  - question: "Dans un logiciel de gestion de stock, `article1` est créé à partir de la classe `Article`. Quelle affirmation est juste ?"
    choix:
      - "`Article` et `article1` sont deux noms pour la même chose."
      - "La classe `Article` contient les valeurs de tous les articles du magasin."
      - "`article1` est une instance de `Article` : il possède ses propres valeurs pour les attributs décrits par la classe."
      - "`article1` décrit la structure commune à tous les articles."
    reponse: 3
    explication: "La classe décrit la structure et le comportement communs ; chaque objet, ou instance, possède ses propres valeurs d'attributs (référence, prix, quantité…). Ne confondez pas objet et classe !"
    revoir: "instanciation"
  - question: "Qu'est-ce qui représente l'**état** d'un objet ?"
    choix:
      - "Les valeurs de ses attributs (ses données)."
      - "Ses méthodes."
      - "Le nom de sa classe."
      - "Les messages qu'il envoie aux autres objets."
    reponse: 1
    explication: "Un objet est caractérisé par un état et un comportement : son état est représenté par ses données (attributs), son comportement par ses opérations (méthodes)."
    revoir: "etat-et-comportement-d-un-objet"
  - question: "Comment appelle-t-on le mécanisme par lequel l'exécution d'un programme produit un objet à partir d'une classe ?"
    choix:
      - "L'encapsulation."
      - "L'héritage."
      - "L'abstraction."
      - "L'instanciation."
    reponse: 4
    explication: "L'instanciation crée un objet, appelé instance, en suivant le « plan de construction » défini par sa classe."
    revoir: "instanciation"
  - question: "En quoi consiste l'**abstraction** ?"
    choix:
      - "À cacher les attributs d'une classe avec le mot clé `private`."
      - "À retenir les caractéristiques pertinentes d'un élément sans en considérer tous les détails."
      - "À créer plusieurs objets à partir d'une même classe."
      - "À donner le même nom à plusieurs fonctions."
    reponse: 2
    explication: "L'abstraction retient ce qui est utile au problème. Un objet est à la fois une abstraction de données et une abstraction de code. Cacher les détails d'implémentation relève plutôt de l'encapsulation."
    revoir: "l-abstraction"
  - question: "Un compte bancaire garde son solde privé et offre les méthodes `deposer(montant)` et `retirer(montant)`. Quel est le principal intérêt de cette conception ?"
    choix:
      - "Le programme s'exécute plus rapidement."
      - "On peut créer davantage de comptes."
      - "Les méthodes peuvent vérifier chaque opération (montant positif, fonds suffisants), ce qui préserve la cohérence de l'objet."
      - "Toutes les autres classes peuvent modifier le solde directement."
    reponse: 3
    explication: "C'est l'encapsulation : l'interface publique offre des services, tandis que l'implémentation (le solde) reste protégée. L'objet reste cohérent, car aucune modification ne contourne les vérifications."
    revoir: "encapsulation-des-donnees"
  - question: "En C++, quel est le mode d'accès par défaut des membres d'une `class` ?"
    choix:
      - "`public`"
      - "`private`"
      - "`protected`"
      - "Il n'y en a pas : il faut toujours le préciser."
    reponse: 2
    explication: "Dans une `class`, l'accès par défaut est `private` ; dans une `struct`, il est `public`."
    revoir: "controle-d-acces-en-c"
  - question: "Que fait l'instruction C++ `compte.deposer(100);` ?"
    choix:
      - "Elle envoie un message à l'objet `compte` : exécuter sa méthode `deposer` avec l'argument `100`."
      - "Elle crée un nouvel objet nommé `compte`."
      - "Elle déclare une classe nommée `deposer`."
      - "Elle modifie directement l'attribut solde, sans passer par une méthode."
    reponse: 1
    explication: "L'appel d'une méthode sur un objet est la forme C++ courante de l'envoi de message : destinataire (`compte`), méthode à exécuter (`deposer`) et arguments (`100`)."
    revoir: "communication-entre-objets"
  - question: "Lequel de ces cas se modélise le mieux par une relation d'**héritage** ?"
    choix:
      - "Une maison et ses portes."
      - "Une voiture et son moteur."
      - "Une commande et ses produits."
      - "Un rectangle et un polygone."
    reponse: 4
    explication: "L'héritage convient à la relation « est un » : un rectangle **est un** polygone. Une maison **a** des portes : c'est une relation client (« a »), pas un héritage."
    revoir: "heritage-et-relations-entre-classes"
  - question: "Qu'est-ce que l'**héritage multiple** ?"
    choix:
      - "Plusieurs classes qui dérivent d'une même classe de base."
      - "Une classe qui dérive directement de plusieurs classes de base."
      - "Une hiérarchie de plusieurs niveaux, par exemple `Carre`, qui hérite de `Rectangle`, qui hérite de `Polygone`."
      - "Plusieurs objets créés à partir d'une même classe."
    reponse: 2
    explication: "L'héritage est multiple lorsqu'une classe a plusieurs classes de base **directes**. Une hiérarchie à plusieurs niveaux reste de l'héritage simple : la relation est simplement transitive."
    revoir: "heritage-et-relations-entre-classes"
  - question: "Une application graphique demande à chaque figure d'une collection de se dessiner, et chaque type de figure le fait à sa manière. Quel concept est illustré ?"
    choix:
      - "L'encapsulation."
      - "L'instanciation."
      - "Le polymorphisme."
      - "La modularité."
    reponse: 3
    explication: "Le polymorphisme permet à des objets différents de répondre de manière différente au même message (« dessine-toi »)."
    revoir: "le-polymorphisme"
  - question: "Que permet la **surcharge** ?"
    choix:
      - "Définir des fonctions ou des opérateurs portant le même nom, distingués par leurs paramètres."
      - "Écrire des fonctions ou des classes paramétrées par des types."
      - "Hériter de plusieurs classes à la fois."
      - "Masquer les attributs d'une classe."
    reponse: 1
    explication: "La surcharge réutilise un même nom pour des fonctions ou des opérateurs selon les règles du langage. Les fonctions et classes paramétrées par des types relèvent de la généricité (les `templates`)."
    revoir: "surcharge-et-genericite-apercu"
  - question: "Quelle qualité logicielle désigne la capacité d'un logiciel à réagir de manière appropriée à des conditions anormales ?"
    choix:
      - "La portabilité."
      - "L'extensibilité."
      - "La réutilisabilité."
      - "La robustesse."
    reponse: 4
    explication: "La robustesse est la capacité à réagir correctement aux conditions anormales. La portabilité concerne le passage d'un environnement à un autre, l'extensibilité l'adaptation aux changements de spécifications."
    revoir: "pourquoi-representer-un-probleme-par-des-objets"
---

# Module 1 : questionnaire d'autoévaluation

Ce questionnaire n'est pas noté. Il vous permet de vérifier, à votre rythme, que les notions du module 1 sont bien comprises. Choisissez une réponse pour chaque question : la bonne réponse et une explication s'affichent aussitôt, avec un lien vers la section du module à revoir au besoin. Vos réponses ne sont ni enregistrées ni transmises, et vous pouvez recommencer autant de fois que vous le souhaitez.

{{< qcm >}}
