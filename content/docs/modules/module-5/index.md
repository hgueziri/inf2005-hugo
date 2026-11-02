---
title: "Module 5 : Programmation parallèle, distribuée et réseau en C++"
linkTitle: "Module 5"
description: "INF 2005 – Programmation orientée objet avec C++"
weight: 50
---

{{< figure-cours src="figures/banner_5.png" alt="Bannière du cours INF 2005 – Programmation orientée objet avec C++" largeur="100%" >}}

# Module 5 : Programmation parallèle, distribuée et réseau en C++

{{< boite type="objectif" >}}
À la fin de ce module, l'étudiante ou l'étudiant devrait être capable de :

- expliquer l'intérêt de la programmation parallèle et distinguer les grandes familles d'architectures parallèles ;
- différencier un programme séquentiel, parallèle, multitâche et distribué ;
- comprendre les principes d'un système distribué, du modèle client-serveur et du middleware ;
- distinguer un processus d'un thread et expliquer le rôle de la synchronisation ;
- utiliser les notions de base liées aux threads POSIX et aux mutex ;
- comprendre les notions fondamentales des sockets : domaine, type, protocole, descripteur et primitives ;
- situer le rôle des bibliothèques scientifiques et des patrons de classes en C++ ;
- exécuter des exemples courts avec Jupyter Notebook, VS Code et `g++`.

{{< /boite >}}

{{< boite type="contenu" >}}
**Contenu du module :** comprendre les bases de la programmation parallèle, distribuée et réseau en C++, puis savoir tester des exemples simples dans un environnement moderne.
{{< /boite >}}

{{< boite type="fiche" >}}
| | |
|---|---|
| Cours | INF 2005 – Programmation orientée objet avec C++ |
| Document | Texte 5 – Programmation parallèle, distribuée et réseau |
| Thèmes principaux | Parallélisme, systèmes distribués, multitâche, threads, POSIX, mutex, sockets, programmation réseau, bibliothèques scientifiques et patrons de classes |
| Environnement recommandé | Jupyter Notebook et VS Code avec `g++` |
| Norme recommandée | C++17 ou version plus récente |
{{< /boite >}}

## Table des matières {#table-des-matieres}

