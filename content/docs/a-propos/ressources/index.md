---
title: "Ressources"
weight: 30
---

# Ressources

Cette page rassemble les gabarits de rapport des travaux pratiques et une sélection de références pour apprendre le C++ et l’approfondir au-delà du cours.

## Gabarits de rapport des travaux pratiques

Chaque travail pratique se remet avec un rapport rédigé dans Word. Téléchargez le gabarit du travail que vous réalisez. Il contient la page de présentation (feuille d’identité et zone réservée à la personne tutrice), suivie d’une section par exercice, avec le nombre de points et les rubriques à remplir.

{{< tableau >}}
| Travail pratique | Contenu du rapport | Gabarit |
|---|---|---|
| [Travail pratique 1]({{< relref "/docs/evaluation/travail-pratique-1" >}}) | Réponses aux questions de conception, tableaux des classes et des relations à compléter | [INF2005_Travail-Pratique-1.docx](gabarits/INF2005_Travail-Pratique-1.docx) |
| [Travail pratique 2]({{< relref "/docs/evaluation/travail-pratique-2" >}}) | Pour chaque exercice : nom du fichier source, captures d’écran, commentaires | [INF2005_Travail-Pratique-2.docx](gabarits/INF2005_Travail-Pratique-2.docx) |
| [Travail pratique 3]({{< relref "/docs/evaluation/travail-pratique-3" >}}) | Pour chaque exercice : nom du fichier source, captures d’écran, commentaires | [INF2005_Travail-Pratique-3.docx](gabarits/INF2005_Travail-Pratique-3.docx) |
| [Travail pratique 4]({{< relref "/docs/evaluation/travail-pratique-4" >}}) | Pour chaque exercice : nom du fichier source, captures d’écran, justification demandée, commentaires | [INF2005_Travail-Pratique-4.docx](gabarits/INF2005_Travail-Pratique-4.docx) |
{{< /tableau >}}

{{< boite type="remarque" titre="Pour bien utiliser les gabarits" >}}
- Remplissez la feuille d’identité et laissez vide la zone réservée à la personne tutrice.
- Inscrivez vos réponses sous chaque rubrique, en ajoutant autant d’espace que nécessaire.
- Enregistrez le rapport sous le nom indiqué sur la page de présentation (par exemple `INF2005_TP1_VOTRENOM`).
- Pour les travaux pratiques 2 à 4, les fichiers sources sont nommés comme dans l’énoncé (par exemple `TP2_exercice1.cpp`).
- L’énoncé de chaque travail pratique demeure la référence pour les consignes de remise.
{{< /boite >}}

## Références pour apprendre le C++

Le cours utilise la norme C++17. Les ressources ci-dessous couvrent cette norme et les suivantes (C++20, C++23). Elles sont gratuites, à l’exception des livres. La langue est indiquée pour chacune.

### Cours et tutoriels en ligne

- **[La programmation en C++ moderne](https://zestedesavoir.com/tutoriels/822/la-programmation-en-c-moderne/)** — Zeste de Savoir, en français. Cours pour débutants, fondé sur C++17, qui présente les bases du langage et la bibliothèque standard. La partie sur la programmation orientée objet est encore en rédaction.
- **[Learn C++](https://www.learncpp.com/)** — en anglais. Tutoriel très progressif et mis à jour régulièrement, des premiers programmes jusqu’à l’héritage, aux fonctions virtuelles et aux normes récentes.
- **[Bienvenue dans C++ moderne](https://learn.microsoft.com/fr-ca/cpp/cpp/welcome-back-to-cpp-modern-cpp)** — Microsoft Learn, en français. Survol des bonnes pratiques actuelles : pointeurs intelligents, conteneurs standards, gestion des ressources (RAII).
- **[Get Started!](https://isocpp.org/get-started)** — Standard C++ Foundation, en anglais. Point de départ officiel qui oriente vers des livres, des compilateurs et des tutoriels recommandés.
- **[CppCon](https://www.youtube.com/@CppCon)** — conférences vidéo en anglais. La série « Back to Basics » présente les notions fondamentales (classes, héritage, polymorphisme, gestion de la mémoire) par des experts du langage.

### Références du langage

- **[cppreference.com](https://en.cppreference.com/cpp)** — en anglais ([version française](https://fr.cppreference.com/cpp) partielle et moins à jour). Référence la plus complète du langage et de la bibliothèque standard ; chaque fonctionnalité y est associée à la norme qui l’a introduite.
- **[Référence du langage C++](https://learn.microsoft.com/fr-ca/cpp/cpp/cpp-language-reference)** et **[Référence de la bibliothèque standard C++](https://learn.microsoft.com/fr-ca/cpp/standard-library/cpp-standard-library-reference)** — Microsoft Learn, en français.
- **[C++ Core Guidelines](https://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines)** — en anglais. Règles de bonne pratique rédigées sous la direction de Bjarne Stroustrup et Herb Sutter, notamment sur la conception des classes et des hiérarchies.
- **[Aide-mémoire hacking C++](https://hackingcpp.com/cpp/cheat_sheets.html)** — en anglais. Fiches visuelles sur la bibliothèque standard, les conteneurs et les algorithmes.

### Outils

- **[C++ dans Visual Studio Code](https://code.visualstudio.com/docs/languages/cpp)** et **[Utiliser GCC avec MinGW](https://code.visualstudio.com/docs/cpp/config-mingw)** — en anglais. Installation et configuration de l’environnement utilisé dans le cours (VS Code et g++).
- **[Compiler Explorer](https://godbolt.org/)** — compiler et exécuter du code C++ dans le navigateur, sans rien installer, et comparer plusieurs compilateurs et normes.
- **[C++ Insights](https://cppinsights.io/)** — montre le code que le compilateur génère implicitement (constructeurs, destructeurs, opérateurs) : utile pour comprendre ce qui se passe dans une classe.

### Livres

- Bjarne Stroustrup, *[Programming: Principles and Practice Using C++](https://www.stroustrup.com/PPP3.html)*, 3ᵉ éd., Addison-Wesley, 2024 — en anglais. Apprendre à programmer avec le C++ moderne (C++20 et C++23), par le créateur du langage.
- Bjarne Stroustrup, *[A Tour of C++](https://www.stroustrup.com/tour3.html)*, 3ᵉ éd., Addison-Wesley, 2022 — en anglais. Survol concis de l’ensemble du langage (C++20), pour les personnes qui programment déjà.
- Marc Gregoire, *[Professional C++](https://www.wiley.com/en-us/Professional+C%2B%2B%2C+6th+Edition-p-9781394193172)*, 6ᵉ éd., Wiley, 2024 — en anglais. Ouvrage de référence complet, à jour avec C++23, qui accorde une large place à la conception orientée objet.
- Nicolai M. Josuttis, *[C++17 – The Complete Guide](https://www.cppstd17.com/)*, 2019 — en anglais. Toutes les nouveautés de la norme C++17, celle du cours.
- Claude Delannoy, *Programmer en langage C++*, 9ᵉ éd., Eyrolles, 2017 — en français. Manuel classique qui couvre C++11, C++14 et C++17.

Pour savoir si un ouvrage est accessible en ligne ou peut être emprunté, consultez la [Bibliothèque de la TÉLUQ](https://bibliotheque.teluq.ca/).
