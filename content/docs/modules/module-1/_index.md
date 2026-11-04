---
title: "Module 1 : Introduction à l'approche orientée objet"
linkTitle: "Module 1"
description: "INF 2005 – Programmation orientée objet avec C++"
weight: 10
bookCollapseSection: true
---

{{< figure-cours src="figures/banner_1.png" alt="Bannière du cours INF 2005 – Programmation orientée objet avec C++" largeur="100%" >}}

# Module 1 : Introduction à l'approche orientée objet

{{< boite type="objectif" >}}
À la fin de ce texte, l'étudiante ou l'étudiant devrait être capable de :

- expliquer les principes généraux et l’intérêt de l’approche orientée objet ;
- distinguer les notions d’objet, de classe et d’instance ;
- identifier les attributs, les méthodes et les responsabilités d’une classe ;
- expliquer l’abstraction, l’encapsulation et les règles de contrôle d’accès ;
- distinguer les relations entre objets, l’héritage et le polymorphisme ;
- analyser une petite étude de cas de conception orientée objet.

{{< /boite >}}

{{< boite type="contenu" >}}
**Contenu du module :** comprendre les fondements de l'approche orientée objet et savoir distinguer les notions d'objet, de classe, d'encapsulation, d'abstraction, d'héritage et de polymorphisme.
{{< /boite >}}

## Table des matières {#table-des-matieres}