- [1 Notions sur la programmation parallèle](#notions-sur-la-programmation-parallele)
  - [1.1 Intérêt de la programmation parallèle](#interet-de-la-programmation-parallele)
  - [1.2 Programmes parallèles et ordinateurs parallèles](#programmes-paralleles-et-ordinateurs-paralleles)
- [2 Programmation répartie ou distribuée](#programmation-repartie-ou-distribuee)
  - [2.1 Définition d'un système distribué](#definition-d-un-systeme-distribue)
  - [2.2 Caractéristiques des systèmes distribués](#caracteristiques-des-systemes-distribues)
  - [2.3 Types de systèmes distribués](#types-de-systemes-distribues)
  - [2.4 Environnements distribués et intergiciels](#environnements-distribues-et-intergiciels)
- [3 Programmation multitâche et threads en C++](#programmation-multitache-et-threads-en-c)
  - [3.1 Processus et threads](#processus-et-threads)
  - [3.2 Approche moderne : `std::thread`](#approche-moderne-std-thread)
  - [3.3 Utilisation de POSIX](#utilisation-de-posix)
  - [3.4 Mutex et zones critiques](#mutex-et-zones-critiques)
- [4 Introduction à la programmation réseau](#introduction-a-la-programmation-reseau)
  - [4.1 Définition d'un socket](#definition-d-un-socket)
  - [4.2 Entités et descripteur d'un socket](#entites-et-descripteur-d-un-socket)
  - [4.3 Domaines d'un socket](#domaines-d-un-socket)
  - [4.4 Modes de communication : TCP et UDP](#modes-de-communication-tcp-et-udp)
  - [4.5 Primitives sur les sockets](#primitives-sur-les-sockets)
  - [4.6 Exemple guidé d'un serveur TCP](#exemple-guide-d-un-serveur-tcp)
- [5 Bibliothèques scientifiques en C++](#bibliotheques-scientifiques-en-c)
  - [5.1 Bibliothèques scientifiques](#bibliotheques-scientifiques)
  - [5.2 Bibliothèque mathématique](#bibliotheque-mathematique)
  - [5.3 Patrons de fonctions et de classes](#patrons-de-fonctions-et-de-classes)
- [6 Synthèse finale du module](#synthese-finale-du-module)
- [Annexe A – Commandes utiles](#annexe-a-commandes-utiles)
- [Annexe B – Portabilité des exemples](#annexe-b-portabilite-des-exemples)
- [Annexe C – Exemple complet : threads POSIX et mutex](#annexe-c-exemple-complet-threads-posix-et-mutex)
- [Annexe D – Détail des primitives sockets](#annexe-d-detail-des-primitives-sockets)
- [Annexe E – Client et serveur : séquence conceptuelle](#annexe-e-client-et-serveur-sequence-conceptuelle)
- [Annexe F – Bibliothèques scientifiques : exemples supplémentaires](#annexe-f-bibliotheques-scientifiques-exemples-supplementaires)

## 1. Notions sur la programmation parallèle {#notions-sur-la-programmation-parallele}

Les modules précédents ont présenté la structuration d'un programme en classes, les fonctions et les bibliothèques standard. Ce dernier module ouvre sur la manière dont plusieurs tâches ou plusieurs programmes peuvent coopérer. Il s'agit d'une introduction aux principes de concurrence, de parallélisme et de communication, et non d'une formation complète à l'administration de systèmes ou aux réseaux.

La programmation parallèle consiste à décomposer un traitement en plusieurs tâches pouvant être exécutées simultanément, par exemple sur plusieurs cœurs d'un processeur. Ces tâches peuvent coopérer pour accélérer un calcul ou traiter un volume important de données. Le parallélisme ne doit pas être confondu avec la simple concurrence : plusieurs tâches peuvent progresser de façon entrelacée sur un seul cœur sans s'exécuter exactement au même instant.

{{< boite type="definition" >}}
La **programmation parallèle** cherche à effectuer plusieurs calculs en même temps. La **concurrence** désigne plus généralement la progression de plusieurs tâches pendant une même période, même si leurs instructions s'alternent sur un seul cœur.
{{< /boite >}}

Elle répond à plusieurs limites des architectures classiques : puissance de calcul limitée, contraintes de mémoire, lenteur des entrées-sorties, problèmes de synchronisation et difficulté de traiter rapidement des problèmes de grande taille.

### 1.1. Intérêt de la programmation parallèle {#interet-de-la-programmation-parallele}

La programmation parallèle est utile dans de nombreux domaines : météorologie, climatologie, aéronautique, simulation, traitement d'images, analyse de données, intelligence artificielle et calcul scientifique.

{{< boite type="important" >}}
Ajouter des cœurs ou des processeurs ne rend pas automatiquement un programme plus rapide. Il faut que le programme soit conçu pour exploiter le parallélisme : découpage en tâches, synchronisation correcte et limitation des parties strictement séquentielles.
{{< /boite >}}

{{< tableau >}}
| Avantage | Explication |
|---|---|
| Réduction du temps de calcul | Plusieurs sous-tâches peuvent être exécutées simultanément. |
| Meilleure utilisation du matériel | Les différents cœurs du processeur sont mieux exploités. |
| Traitement de grands volumes | Les données peuvent être réparties entre plusieurs unités de calcul. |
| Traitement de lots indépendants | Des fichiers ou ensembles de données distincts peuvent être traités simultanément. |
{{< /tableau >}}

### 1.2. Programmes parallèles et ordinateurs parallèles {#programmes-paralleles-et-ordinateurs-paralleles}

Un programme séquentiel s’exécute essentiellement sur un seul fil d’exécution. Un programme parallèle, lui, peut diviser son travail entre plusieurs tâches. Les outils utilisés peuvent être des threads, OpenMP, des processus, ou encore des bibliothèques de calcul spécialisées.

{{< boite type="important" >}}
Par exemple, une application peut continuer à répondre à l'utilisateur pendant le téléchargement d'un fichier (tâches concurrentes). Le calcul simultané de deux parties d'une image sur deux cœurs constitue plutôt un exemple de parallélisme.
{{< /boite >}}

{{< figure-cours src="figures/flynn.png" numero="1" legende="Classification de Flynn des architectures parallèles." largeur="93%" >}}

La classification de Flynn distingue les architectures selon le nombre de flux d'instructions et de flux de données :

- **SISD** : une instruction agit sur une donnée ; modèle séquentiel classique ;
- **SIMD** : une instruction agit sur plusieurs données ; utile pour les calculs vectoriels et certains GPU ;
- **MISD** : plusieurs instructions agissent sur une même donnée ; cas plus rare ;
- **MIMD** : plusieurs processeurs exécutent plusieurs instructions sur plusieurs données ; modèle courant dans les systèmes multicœurs et les grappes.

## 2. Programmation répartie ou distribuée {#programmation-repartie-ou-distribuee}

Un système distribué répond au problème de la centralisation des ressources. Dans un tel système, les ressources sont réparties entre plusieurs machines, services ou composants, parfois hétérogènes et géographiquement éloignés.

### 2.1. Définition d'un système distribué {#definition-d-un-systeme-distribue}

{{< boite type="definition" >}}
Un **système distribué** est un ensemble de composants informatiques autonomes, reliés par un réseau, qui coopèrent et se présentent à l'utilisateur comme un système cohérent.
{{< /boite >}}

Les ressources distribuées peuvent être des ordinateurs, des services web, des bases de données, des fichiers, des imprimantes, des capteurs ou des applications distantes.

### 2.2. Caractéristiques des systèmes distribués {#caracteristiques-des-systemes-distribues}

Les propriétés suivantes constituent des objectifs fréquents de conception d’un système distribué, mais elles ne sont pas automatiquement garanties :

- **hétérogène** : les composants peuvent utiliser des systèmes et plateformes différents ;
- **ouvert** : il doit permettre l'ajout ou le remplacement de composants ;
- **disponible** : certaines pannes ne doivent pas interrompre tout le système ;
- **évolutif** : il doit pouvoir grandir tout en conservant des performances acceptables ;
- **transparent** : l'utilisateur ne doit pas toujours connaître l'emplacement exact des ressources.

### 2.3. Types de systèmes distribués {#types-de-systemes-distribues}

{{< tableau >}}
| Type | Exemple ou rôle |
|---|---|
| Grappes et grilles de calcul | Plusieurs machines coopèrent pour exécuter des calculs ou partager des ressources. |
| Systèmes d'information distribués | Plusieurs applications ou bases de données collaborent dans une organisation. |
| Systèmes embarqués distribués | Plusieurs dispositifs autonomes ou mobiles échangent des données. |
| Services web | Des applications distantes communiquent par protocoles réseau. |
{{< /tableau >}}

### 2.4. Environnements distribués et intergiciels {#environnements-distribues-et-intergiciels}

Un intergiciel (*middleware*) fournit des services de communication et d'échange de données à des applications distribuées. Des technologies comme CORBA, DCOM ou Java RMI en sont des exemples historiques ; aujourd'hui, des API réseau et des mécanismes d'appel à distance remplissent souvent des rôles comparables.

{{< figure-cours src="figures/distributed.png" numero="2" legende="Rôle d'un intergiciel dans un système distribué." largeur="93%" >}}

{{< boite type="important" >}}
Le **modèle client-serveur** décrit une interaction : un client demande un service à un serveur. Un **intergiciel** (*middleware*) est plutôt une couche logicielle qui facilite cette communication. Les deux notions sont donc complémentaires, et non deux modèles concurrents.
{{< /boite >}}

## 3. Programmation multitâche et threads en C++ {#programmation-multitache-et-threads-en-c}

La programmation multitâche permet à un système d’exécuter plusieurs activités simultanément. En C++, cette idée peut être mise en œuvre par des processus, des threads POSIX ou, dans une approche moderne, par les classes de la bibliothèque standard comme `std::thread`.

### 3.1. Processus et threads {#processus-et-threads}

Un processus possède son propre espace mémoire. Un thread, au contraire, est un fil d'exécution à l’intérieur d'un processus. Plusieurs threads d'un même processus partagent la même mémoire.

{{< figure-cours src="figures/thread_process.png" numero="3" legende="Relation entre processus, mémoire partagée et threads." largeur="93%" >}}

{{< tableau >}}
| Élément | Processus | Thread |
|---|---|---|
| Mémoire | Espace mémoire propre. | Mémoire partagée avec les autres threads du processus. |
| Communication | Plus coûteuse. | Plus rapide, car les données sont partagées. |
| Risque | Isolation plus forte. | Risques de conflits d’accès aux données. |
| Usage | Applications indépendantes. | Sous-tâches d'une même application. |
{{< /tableau >}}

### 3.2. Approche moderne : `std::thread` {#approche-moderne-std-thread}

Pour débuter avec les threads en C++, on privilégie ici `std::thread`, qui fait partie de la bibliothèque standard depuis C++11. L'interface POSIX est présentée ensuite comme complément propre aux environnements compatibles.

```cpp {linenos=table}
#include <iostream>
#include <thread>

void afficher_message(int id) {
    std::cout << "Thread " << id << " en execution\n";
}

int main() {
    std::thread t1(afficher_message, 1);
    std::thread t2(afficher_message, 2);

    t1.join();
    t2.join();

    return 0;
}
```

Compilation :

```bash {linenos=table}
g++ -std=c++17 main.cpp -o main -pthread
./main
```

{{< boite type="important" >}}
Les appels à `join()` attendent la fin des threads avant la sortie de `main()`. Les deux messages peuvent apparaître dans un ordre différent selon l'exécution ; leurs caractères peuvent aussi s'entrelacer à l'affichage. Ne supposez donc pas que le premier thread créé affiche toujours son message en premier.
{{< /boite >}}

### 3.3. Utilisation de POSIX {#utilisation-de-posix}

POSIX propose une API pour les threads, disponible surtout dans les environnements Unix/Linux. Les fonctions importantes sont :

- `pthread_create()` pour créer un thread ;
- `pthread_join()` pour attendre la fin d'un thread ;
- `pthread_exit()` pour terminer explicitement un thread ;
- `pthread_mutex_lock()` et `pthread_mutex_unlock()` pour protéger une zone critique.

```cpp {linenos=table}
#include <iostream>
#include <pthread.h>

void* travail(void* arg) {
    int id = *static_cast<int*>(arg);
    std::cout << "Thread POSIX " << id << "\n";
    return nullptr;
}

int main() {
    pthread_t thread;
    int id = 1;

    int code = pthread_create(&thread, nullptr, travail, &id);
    if (code != 0) {
        std::cerr << "Creation du thread impossible\n";
        return 1;
    }
    pthread_join(thread, nullptr);

    return 0;
}
```

Compilation :

```bash {linenos=table}
g++ -std=c++17 main.cpp -o main -pthread
./main
```

### 3.4. Mutex et zones critiques {#mutex-et-zones-critiques}

Lorsque plusieurs threads modifient une même variable sans synchronisation, le programme peut subir une **course aux données** (*data race*), qui entraîne un comportement indéfini en C++. Un mutex protège une **section critique** : un seul thread à la fois peut accéder à la partie protégée.

{{< figure-cours src="figures/mutex.png" numero="4" legende="Principe d'un mutex autour d'une zone critique." largeur="93%" >}}

```cpp {linenos=table}
#include <iostream>
#include <thread>
#include <mutex>

std::mutex verrou;
int compteur = 0;

void incrementer() {
    for (int i = 0; i < 1000; ++i) {
        std::lock_guard<std::mutex> garde(verrou);
        ++compteur;
    }
}

int main() {
    std::thread t1(incrementer);
    std::thread t2(incrementer);

    t1.join();
    t2.join();

    std::cout << "Compteur = " << compteur << '\n';
    return 0;
}
```

{{< boite type="attention" >}}
Le programme affiche normalement `Compteur = 2000` : chaque thread ajoute 1 au compteur mille fois. Le garde `std::lock_guard` verrouille le mutex à sa construction et le libère automatiquement à la fin du bloc. Sans cette protection, une *data race* rendrait le comportement indéfini ; il ne s'agit pas seulement d'un résultat qui varie.
{{< /boite >}}

## 4. Introduction à la programmation réseau {#introduction-a-la-programmation-reseau}

La programmation réseau permet à plusieurs processus de communiquer localement ou à distance. Le mécanisme classique présenté dans le texte original est la **socket**, qui représente une extrémité de communication.

### 4.1. Définition d'un socket {#definition-d-un-socket}

{{< boite type="definition" >}}
Une **socket** est un point de communication permettant à un processus d'envoyer ou de recevoir des données. Elle est manipulée par un descripteur, de manière proche d'un fichier dans les systèmes Unix.
{{< /boite >}}

Dans un modèle client-serveur, le serveur attend des connexions sur un port, tandis que le client initie la connexion vers ce port.

{{< figure-cours src="figures/socket_lifecycle.png" numero="5" legende="Cycle simplifié d'une communication client-serveur par socket." largeur="93%" >}}

### 4.2. Entités et descripteur d'un socket {#entites-et-descripteur-d-un-socket}

Le client doit connaître l'adresse IP et le port du serveur. Le serveur crée un socket, l'associe à une adresse et attend les clients. Une fois la connexion établie, les deux programmes peuvent échanger des données.

{{< tableau >}}
| Entête | Rôle |
|---|---|
| Client | Crée un socket, demande une connexion, échange des données, puis ferme la connexion. |
| Serveur | Crée un socket, l'associe à un port, attend une connexion, accepte le client, échange des données. |
| Descripteur | Entier utilisé par le programme pour manipuler la socket créée. |
| Port | Numéro permettant d'identifier un service réseau sur une machine. |
{{< /tableau >}}

### 4.3. Domaines d'un socket {#domaines-d-un-socket}

Les domaines précisent le contexte de communication :

- `AF_UNIX` ou `AF_LOCAL` : communication entre processus sur une même machine ;
- `AF_INET` : communication IPv4 sur réseau ;
- `AF_INET6` : communication IPv6.

Les structures d'adresses sont fournies par les en-têtes du système. Il ne faut pas les redéfinir soi-même ; leurs détails peuvent dépendre de la plateforme. Par exemple, sous Linux :

```cpp {linenos=table}
#include <sys/un.h>      // sockaddr_un (local)
#include <netinet/in.h>  // sockaddr_in (IPv4)

sockaddr_un local{};
local.sun_family = AF_UNIX;

sockaddr_in ipv4{};
ipv4.sin_family = AF_INET;
ipv4.sin_port = htons(18080);
```

{{< boite type="important" >}}
Ce bloc est un **extrait**, pas un programme autonome. Le champ `sin_port` utilise l'ordre des octets du réseau, d'où l'appel à `htons()`. Le chemin local et l'adresse IP doivent encore être renseignés pour établir une communication réelle.
{{< /boite >}}

### 4.4. Modes de communication : TCP et UDP {#modes-de-communication-tcp-et-udp}

{{< figure-cours src="figures/tcp_udp.png" numero="6" legende="Comparaison pédagogique entre TCP et UDP." largeur="93%" >}}

{{< boite type="important" >}}
En réseau IP, `SOCK_STREAM` est habituellement utilisé avec TCP : il transporte un flux ordonné et fiable d'octets, sans conserver les limites des messages envoyés. `SOCK_DGRAM` est habituellement utilisé avec UDP : chaque envoi correspond à un datagramme, mais sa livraison et son ordre ne sont pas garantis.
{{< /boite >}}

### 4.5. Primitives sur les sockets {#primitives-sur-les-sockets}

{{< figure-cours src="figures/socket_primitives.png" numero="7" legende="Principales primitives d'un serveur TCP." largeur="93%" >}}

{{< tableau >}}
| Primitive | Rôle |
|---|---|
| `socket()` | Crée un socket et retourne un descripteur. |
| `bind()` | Associe un socket à une adresse et à un port. |
| `listen()` | Met un socket serveur en attente de connexions. |
| `accept()` | Accepte une connexion entrante. |
| `connect()` | Demande une connexion vers un serveur. |
| `send()` / `recv()` | Envoie et reçoit des données. |
| `close()` | Ferme le descripteur de socket. |
{{< /tableau >}}

### 4.6. Exemple guidé d'un serveur TCP {#exemple-guide-d-un-serveur-tcp}

Le programme ci-dessous illustre un serveur TCP local sous Linux ou WSL. Contrairement à un simple appel à `listen()`, il accepte effectivement une connexion avec `accept()`. Il se termine après avoir reçu un message d'un client. Cet exemple reste volontairement limité à un seul échange.

```cpp {linenos=table}
#include <sys/socket.h>
#include <netinet/in.h>
#include <unistd.h>
#include <iostream>

int main() {
    int serveur = socket(AF_INET, SOCK_STREAM, 0);
    if (serveur == -1) return 1;

    sockaddr_in adresse{};
    adresse.sin_family = AF_INET;
    adresse.sin_addr.s_addr = htonl(INADDR_LOOPBACK);
    adresse.sin_port = htons(18080);

    if (bind(serveur, reinterpret_cast<sockaddr*>(&adresse),
             sizeof(adresse)) == -1 || listen(serveur, 1) == -1) {
        std::cerr << "Erreur bind/listen\n";
        close(serveur);
        return 1;
    }

    std::cout << "En attente d'un client sur le port 18080...\n";
    int client = accept(serveur, nullptr, nullptr);
    if (client == -1) {
        std::cerr << "Erreur accept\n";
        close(serveur);
        return 1;
    }

    char message[128]{};
    ssize_t n = recv(client, message, sizeof(message), 0);
    if (n > 0) {
        std::cout << "Message recu : ";
        std::cout.write(message, n);
        std::cout << '\n';
    }
    close(client);
    close(serveur);
    return 0;
}
```

{{< boite type="important" >}}
Pour effectuer un échange, il faut exécuter ce serveur dans un premier terminal, puis lancer le client ci-dessous depuis un second terminal de la même machine. Le serveur écoute uniquement l'adresse locale `127.0.0.1` ; il n'est donc pas accessible directement depuis un autre ordinateur. Les applications réelles doivent aussi gérer les erreurs de transmission, les lectures partielles, les délais et plusieurs clients.
{{< /boite >}}

```cpp {linenos=table}
#include <sys/socket.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <iostream>

int main() {
    int client = socket(AF_INET, SOCK_STREAM, 0);
    if (client == -1) return 1;

    sockaddr_in adresse{};
    adresse.sin_family = AF_INET;
    adresse.sin_port = htons(18080);
    if (inet_pton(AF_INET, "127.0.0.1", &adresse.sin_addr) != 1 ||
        connect(client, reinterpret_cast<sockaddr*>(&adresse),
                sizeof(adresse)) == -1) {
        std::cerr << "Connexion impossible\n";
        close(client);
        return 1;
    }

    const char message[] = "Bonjour du client";
    send(client, message, sizeof(message) - 1, 0);
    close(client);
    return 0;
}
```

{{< boite type="important" >}}
Enregistrez les deux programmes séparément dans `serveur.cpp` et `client.cpp`. Compilez-les avec `g++ -std=c++17 serveur.cpp -o serveur` et `g++ -std=c++17 client.cpp -o client`. Lancez d'abord `./serveur`, puis `./client` dans un autre terminal. Le serveur doit afficher `Message reçu : Bonjour du client`. Ces deux programmes utilisent l'API POSIX (Linux ou WSL).
{{< /boite >}}

{{< boite type="attention" >}}
Les sockets système ne sont pas toujours simples à tester dans Jupyter, surtout sur Windows. Pour les exercices du cours, il est préférable de tester les exemples réseau dans VS Code avec WSL/Linux ou dans un terminal Linux.
{{< /boite >}}

## 5. Bibliothèques scientifiques en C++ {#bibliotheques-scientifiques-en-c}

Les bibliothèques scientifiques fournissent des fonctions et structures spécialisées pour le calcul numérique, l’algèbre linéaire, les statistiques, la simulation ou le traitement de données.

### 5.1. Bibliothèques scientifiques {#bibliotheques-scientifiques}

En C++, certaines bibliothèques sont incluses dans la bibliothèque standard, tandis que d'autres sont externes. Dans un cours introductif, il faut surtout comprendre le principe : réutiliser un code testé et bien documenté plutôt que tout reprogrammer.

{{< tableau >}}
| Bibliothèque | Usage typique |
|---|---|
| `<cmath>` | Fonctions mathématiques : racine, puissance, sinus, cosinus, logarithme. |
| `<vector>` | Tableau dynamique, plus sûr et plus flexible qu'un tableau C classique. |
| `<algorithm>` | Tri, recherche, parcours et opérations générales. |
| `<numeric>` | Accumulation, produits, opérations numériques simples. |
| Bibliothèques externes | Calcul scientifique avancé, matrices, statistiques, simulation, optimisation. |
{{< /tableau >}}

### 5.2. Bibliothèque mathématique {#bibliotheque-mathematique}

```cpp {linenos=table}
#include <iostream>
#include <cmath>

int main() {
    double x = 16.0;
    double angle = 3.141592653589793 / 2.0;

    std::cout << "sqrt(x) = " << std::sqrt(x) << '\n';
    std::cout << "pow(x, 2) = " << std::pow(x, 2) << '\n';
    std::cout << "sin(pi/2) = " << std::sin(angle) << '\n';

    return 0;
}
```

### 5.3. Patrons de fonctions et de classes {#patrons-de-fonctions-et-de-classes}

Un patron (*template*) permet de définir un modèle générique pour plusieurs types. Il existe des **patrons de fonctions**, comme `maximum()` ci-dessous, et des **patrons de classes**, comme la classe `Boite` présentée à l'annexe F. Le type concret est déterminé lors de l'utilisation du patron.

{{< figure-cours src="figures/templates.png" numero="8" legende="Principe d'un patron de classe." largeur="93%" >}}

```cpp {linenos=table}
#include <iostream>

template <typename T>
T maximum(T a, T b) {
    return (a > b) ? a : b;
}

int main() {
    std::cout << maximum(4, 9) << '\n';
    std::cout << maximum(3.5, 2.1) << '\n';
    return 0;
}
```

{{< boite type="important" >}}
Les templates et la STL sont essentiels en C++ moderne. Ils permettent de construire du code réutilisable tout en conservant la vérification des types par le compilateur.
{{< /boite >}}

## 6. Synthèse finale du module {#synthese-finale-du-module}

{{< tableau >}}
| Notion | Ce qu'il faut retenir |
|---|---|
| Programmation parallèle | Découper un problème pour exploiter plusieurs unités de calcul. |
| Architecture parallèle | SISD, SIMD, MISD et MIMD classent les machines selon les flux de données et d'instructions. |
| Système distribué | Ensemble de composants autonomes coopérant à travers un réseau. |
| Thread | Fil d'exécution partageant la mémoire du processus. |
| Mutex | Mécanisme de verrouillage pour protéger une zone critique. |
| Socket | Point de communication entre processus locaux ou distants. |
| TCP/UDP | TCP est fiable et connecté ; UDP est plus léger mais non garanti. |
| Bibliothèques et templates | Outils de réutilisation et de généralisation du code C++. |
{{< /tableau >}}

{{< boite type="exemple" titre="Mini-activité" >}}
**Exercices de consolidation**

1. Expliquez la différence entre un programme séquentiel et un programme parallèle.
2. Donnez un exemple concret de système distribué utilisé dans la vie quotidienne.
3. Comparez un processus et un thread.
4. Expliquez pourquoi un mutex est nécessaire lorsque plusieurs threads modifient une même variable.
5. Classez les primitives suivantes selon leur rôle : `socket`, `bind`, `listen`, `accept`, `connect`, `send`, `recv`, `close`.
6. Écrivez une fonction template `minimum` qui retourne le plus petit de deux éléments.

{{< /boite >}}

## Annexe A – Commandes utiles {#annexe-a-commandes-utiles}

```bash {linenos=table}
g++ -std=c++17 main.cpp -o main
./main
```

```bash {linenos=table}
g++ -std=c++17 main.cpp -o main -pthread
./main
```

```bash {linenos=table}
%%bash
g++ -std=c++17 main.cpp -o main -pthread
./main
```

## Annexe B – Portabilité des exemples {#annexe-b-portabilite-des-exemples}

- Pour les threads en C++ moderne, `std::thread` et `std::mutex` sont préférables pour une introduction portable.
- Les exemples POSIX restent utiles pour comprendre les systèmes Unix/Linux, mais ils sont moins portables.
- Les exemples de sockets sont dépendants du système ; pour les tester dans le cours, VS Code avec WSL/Linux est recommandé.

## Annexe C – Exemple complet : threads POSIX et mutex {#annexe-c-exemple-complet-threads-posix-et-mutex}

Cette annexe conserve l'esprit du texte original sur POSIX, tout en proposant un exemple plus clair. Le programme crée deux threads qui incrémentent une variable partagée. Le mutex protège la zone critique.

```cpp {linenos=table}
#include <iostream>
#include <pthread.h>

pthread_mutex_t mutex = PTHREAD_MUTEX_INITIALIZER;
int compteur = 0;

void* incrementer(void*) {
    for (int i = 0; i < 100000; ++i) {
        pthread_mutex_lock(&mutex);
        ++compteur;           // zone critique
        pthread_mutex_unlock(&mutex);
    }
    return nullptr;
}

int main() {
    pthread_t t1, t2;

    pthread_create(&t1, nullptr, incrementer, nullptr);
    pthread_create(&t2, nullptr, incrementer, nullptr);

    pthread_join(t1, nullptr);
    pthread_join(t2, nullptr);

    std::cout << "Compteur final = " << compteur << std::endl;
    pthread_mutex_destroy(&mutex);
    return 0;
}
```

{{< boite type="important" >}}
Pour compiler cet exemple sous Linux ou WSL : `g++ -std=c++17 main.cpp -o main -pthread`. L'option `-pthread` informe le compilateur et l’éditeur de liens que le programme utilise la bibliothèque de threads.
{{< /boite >}}

## Annexe D – Détail des primitives sockets {#annexe-d-detail-des-primitives-sockets}

{{< tableau >}}
| Primitive | Utilisée par | Commentaire |
|---|---|---|
| `socket()` | Client et serveur | Crée le point de communication. Retourne un descripteur entier. |
| `bind()` | Serveur | Associe un socket à une adresse locale et à un port. |
| `listen()` | Serveur TCP | Place la socket en attente de connexions entrantes. |
| `accept()` | Serveur TCP | Accepte un client et retourne un nouveau descripteur pour le dialogue. |
| `connect()` | Client TCP | Demande l’établissement d'une connexion avec le serveur. |
| `send()` | Client et serveur | Envoie des octets sur un socket connectée. |
| `recv()` | Client et serveur | Reçoit des octets sur un socket connectée. |
| `shutdown()` | Client et serveur | Ferme une partie ou la totalité du canal de communication. |
| `close()` | Client et serveur | Libère le descripteur de socket. |
{{< /tableau >}}

{{< boite type="attention" >}}
Les exemples de sockets du texte original sont liés à l'API Unix. Ils ne sont pas directement portables tels quels dans tous les environnements Windows. Pour les faire fonctionner correctement, utiliser Linux, WSL ou un environnement compatible POSIX.
{{< /boite >}}

## Annexe E – Client et serveur : séquence conceptuelle {#annexe-e-client-et-serveur-sequence-conceptuelle}

{{< tableau >}}
| Serveur | Client |
|---|---|
| Créer un socket avec `socket()`. | Créer un socket avec `socket()`. |
| Associer l'adresse avec `bind()`. | Connaître l'adresse IP et le port du serveur. |
| Attendre avec `listen()`. | Demander la connexion avec `connect()`. |
| Accepter avec `accept()`. | Attendre que la connexion soit acceptée. |
| Échanger avec `send()` et `recv()`. | Échanger avec `send()` et `recv()`. |
| Fermer avec `close()`. | Fermer avec `close()`. |
{{< /tableau >}}

```cpp {linenos=table}
serveur = socket(AF_INET, SOCK_STREAM, 0)
bind(serveur, adresse_locale)
listen(serveur, taille_file)
client = accept(serveur)
recv(client, message)
send(client, reponse)
close(client)
close(serveur)
```

```cpp {linenos=table}
client = socket(AF_INET, SOCK_STREAM, 0)
connect(client, adresse_serveur)
send(client, message)
recv(client, reponse)
close(client)
```

## Annexe F – Bibliothèques scientifiques : exemples supplémentaires {#annexe-f-bibliotheques-scientifiques-exemples-supplementaires}

### Utilisation de `std::vector` et `std::accumulate` {#utilisation-de-std-vector-et-std-accumulate}

```cpp {linenos=table}
#include <iostream>
#include <vector>
#include <numeric>

int main() {
    std::vector<double> notes {14.5, 16.0, 12.0, 18.5};
    double somme = std::accumulate(notes.begin(), notes.end(), 0.0);
    double moyenne = somme / notes.size();

    std::cout << "Moyenne = " << moyenne << std::endl;
    return 0;
}
```

### Patron de classe simple {#patron-de-classe-simple}

```cpp {linenos=table}
#include <iostream>
#include <string>

template <typename T>
class Boite {
private:
    T valeur;
public:
    explicit Boite(T v) : valeur(v) {}
    T get() const { return valeur; }
};

int main() {
    Boite<int> entier(42);
    Boite<std::string> texte("INF 2005");

    std::cout << entier.get() << std::endl;
    std::cout << texte.get() << std::endl;
    return 0;
}
```

{{< boite type="important" >}}
La bibliothèque standard C++ moderne permet souvent de remplacer du code manuel par des conteneurs, algorithmes et patrons plus fiables. Dans un module d'introduction, il faut surtout apprendre à reconnaître quand réutiliser une bibliothèque plutôt que tout reprogrammer.
{{< /boite >}}