- [1 Introduction à la programmation orientée objet](#introduction-a-la-programmation-orientee-objet)
- [2 Objets, classes et instances](#objets-classes-et-instances)
  - [2.1 Pourquoi représenter un problème par des objets ?](#pourquoi-representer-un-probleme-par-des-objets)
  - [2.2 Conception orientée objet](#conception-orientee-objet)
  - [2.3 État et comportement d’un objet](#etat-et-comportement-d-un-objet)
  - [2.4 La notion de classe](#la-notion-de-classe)
    - [2.4.1 Représentation et exemple de classe](#representation-et-exemple-de-classe)
    - [2.4.2 Détermination des classes](#determination-des-classes)
    - [2.4.3 Instanciation](#instanciation)
- [3 Abstraction, encapsulation et interactions](#abstraction-encapsulation-et-interactions)
  - [3.1 L’abstraction](#l-abstraction)
  - [3.2 Encapsulation des données](#encapsulation-des-donnees)
  - [3.3 Contrôle d’accès en C++](#controle-d-acces-en-c)
  - [3.4 Comportement et services des objets](#comportement-et-services-des-objets)
  - [3.5 Communication entre objets](#communication-entre-objets)
- [4 Modularité et réutilisabilité](#modularite-et-reutilisabilite)
  - [4.1 La modularité](#la-modularite)
  - [4.2 La réutilisabilité](#la-reutilisabilite)
  - [4.3 Surcharge et généricité : aperçu](#surcharge-et-genericite-apercu)
- [5 Relations entre classes, héritage et polymorphisme](#relations-entre-classes-heritage-et-polymorphisme)
  - [5.1 Héritage et relations entre classes](#heritage-et-relations-entre-classes)
  - [5.2 Le polymorphisme](#le-polymorphisme)
- [6 Les langages orientés objet et la place de C++](#les-langages-orientes-objet-et-la-place-de-c)
- [7 Conception par objets : étude de cas](#conception-par-objets-etude-de-cas)

## 1. Introduction à la programmation orientée objet {#introduction-a-la-programmation-orientee-objet}

Lorsqu'on commence à programmer, les premiers programmes reposent généralement sur des variables, des conditions, des boucles et des fonctions. Ces outils permettent de résoudre de nombreux problèmes. À mesure qu'un programme grandit, il devient cependant nécessaire d'organiser les données et les opérations qui leur sont associées afin de faciliter sa compréhension et son évolution.

Prenons l'exemple d'une application de gestion des stocks d'un magasin. Elle doit représenter des articles, conserver leur prix et leur quantité disponible, puis permettre l'ajout ou le retrait d'articles. Si les informations et les traitements sont dispersés dans le programme, une modification peut entraîner des changements à plusieurs endroits. La programmation orientée objet (POO) propose de regrouper les informations et les opérations associées au sein d'entités appelées *objets*.

La POO constitue une manière d'organiser un programme et de répartir les responsabilités entre ses composantes. Elle peut favoriser la modularité, la maintenance et la réutilisation du code, à condition que les classes et leurs interactions soient bien conçues. Le langage C++, utilisé dans ce cours, prend en charge cette approche tout en permettant également la programmation procédurale et générique.

Ce premier module vise à établir les fondements conceptuels de la POO : objets, classes, instances, abstraction, encapsulation, relations entre classes, héritage et polymorphisme. Les exemples servent surtout à comprendre ces notions; les modules suivants permettront d'en approfondir la mise en œuvre en C++.

## 2. Objets, classes et instances {#objets-classes-et-instances}

### 2.1. Pourquoi représenter un problème par des objets ? {#pourquoi-representer-un-probleme-par-des-objets}

Un objet logiciel représente une entité pertinente pour l’application, qu’elle soit concrète ou abstraite. Il ne reproduit pas nécessairement tous les détails d’un objet du monde réel : il retient les informations et les comportements utiles au problème considéré.

La conception par objets trouve ses fondements dans la réflexion menée autour de la vie du logiciel. D'une part, le développement de logiciels de plus en plus importants nécessite l'utilisation de règles permettant d'assurer une certaine qualité de réalisation. D'autre part, la réalisation d'un logiciel comporte plusieurs étapes, dont le développement ne constitue que la première partie. Elle est suivie dans la plupart des cas de l’étape de maintenance qui consiste à corriger le logiciel, à l’adapter et à le faire évoluer. La maintenance peut représenter une part importante de l’effort consacré à un logiciel.

La conception par objets s’inscrit dans une réflexion sur la qualité logicielle, à laquelle contribuent notamment les critères suivants :

- la validité, soit le fait qu'un logiciel effectue exactement les tâches pour lesquelles il a été conçu;
- l'extensibilité, soit la facilité d'adaptation des produits logiciels aux changements de spécifications;
- la réutilisabilité, soit la facilité des éléments logiciels à servir à la construction de plusieurs applications différentes;
- la portabilité, soit la facilité avec laquelle des produits logiciels peuvent être transférés d'un environnement logiciel ou matériel à un autre;
- la robustesse, soit la capacité des systèmes logiciels à réagir de manière appropriée à la présence de conditions anormales;
- la modularité, soit une architecture assez flexible pour intégrer des entités indépendantes : les modules.

Ces critères guideront la conception des classes que nous étudierons dans la suite du module. Nous reviendrons ensuite sur la modularité et la réutilisabilité.

### 2.2. Conception orientée objet {#conception-orientee-objet}

Une démarche de conception orientée objet consiste à identifier les entités pertinentes d’un problème, puis à définir leurs données, leurs comportements et leurs interactions. Elle complète les approches centrées sur les traitements plutôt qu’elle ne les remplace dans toutes les situations.

Dans cette optique, voici une définition proposée par Bertrand Meyer[^1] : « La conception par objets est la méthode qui conduit à des architectures logicielles fondées sur les OBJETS que tout système ou sous-système manipule. » Il ajoutait : « Ne commencez pas par demander ce que fait le système, demandez À QUOI il le fait! »

La spécification d’un système va donc maintenant s’axer principalement sur la détermination des objets manipulés. Le concepteur précise ensuite les responsabilités et les interactions des objets, sans perdre de vue les fonctionnalités attendues du système. Examinons maintenant la structure et le comportement d’un objet.

### 2.3. État et comportement d’un objet {#etat-et-comportement-d-un-objet}

Dans la réalité, physique ou abstraite, les objets sont présents partout. Le modèle du monde est en effet constitué d’objets : étudiants, employés, avions, chèques, etc. Les objets logiciels peuvent représenter certains aspects de ces entités, mais aussi des notions abstraites propres au logiciel. Dans un système graphique, les objets sont les points, les lignes, les polygones, les cercles, etc.; dans un système de paie, les objets sont les employés, les chèques, les échelles de salaire et ainsi de suite. La conception par objets consiste à sélectionner les entités utiles au problème et à définir leurs responsabilités. Toutefois, les opérations à effectuer sur chacun requièrent un minimum de connaissances sur leur structure.

Un objet est caractérisé par un état et un comportement. Son état est représenté par des données, tandis que son comportement est défini par des opérations qui peuvent agir sur ces données. Les données constituent les attributs de l’objet, alors que les procédures sont des méthodes. De plus, l’objet est muni d’une interface qui spécifie les interactions qu’il peut avoir avec le monde extérieur.

La [figure 1](#fig-figure-07) illustre, d'une façon générale, le concept d’objet. L’interface présente les opérations que les autres parties du programme sont autorisées à utiliser. La protection des détails internes dépend des règles d’accès définies dans la classe. Une interface stable peut limiter les conséquences d’une modification de l’implémentation, sans garantir qu’aucune autre partie du programme ne sera touchée.

{{< figure-cours src="figures/figure_07.png" id="fig-figure-07" numero="1" legende="Concept d’objet." largeur="82%" >}}

### 2.4. La notion de classe {#la-notion-de-classe}

Comme nous l’avons déjà mentionné, un objet est caractérisé par sa structure et son comportement. Toutefois, nous pouvons regrouper tous les objets ayant la même structure et le même comportement dans une catégorie spécifique d’objets, appelée classe. Voyons comment représenter et déterminer une classe.

#### 2.4.1. Représentation et exemple de classe {#representation-et-exemple-de-classe}

Une classe est la description d’un ensemble d’objets ayant la même structure et le même comportement. Elle constitue une entité génératrice d’une famille d’objets dont elle définit la structure et le comportement par les propriétés relationnelles (ses attributs) et fonctionnelles (ses méthodes).

Autrement dit, chaque classe possède une double composante : une composante statique (les données) constituée de champs qui caractérisent l’état des objets pendant l’exécution du programme, et une composante dynamique (les procédures); celles-ci, aussi appelées méthodes, traduisent le comportement des objets appartenant à la classe en question et en manipulent les champs.

Une classe peut exposer une interface publique tout en conservant des détails d’implémentation internes. L’interface d’une classe constitue la partie accessible à son utilisateur. Plus précisément, elle fournit la spécification de la classe, en indiquant ses propriétés, en précisant l’ensemble de ses instances et en décrivant les moyens permettant d’utiliser les services qu'offre cette classe.

Quant au corps de la classe, il décrit son implémentation, c’est-à-dire la manière dont les traitements sont effectués. L’accès à la représentation interne dépend des niveaux de visibilité définis par la classe. Ses méthodes peuvent notamment modifier des attributs privés tout en vérifiant les règles de l’application. Pour illustrer notre propos, concevons un système permettant de gérer le stock d’un magasin. Dans ce cas, nous pouvons créer une classe d’articles avec, comme attributs, les champs suivants :

- Référence, qui désigne le numéro de référence de cet article;
- Désignation, représentée par un texte qui décrit l’article en question;
- PrixHT, indiquant le prix unitaire de l’article;
- Quantité, qui désigne le nombre d’articles disponibles dans le stock.

En outre, la définition de la classe doit être complétée par une liste de méthodes qui permettent de manipuler les champs mentionnés plus haut. Chaque méthode est définie par un nom, souvent appelé sélecteur, une liste de paramètres et un corps de fonction. Pour notre exemple, nous pouvons définir les méthodes suivantes :

- CalculerPrixTTC, qui calcule le prix toutes taxes comprises en ajoutant au prix hors taxes le montant des taxes applicables;
- CalculerPrixtransport, qui calcule le prix de transport de l’article en considérant que ce coût équivaut à un certain pourcentage, par exemple 5 % du coût avant taxe de l’article;
- Retirer, qui permet de retirer des articles du stock en soustrayant la valeur de son paramètre au champ Quantité;
- Ajouter, qui permet d’ajouter des articles au stock.

Voici un exemple d’une implémentation possible de la classe Article.

{{< boite type="code" >}}
```text
Classe Article
Champs : Référence, Désignation, PrixHT, Quantité
Méthodes :
CalculerPrixTTC() : retourner (1.15 * PrixHT)
CalculerPrixTransport() : retourner (0.05 * PrixHT)
Retirer(q) : si 0 <= q <= Quantité, Quantité = Quantité - q
Ajouter(q) : si q > 0, Quantité = Quantité + q
```
{{< /boite >}}

{{< boite type="remarque" >}}
Le taux de 15 % et les frais de transport de 5 % sont des valeurs choisies uniquement pour illustrer les calculs. Dans une application réelle, ces paramètres dépendraient des règles applicables et ne devraient pas nécessairement être fixés dans la classe.
{{< /boite >}}

{{< boite type="exemple" >}}
Pour deux articles du magasin, la classe `Article` décrit la structure commune, tandis que chaque objet possède ses propres valeurs de référence, de prix et de quantité. Les opérations `Ajouter` et `Retirer` permettent de modifier les quantités en respectant les contraintes prévues.
{{< /boite >}}

#### 2.4.2. Détermination des classes {#determination-des-classes}

Les programmeurs habitués à utiliser l’approche fonctionnelle doivent encore se demander comment trouver, déterminer les classes. Bien qu’il n’existe pas de méthode universelle permettant d’identifier les classes les plus appropriées à un problème donné, certaines techniques et certains principes de conception peuvent guider cette démarche. L’expérience contribue également à affiner ces choix.

Ainsi, lorsqu’un ensemble de classes est proposé pour résoudre un problème, nous pouvons les examiner selon des principes et critères de modularité. De cette analyse, nous pouvons déduire les classes qui peuvent être réutilisées pour nos besoins spécifiques. En effet, un bon environnement à objets offre un certain nombre de classes prédéfinies qui implémentent des abstractions importantes, et qu’on peut aller chercher pour éventuellement les réutiliser. C’est le cas des listes, de certains fichiers, des piles, des files, etc. Cela nous amène à la conclusion suivante : plus les techniques à objets se développent, plus le nombre et le niveau d’abstraction des composantes réutilisables augmentent. Ainsi, la réutilisation de certaines classes, dites classes de base, permet de résoudre en partie le problème de détermination de nouvelles classes. La question à se poser maintenant est la suivante : « Comment créer des classes à partir des spécifications du système à concevoir? »

Lorsque l’on conçoit un système avec des objets, une bonne façon de trouver les classes consiste à souligner les noms, lors de la lecture du document de spécification; pour ce qui est des méthodes fonctionnelles, on souligne surtout les verbes.

Par exemple, la phrase « Le radar doit contrôler la position et la vitesse des automobiles » conduirait un concepteur par objets à détecter deux classes : Radar et Automobile. Cette technique, d’ailleurs simpliste, ne donne que des résultats approximatifs. En effet, si elle est appliquée à la lettre, elle est susceptible de fournir trop de classes candidates. Dans notre exemple, il n’est pas évident que position et vitesse doivent servir à déterminer des classes.

La création de classes inutiles est une erreur typique de débutant. Il n’existe toutefois pas de méthode sûre pour éviter de telles erreurs. Le fil conducteur demeure la théorie des abstractions de données : une notion ne doit être établie comme classe que si elle décrit un ensemble d’objets caractérisés par des opérations intéressantes et par des propriétés significatives.

Ainsi, dans l’exemple précédent, la position des automobiles peut-elle être considérée comme une classe? Oui et non. S’il n’existe pas d’opération spécifique sur les positions, il vaut mieux considérer Position comme un attribut de la classe Automobile. Toutefois, si une position est une entité significative, avec des opérations qui lui sont associées (distance d’une autre position, erreur de mesure, conversion à un autre système de coordonnées), alors elle peut être définie comme une classe. Il en est de même pour la vitesse : si la vitesse d’une automobile a des propriétés utiles propres, elle peut être définie par une classe spécifique.

{{< boite type="important" >}}
Attention, ne confondez pas objet et classe!
{{< /boite >}}

Une classe définit un type; un objet en est une instance. En C++, une classe peut aussi comporter des membres statiques, associés à la classe plutôt qu’à chaque objet. Il convient donc de distinguer la définition d’un type et les objets qui en sont créés.

#### 2.4.3. Instanciation {#instanciation}

Le mécanisme par lequel l’exécution d’un programme produit un objet à partir d’une classe constitue l’instanciation. Par cette dernière, la définition d’une classe sert de modèle à la construction de ses représentants physiques, appelés instances. Une instance constitue un objet particulier créé en respectant les plans de construction de sa classe; cette dernière définit la structure et le comportement de l’instance. Par ailleurs, l’état d’une instance est caractérisé par les valeurs de ses attributs. De plus, un attribut (ou une méthode) associé à une classe sera défini pour toutes les instances de cette classe. La [figure 2](#fig-figure-10) illustre la création de deux instances de la classe Article.

Deux instances d’une même classe se distinguent par les valeurs de leurs attributs. Lorsque toutes les instances d’une classe possèdent les mêmes champs, ces derniers prennent des valeurs différentes, correspondant à la nature particulière de chacune de ces instances. Cela est illustré à la [figure 2](#fig-figure-10) où l’une des instances représente l’ensemble des pantalons et l’autre, l’ensemble des téléviseurs. Nous nous rendons compte que la structure de données décrite par les champs est dupliquée pour former la structure de chaque instance. Une telle structure est remplie avec les valeurs propres de l’objet représenté par chaque instance.

En C++, il faut porter attention à l’initialisation des attributs : un membre de type fondamental qui n’est pas initialisé ne possède pas nécessairement une valeur déterminée. On privilégie donc une initialisation explicite, notamment au moyen d’un constructeur ou d’une valeur initiale. Chaque objet possède un type défini par sa classe; la relation d’instanciation est illustrée à la [figure 2](#fig-figure-10).

{{< figure-cours src="figures/figure_10.png" id="fig-figure-10" numero="2" legende="Création de deux instances de la classe Article." largeur="82%" >}}

{{< boite type="exemple" >}}
Dans une expression C++ telle que `Article article1;`, `Article` désigne le type (la classe) et `article1` désigne un objet. Cette écriture suppose que la classe dispose d’un constructeur accessible sans argument; les constructeurs seront étudiés ultérieurement.
{{< /boite >}}

## 3. Abstraction, encapsulation et interactions {#abstraction-encapsulation-et-interactions}

### 3.1. L’abstraction {#l-abstraction}

Deux principes importants de la programmation orientée objet sont l’abstraction et l’encapsulation. Examinons d’abord l’abstraction; l’encapsulation sera développée dans la section suivante.

L’abstraction consiste à retenir les caractéristiques pertinentes d’un élément sans en considérer tous les détails. L'abstraction de code (ou abstraction procédurale) correspond donc à ignorer les détails d'une portion de code pour la voir comme un tout : il s'agit des procédures et des fonctions! L’abstraction de données permet de décrire un type par les propriétés et les opérations qui intéressent ses utilisateurs, indépendamment de certains détails de représentation.

Le modèle objet est une synthèse de ces deux types d'abstraction : un objet est à la fois une abstraction de données et une abstraction de code.

### 3.2. Encapsulation des données {#encapsulation-des-donnees}

L’encapsulation est le mécanisme par lequel le programmeur cache une partie de l’information pour préserver l’intégrité de l’objet. Ce faisant, il établit une séparation entre l’interface (publique) et l’implémentation (invisible). L’encapsulation de données est un arrangement de la structure d’un objet qui permet de réunir des données internes, les méthodes d’utilisation et de manipulation de telles données, ainsi que l’accès à ces données contrôlé par un filtre; la [figure 3](#fig-figure-01) illustre ce concept. Ainsi, l’encapsulation facilite la représentation et l’organisation des connaissances et des données, et influe sur l’usage ultérieur de l’objet.

L’encapsulation est aussi appelée dissimulation, en ce sens que l’accès à un ensemble défini de structures de données est limité à une liste de fonctions déclarées par le concepteur. Toute fonction qui n’est pas explicitement autorisée à accéder à la structure interne de l’objet provoquera une erreur.

En C++, les types fondamentaux tels que `int` et `double` ne sont pas des classes. L’encapsulation s’illustre plutôt avec une classe dont les données internes sont protégées et dont les méthodes publiques définissent les opérations permises.

{{< figure-cours src="figures/figure_01.png" id="fig-figure-01" numero="3" legende="Encapsulation de données." largeur="82%" >}}

L’encapsulation a pour principal objectif de masquer l’implémentation des structures au programmeur qui les utilise en fonction de leurs spécifications. Elle repose sur une séparation logique entre l’interface accessible et les détails de l’implémentation. En C++, ces deux aspects peuvent notamment être organisés dans des fichiers distincts, mais une telle séparation physique n’est pas obligatoire. Ainsi, la modélisation par objets dispose d’un schéma de représentation simple : l’objet en tant qu’encapsulation de données et de traitements, la classe en tant que type abstrait. Plus qu’une simple programmation dirigée par les données, la programmation par objets est une véritable programmation par abstraction de données.

{{< boite type="exemple" >}}
Un compte bancaire peut exposer les opérations `deposer(montant)` et `retirer(montant)`, tout en conservant le solde privé. La méthode de retrait vérifie alors que le montant est positif et que les fonds sont suffisants. L’objet reste cohérent sans donner un accès direct au solde.
{{< /boite >}}

### 3.3. Contrôle d’accès en C++ {#controle-d-acces-en-c}

Dans la définition d’une classe, nous avons vu que les accès aux attributs d’une classe sont les mêmes que ceux que l'on utilise pour accéder aux champs d’une structure. Les mots clés public, private et protected sont utilisés pour contrôler l’accès aux attributs et aux fonctions des classes; par défaut, le mode d’accès des classes est privé. Les membres privés sont accessibles aux fonctions membres et aux fonctions ou classes déclarées amies (`friend`), selon les règles de C++. Les membres publics peuvent être utilisés depuis les contextes où l’objet est accessible. Le niveau `protected` accorde aussi certains accès aux classes dérivées.

Pour faire un lien entre les services offerts par la classe et l’utilisateur d’un logiciel, on a défini des méthodes publiques. L’ensemble de ces services constitue l’interface publique de cette classe. Alors, les utilisateurs d’une classe n’ont plus besoin de se préoccuper de la manière dont s'exécutent les tâches. Ils ne peuvent généralement pas accéder directement aux membres privés; ils utilisent au contraire les méthodes publiques, qui constituent l’interface offerte par la classe.

Les opérations sur les données privées peuvent être contrôlées par des méthodes membres. Certaines sont des accesseurs (lecture) ou des mutateurs (modification), mais il n’est pas nécessaire de fournir une fonction de ce type pour chaque attribut. Par exemple, pour permettre la lecture d’une donnée privée, la classe peut utiliser une fonction get, alors que, pour modifier ces données, la classe peut utiliser la fonction set. De telles modifications semblent violer la notion de données privées.

Une méthode de modification peut effectuer les validations nécessaires avant de changer une donnée. Un accesseur peut fournir une information sans donner directement accès à sa représentation interne. Enfin, une méthode privée peut servir d’utilitaire interne, mais elle ne fait pas partie de l’interface publique de la classe.

{{< boite type="important" >}}
Dans une `class` C++, l’accès par défaut est `private`; dans une `struct`, il est `public`. Les méthodes d’une classe peuvent accéder aux membres privés des objets de cette classe. L’interface publique doit exposer les services nécessaires, sans rendre systématiquement tous les attributs modifiables.
{{< /boite >}}

### 3.4. Comportement et services des objets {#comportement-et-services-des-objets}

Tout objet a un certain comportement qui dépend du milieu dans lequel il évolue. En programmation orientée objet, les applications sont essentiellement composées d’un ensemble d’objets, chacun détenant les clefs de son comportement. Ces objets doivent trouver une manière de communiquer entre eux : l’envoi de messages est le mode privilégié d’échange entre les objets. Un message est une structure qu’on peut formellement décrire comme suit :

{{< boite type="code" >}}
```text
MESSAGE = <objet destinataire, méthode à exécuter, arguments>
```
{{< /boite >}}

Les arguments sont les valeurs passées en paramètres à la méthode activée.

Par ailleurs, le processus d’envoi de messages aboutit à l’activation de certaines méthodes selon un protocole prédéfini; cela fait référence à des notions de fonctions et de services.

Une fonction est une activité (ensemble de traitements) qui conduit à la satisfaction d’un besoin général ou à l’obtention d’un résultat particulier. Un service est un comportement spécifique qu’adopte un objet à la demande d’un autre objet. La [figure 4](#fig-figure-08) illustre une sollicitation de services par laquelle un objet demande à l’objet Employé d’exécuter la méthode Payer_salaire. L’appel d’une méthode est une requête, c'est-à-dire un message de l’appelant demandant l’exécution d’une certaine action. Les relations entre les objets s’établissent par l’application de certains principes de coopération, selon lesquels un objet sous-traite une partie de son activité en sollicitant des services à d’autres objets.

Cette représentation des objets comme destinataires de messages est un modèle conceptuel. En C++, une méthode est exécutée lorsqu’elle est appelée : un objet ordinaire n’est pas un processus qui attend continuellement des messages. La programmation orientée objet organise notamment le code autour des données et des responsabilités des objets. Autrement dit, pour traiter une application, le programmeur définit les types d’objets appropriés, avec leurs comportements spécifiques, chaque entité manipulée dans le programme étant un représentant d’un de ces types.

{{< figure-cours src="figures/figure_08.png" id="fig-figure-08" numero="4" legende="Sollicitation de services." largeur="82%" >}}

### 3.5. Communication entre objets {#communication-entre-objets}

Conceptuellement, les objets peuvent collaborer en demandant l’exécution d’opérations. En C++, une telle interaction se réalise couramment par l’appel d’une méthode sur un objet. Les appels de fonctions, les conditions et les boucles restent bien entendu des mécanismes du langage. Essentiellement, le protocole d’envoi de messages comporte deux parties : l’expéditeur et le destinataire. Lors du transfert d’une information, l’expéditeur doit spécifier le nom du destinataire, un sélecteur de nom de message et des arguments. Une méthode peut retourner une valeur ou effectuer une opération sans valeur de retour. Il ne faut toutefois pas confondre cette distinction avec une communication asynchrone entre objets.

{{< figure-cours src="figures/figure_06.png" id="fig-figure-06" numero="5" legende="Envoi de messages entre plusieurs classes." largeur="82%" >}}

{{< boite type="exemple" >}}
L’instruction C++ `compte.deposer(100);` demande à l’objet `compte` d’exécuter sa méthode `deposer` avec la valeur `100` comme argument.
{{< /boite >}}

## 4. Modularité et réutilisabilité {#modularite-et-reutilisabilite}

### 4.1. La modularité {#la-modularite}

Les critères énoncés ci-dessus influent sur la façon de concevoir un logiciel, en particulier sur l’architecture logicielle. En effet, certains de ces critères ne sont pas respectés lorsque l’architecture d’un logiciel est monolithique. Dans ces conditions, le moindre changement d’une spécification peut avoir des répercussions très importantes sur le logiciel, imposant une lourde charge de travail pour effectuer l’entretien et les mises à jour. Pour la conception des logiciels, on adopte généralement une architecture assez flexible pour éviter un tel problème, soit une architecture intégrant des entités indépendantes : les modules.

L’intérêt de ce type de conception est de concentrer les connaissances liées à une entité logique à l’intérieur d’un module, qui est le seul habilité à exploiter ces connaissances. L’une des conséquences immédiates est que, lorsqu’une mise à jour doit être effectuée sur une entité logique, celle-ci ne touche qu’un seul module, ce qui confine le travail de maintenance. Il existe des approches descendantes, qui décomposent un problème en sous-problèmes, et des approches ascendantes, qui combinent des composants plus simples. Elles peuvent être utilisées de manière complémentaire.

La qualité d’un module dépend notamment de sa compréhensibilité, de la limitation des changements qu’il impose aux autres composants et de sa capacité à contenir les erreurs. Pour y parvenir, ses interfaces doivent être explicites, les dépendances maîtrisées et les détails internes protégés. En C++, les classes constituent un moyen d’appliquer ces principes.

### 4.2. La réutilisabilité {#la-reutilisabilite}

La réutilisabilité consiste à exploiter, dans un nouveau contexte, des composants déjà développés. Les bibliothèques en sont un exemple courant : elles fournissent des structures de données et des opérations de recherche, de tri ou d’insertion.

Une classe réutilisable expose une interface claire et limite les dépendances envers ses détails internes. La composition, l’héritage et la programmation générique offrent des stratégies complémentaires pour éviter de répéter le même code.

{{< boite type="exemple" >}}
Une classe représentant un article peut être utilisée dans une application de caisse et dans un système d’inventaire, à condition que ses responsabilités et son interface soient adaptées aux deux usages.
{{< /boite >}}

### 4.3. Surcharge et généricité : aperçu {#surcharge-et-genericite-apercu}

La surcharge permet de définir des fonctions ou des opérateurs portant le même nom dans des contextes compatibles, selon les règles du langage. La généricité permet, en C++, d’écrire des fonctions ou des classes paramétrées par des types, notamment au moyen des `templates`. Ces deux mécanismes seront approfondis ultérieurement.

## 5. Relations entre classes, héritage et polymorphisme {#relations-entre-classes-heritage-et-polymorphisme}

### 5.1. Héritage et relations entre classes {#heritage-et-relations-entre-classes}

En général, les systèmes ne naissent pas dans un monde vide. Les nouveaux logiciels sont presque toujours issus de développements antérieurs; la meilleure manière de les créer consiste à procéder par imitation, amélioration et combinaison. Il s'agit là de l'une des préoccupations essentielles de la programmation orientée objet.

Les classes permettent de regrouper des données et des opérations au sein de modules cohérents. Lorsqu’une famille d’entités partage des caractéristiques et des comportements, l’héritage offre un mécanisme de spécialisation. Il ne constitue toutefois pas la seule stratégie de réutilisation : la composition et les fonctions génériques sont également importantes.

En effet, pour réaliser des progrès en matière de réutilisabilité et d’extensibilité, il peut être utile d’utiliser des relations entre les classes : une classe peut être une extension, une spécialisation ou une combinaison d’autres classes. Sur ce plan, l’héritage joue les rôles d’outil et de langage qui permettent d’enregistrer et d’utiliser ces relations.

De façon générale, dire qu’une classe B hérite d’une classe A, c’est dire que les propriétés de A sont aussi celles de B. La relation d’héritage organise hiérarchiquement les classes en graphes d’héritage. L’héritage simple correspond au cas où une classe dérive directement d’une seule classe de base. Une hiérarchie n’utilisant que ce type de relation peut être représentée comme un arbre. L’héritage est multiple si une classe peut directement hériter de plusieurs classes de base. Illustrons ces concepts par un exemple.

Supposons que nous désirons créer une librairie graphique pour représenter des figures géométriques. L’une des classes d’une telle librairie pourrait décrire les polygones, avec des opérations telles que le calcul du périmètre, la translation, la rotation, etc. Si nous définissons maintenant une nouvelle classe qui représente les rectangles, nous avons la possibilité de repartir à zéro ou de considérer ces derniers comme des cas particuliers de polygones, avec toutefois des caractéristiques bien spécifiques : le nombre de sommets est 4, les angles sont droits.

Nous pouvons définir une classe Rectangle qui hérite de la classe Polygone. Dans ce cas, toutes les primitives de Polygone sont applicables à Rectangle et ne devraient pas se répéter dans cette dernière classe. Un tel processus est transitif : toute classe qui hérite de Rectangle, par exemple Carré, a aussi les caractéristiques de Polygone. De ce fait, le graphe constitue un arbre dont la racine représente la classe la plus générale. Cette classe générale est définie pour les besoins de la hiérarchie. Contrairement à certains autres langages, C++ n’impose pas de classe racine universelle. La [figure 6](#fig-figure-02) illustre une hiérarchie de classes graphiques.

{{< figure-cours src="figures/figure_02.png" id="fig-figure-02" numero="6" legende="Hiérarchie de classes graphiques." largeur="82%" >}}

L’héritage, tel que nous venons de le voir, est simple. L’héritage multiple désigne un cas différent : une même classe dérive directement de plusieurs classes de base.

Certains langages disposent d’une classe racine commune, souvent appelée `Object`. Ce n’est pas le cas de C++. La [figure 7](#fig-figure-03) présente une hiérarchie illustrative; elle montre plusieurs branches d’héritage, mais pas, à elle seule, une classe possédant plusieurs classes de base directes. En créant la classe AlimElectrique, on regroupe les informations propres à l’alimentation électrique, ce qui permet d’en faire hériter la classe Téléviseur d’une part, et la classe ElectroMénager d’autre part.

L’héritage multiple peut servir à combiner plusieurs interfaces ou comportements, mais il peut aussi accroître la complexité du programme. Il ne garantit ni une économie de mémoire ni une maintenance plus simple. Toutefois, le contenu et l’agencement des classes doivent être développés avec beaucoup de soin. Lorsque le graphe d’héritage devient complexe, son exploitation requiert beaucoup d’expérience.

{{< figure-cours src="figures/figure_03.png" id="fig-figure-03" numero="7" legende="Hiérarchie de classes avec plusieurs branches d’héritage." largeur="82%" >}}

Dans certains cas, lorsqu’une classe B a besoin d’une classe A, il peut y avoir hésitation sur les relations à utiliser : B est-il un héritier de A ou son client? L’héritage est approprié si toute occurrence de B peut aussi être considérée comme une occurrence de A, ce qui donne lieu à la relation « est »; par exemple, un rectangle est un polygone.

Quant à la relation client, elle est appropriée lorsque toute occurrence de B possède simplement un ou plusieurs attributs de type A, ce qui donne lieu à la relation « a ». Une erreur typique consiste à déclarer, par exemple, Maison comme héritier de Porte et de Étage, alors qu’en réalité, une maison possède simplement ces composantes et en est donc un client.

Il faut distinguer la surcharge, qui concerne des fonctions de même nom avec des listes de paramètres différentes, et l’ambiguïté liée à l’héritage multiple, qui peut survenir si plusieurs classes de base proposent un membre du même nom. La [figure 8](#fig-figure-04) illustre une situation de spécialisation des objets; son intitulé historique ne doit pas être interprété comme la démonstration d’un conflit d’héritage multiple.

{{< figure-cours src="figures/figure_04.png" id="fig-figure-04" numero="8" legende="Spécialisation des comportements d’emballage (illustration conceptuelle)." largeur="82%" >}}

Il s’agit d’un problème de partage efficace des connaissances. La classe est considérée comme un réservoir de connaissances à partir duquel il est possible de définir d’autres classes plus spécifiques, complétant les connaissances de leur classe de base. Les connaissances les plus générales sont ainsi mises en commun dans des classes qui sont spécialisées par définition de sous-classes contenant des connaissances de plus en plus spécifiques. Ainsi, une sous-classe constitue une spécialisation de la description de sa superclasse.

{{< boite type="important" >}}
Pour un premier contact, retenons surtout la relation « est un » : un rectangle est un polygone. L’héritage multiple et la résolution de conflits seront approfondis plus tard; les figures précédentes sont conservées pour illustrer des hiérarchies, et non pour enseigner leur syntaxe C++.
{{< /boite >}}

{{< boite type="remarque" >}}
Quelques repères aident à choisir entre la relation « est un » et la relation « a un » :

- un objet ne change jamais de classe : un rôle qui peut changer au cours du temps, comme le statut d'un étudiant à temps plein ou à temps partiel, se représente par un attribut, et non par une classe dérivée ;
- une donnée qui décrit le lien entre deux objets, et non l'un d'eux, appartient à une classe qui représente ce lien : la note obtenue dans un cours ne décrit ni l'étudiant seul, ni le cours seul, mais l'inscription de cet étudiant à ce cours ;
- un objet peut **posséder** ses composantes, qui disparaissent avec lui (une commande et ses lignes), ou seulement **utiliser** un objet qui existe sans lui (une commande et son client).

{{< /boite >}}

### 5.2. Le polymorphisme {#le-polymorphisme}

Le polymorphisme est la capacité d’obtenir plusieurs réactions à une sollicitation donnée. Autrement dit, plusieurs objets différents peuvent répondre de manière différente au même message. La [figure 9](#fig-figure-05) illustre un tel concept. En C++, le polymorphisme dynamique permet notamment d’appeler une méthode virtuelle à travers une référence ou un pointeur vers une classe de base et d’obtenir le comportement de la classe dérivée réelle. Ainsi, une opération `dessiner()` peut produire un résultat différent pour un cercle ou un rectangle. La surcharge des fonctions ou des opérateurs et les templates relèvent d’autres formes de polymorphisme, généralement déterminées à la compilation.

{{< figure-cours src="figures/figure_05.png" id="fig-figure-05" numero="9" legende="Polymorphisme." largeur="82%" >}}

{{< boite type="exemple" >}}
Une application graphique peut manipuler une collection de figures et demander à chacune de se dessiner. Chaque type de figure définit sa propre manière d’exécuter cette opération. La [figure 9](#fig-figure-05) illustre ce principe sans exiger encore de connaître les fonctions virtuelles en détail.
{{< /boite >}}

## 6. Les langages orientés objet et la place de C++ {#les-langages-orientes-objet-et-la-place-de-c}

L’approche orientée objet est prise en charge par plusieurs langages. Smalltalk a joué un rôle historique important dans le développement de cette approche. Objective-C, Java et C# proposent également des mécanismes de classes, d’objets et d’héritage, avec des choix de conception et des environnements différents.

C++ est issu du langage C, mais constitue un langage à part entière, normalisé et multiparadigme. Il permet de combiner des fonctions, des classes, la programmation générique et d’autres mécanismes. Il prend en charge l’encapsulation, l’héritage et le polymorphisme, notamment au moyen des méthodes virtuelles. Il ne possède pas de classe racine `Object` universelle.

La classification historique entre langages « basés objet », « basés classes » et « orientés objet » peut aider à comprendre l’évolution de ces idées, mais elle ne forme pas une taxonomie exhaustive des langages actuels. La [figure 10](#fig-figure-09) est conservée à titre de repère historique; ses catégories et ses exemples ne doivent pas être considérés comme une classification normative ou actuelle.

{{< figure-cours src="figures/figure_09.png" id="fig-figure-09" numero="10" legende="Classification historique et schématique des langages de programmation (à interpréter avec prudence)." largeur="70%" >}}

Dans la suite du cours, nous utiliserons C++ pour passer de ces principes conceptuels à la définition et à la manipulation de classes et d’objets.

## 7. Conception par objets : étude de cas {#conception-par-objets-etude-de-cas}

Après avoir présenté les objets, les classes et leurs relations, appliquons ces notions à un exemple de conception. Il ne s’agit pas encore de produire une application C++ complète, mais d’identifier les responsabilités et les interactions des classes.

Un logiciel doit gérer un dessin graphique interactif dans un système de multifenêtrage. Ce dessin est composé d’objets graphiques qui, une fois sélectionnés à l’aide de la souris, réagissent chacun d’une manière bien spécifique. Ainsi, le dessin doit pouvoir gérer l’apparition et la disparition d’éléments graphiques, être imprimé et transmettre les sélections de l’utilisateur aux objets désignés. Par exemple, lorsqu’un utilisateur clique dans la fenêtre, le dessin reçoit un message qui lui fournit les coordonnées du point sélectionné. La [figure 11](#fig-figure-11) illustre tous ces concepts.

{{< figure-cours src="figures/figure_11.png" id="fig-figure-11" numero="11" legende="Dessin et objets graphiques à concevoir." largeur="82%" >}}

Deux classes d’objets sont alors définies : le dessin et l’objet graphique. La communication entre ces objets se fait par des envois de messages de la forme :

{{< boite type="code" >}}
```text
objet message(paramètres)
```
{{< /boite >}}

Dans le cas de la [figure 11](#fig-figure-11), les opérations que l’on peut effectuer sur la classe Dessin (ses méthodes) sont :

- tenir_compte_sélection (position : coordonnées);
- imprimer().

Quant à la classe Objets_graphiques, elle a les méthodes suivantes :

- tenir_compte_sélection(), où l’objet doit réagir spécifiquement à sa sélection;
- contenir_position(position : coordonnées), qui retourne une valeur booléenne pour indiquer si l’objet possède la position fournie en paramètre.

Lorsqu’un utilisateur clique dans le dessin, ce dernier est informé de l’envoi d’un message tenir_compte_sélection() et exécute le traitement suivant :

{{< boite type="code" >}}
```text
POUR chaque objet_courant de la classe Objets_graphiques
SI objet_courant contenir_position(position)
objet_courant tenir_compte_sélection()
FINSI
FINPOUR
```
{{< /boite >}}

Poursuivons notre exemple en faisant correspondre des noms aux objets graphiques. Nous avons alors :

- les navettes, qui sont des objets graphiques mobiles, créés périodiquement par le dessin et qui le traversent de part et d’autre en évitant les objets graphiques situés sur leur trajectoire;
- les missiles, qui sont aussi des objets mobiles créés aléatoirement et qui se déplacent vers les navettes les plus proches pour entrer en collision avec elles;
- les obstacles, qui sont des objets graphiques immobiles situés dans le dessin et créés au début de l’application; lorsqu’un objet mobile entre en collision avec eux ou lorsqu’ils sont sélectionnés, ils changent de forme;
- les objets mobiles, qui se déplacent et qui changent de trajectoire lorsqu’ils sont sélectionnés.

Ces catégories sont illustrées à la [figure 12](#fig-figure-12). Les objets mobiles peuvent spécialiser les objets graphiques, tandis que les navettes et les missiles peuvent spécialiser les objets mobiles. Les classes dérivées précisent notamment :

- leur forme spécifique;
- la redéfinition de certaines méthodes comme tenir_compte_sélection();
- les propriétés supplémentaires que possèdent certaines classes, telles que déplacer().

Le principe de fonctionnement du système est simple : la classe Dessin aura une méthode appelée traiter_cycliquement qui sera activée cycliquement et agira comme un séquenceur par rapport aux objets mobiles. Une telle méthode exécute le traitement suivant :

{{< boite type="code" >}}
```text
SI un intervalle de temps est écoulé
navette create()
missile create()
FINSI
Pour chaque objet_courant parmi les Objets_graphiques
SI objet_courant appartient à la classe Objets_mobiles
objet_courant déplacer()
FINSI
FINPOUR
```
{{< /boite >}}

{{< figure-cours src="figures/figure_12.png" id="fig-figure-12" numero="12" legende="Navette, missile et obstacle." largeur="82%" >}}

Par ailleurs, les objets mobiles doivent tenir compte des autres objets graphiques pour réagir. La navette doit éviter les obstacles, alors que le missile vise les navettes. Cela amène à la définition des méthodes suivantes :

- Présence(trajectoire_souhaitée : trajectoire), qui retourne une valeur booléenne pour indiquer si l’objet courant est sur la trajectoire fournie;
- Déterminer_position(), qui spécifie la position de l’objet courant.

L’ensemble des classes et de leurs méthodes donne alors lieu au modèle de la [figure 13](#fig-figure-13).

{{< figure-cours src="figures/figure_13.png" id="fig-figure-13" numero="13" legende="Classes de l’application graphique." largeur="82%" >}}

Cet exemple montre comment la conception par objets mène à une structure simple organisée autour des classes. Ces dernières n’ont pas besoin d’être complètes au moment de la conception du programme, mais peuvent être élaborées progressivement. La simplicité de l’implémentation suggère des idées intéressantes pour la spécification des modules.

{{< boite type="synthese" >}}
Ce module a introduit les objets et les classes, puis l’abstraction, l’encapsulation et la collaboration entre objets. Il a également présenté les relations entre classes, l’héritage et le polymorphisme, ainsi que leur contribution possible à la modularité et à la réutilisabilité. L’objectif était de savoir reconnaître ces concepts dans un problème concret avant d’en maîtriser la syntaxe C++.
{{< /boite >}}

[^1]: Meyer, B. (1991). *Conception et programmation par objets* (2e éd.). Paris : InterÉditions.
