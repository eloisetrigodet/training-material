---
layout: tutoriel de prise en mains
topic_name: formation
tutorial_name: créer un nouveau tutoriel de circuit interactif
---

# Introduction
{:.no_toc}

Galaxy est une excellente solution pour former aux concepts de la bio-informatique.

- de nombreux outils de bioinformatique sont disponibles (près de 5000 dans le ToolShed)
- il peut être utilisé par des personnes qui n'ont pas de compétences particulières en informatique
- il forme à utiliser ces outils, en décrivant les moyens et les efforts mis en oeuvre pour les rendre accessibles aux 
  chercheurs
- il est évolutif

En 2016, le galaxy Training Network décide de mettre en place une nouvelle infrastructure pour fournir facilement du matériel de formation Galaxy. L'idée était de développer quelque chose d'ouvert et en ligne basé sur un effort de la communauté, comme la plupart du temps dans Galaxy.

Nous nous inspirons de [Software Carpentry](https://software-carpentry.org). Nous avons tout rassembler sur un répertoire GitHub: [https://github.com/galaxyproject/training-material ](https://github.com/galaxyproject/training-material). Nous avons choisi une structure basée sur des tutoriels pratiques adaptées à la fois à l'auto-apprentissage en ligne et aux ateliers regroupés en thèmes. Chaque tutoriel suit la même structure et dispose d'un support technique pour pouvoir s'exécuter.

Dans ce tutoriel, vous comprendrez comment concevoir et développer un nouveau tutoriel dans ce répertoire de matériel de formation.
Comme cela aide à comprendre, nous développerons un petit tutoriel pour expliquer BLAST avec l'infrastructure complète pour pouvoir exécuter ce tutoriel n'importe où.

> ### Agenda
>
> Dans ce tutoriel nous traiterons de: 
>
> 1. TOC
> {:toc}
>
{: .agenda}

# Un circuit interactif sur Galaxy

Un circuit interactif sur Galaxy est un moyen de parcourir une analyse complète, étape par étape, à l'intérieur de Galaxy, d'une manière interactive et exploratoire pédagogique d'exécuter le didacticiel directement à l'intérieur de Galaxy. 

![Demonstration d'un circuit interactif](../../../dev/images/galaxy_tour_demo.gif "Demonstration d'un tour interactif")

Un tour est un fichier YAML comme: 

```
id: galaxy_iu
name: Galaxy IU
description: Une introduction à l'interface utilisateur Galaxy
title_default: "Bienvenue dans Galaxy"

steps:
    - title: "Bienvenue dans Galaxy"
      content: "Ce cours circuit vous guidera dans l'interface utilisateur de Galaxy.<br>
                Vous pouvez naviguer avec vos touches directionnelles et quitter le circuit à  
                nimporte quel moment avec 'échapper' ou le bouton 'fin de circuit'.
      backdrop: vrai

    - title: "télécharger vos données"
      element: ".upload-button"
      intro: "Galaxy prend en charge de nombreuses façons d'obtenir vos données.<br>
              Utiliser ce bouton pour télécharger vos données."
      position: "droite"
      postclick:
        - ".upload-button"
```

- en haut des métadonnées liées au circuit:
    - `id`: ID du circuit
    - `name`: nom du circuit
    - `description`: une courte description du circuit
    - `title_default`: un titre
- plusieurs étapes correpondantes à différentes boites

   Chaque étape commence par un tiret `-` et avec des arguments possibles

    Argument | Description
    ---  | ---
    `title`  | En-tête de chaque conteneur-étape
    `content` | Texte qui s'affiche à l'utilisateur
    `element` | [JQuery Selector](https://api.jquery.com/category/selectors/) de l'élément que vous voulez décrire / click
    `placement` | Placement de la zone de texte par rapport à l'élément sélectionné
    `preclick` or `postclick` | Les éléments qui reçoivent un événement click () avant (`preclick`) ou après (` postclick`), 
     l'étape est affichée
    `textinsert` | Pour insérer une zone de texte (ex recherche d'outils ou téléchargement)
    `backdrop` | `true/false`:  Affichez un fond sombre derrière le popover et son élément, mettant en évidence l'étape 
     actuelle
     
    [Référence complète des propriétés](https://bootstraptour.com/api/)

Le fichier YAML d'une visite peut être intégré dans une instance Galaxy en le plaçant dans le répertoire `config / plugins / tours` du code Galaxy et en redémarrant l'instance Galaxy.

# Créer un circuit interactif Galaxy

[Un plugin de navigateur Web](https://github.com/TailorDev/galaxy-tourbuilder) est disponible pour aider à la création et au test d'un circuit interactif.

<blockquote class="imgur-embed-pub" lang="en" data-id="a/0YVvz"><a href="//imgur.com/a/0YVvz">Galaxy Tour Builder by TailorDev</a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>

> ### :pencil2: Hands-on: Installer et démarrer le plugin
>
> 1. Installer [node.js](https://nodejs.org/en/)
> 2. Cloner le [plugin GitHub repository](https://github.com/TailorDev/galaxy-tourbuilder)
> 3. Lancer `npm install`
> 4. Lancer `npm run build`
> 5. Chargez l'extension dans votre navigateur web
>    - Charger l'extension dans Chrome & Opera
>       - Ouvrir Chrome/Opera et navigez avec chrome://extensions
>       - Sélectionner "Developer Mode" et clickez sur "Load unpacked extension..."
>       - Dans le navigateur de fichiers choisissez `galaxy-tourbuilder/build/chrome` ou (`galaxy-tourbuilder/build/opera`)
>    - Charger l'extension dans Firefox
>       - Ouvrir Firefox et naviguez avec about:debugging
>       - Cliquez sur "Load Temporary Add-on" et à partir du navigateur de fichiers, choississez `galaxy 
>         tourbuilder/build/firefox`
> 6. Charger la page web de toute instance de Galaxy
> 7. Démarrer le plugin en cliquant sur l'icône à droite
{: .hands_on}

Nous pouvons maintenant créer facilement un tour interactif galaxy et le tester.

> ### :pencil2: Hands-on: Créer un circuit interactif galaxy
>
> 1. Créez un circuit interactif Galaxy pour un tutoriel "BLAST"
> 2. Testez le avec le plugin
> 3. Copiez le contenu YAML et ajoutez le à un fichier
> 2. Ajoutez le fichier au répertoire `tours` du tutoriel
> 3. Le tester dans l'instance Galaxy local
{: .hands_on}

# Conclusion
{:.no_toc}

> ### Développer du matériel de formation GTN
>
> Ce tutoriel fait partie d'une série pour développer du matériel de formation GTN, n'hésitez pas à consulter:
>
> 1. [Rédaction de contenu en Markdown](../create-new-tutorial-content/tutorial.html)
> 1. [Définition des métadonnées](../create-new-tutorial-metadata/tutorial.html)
> 1. [Configuration de l'infrastructure](../create-new-tutorial-jekyll/tutorial.html)
> 1. [Création des circuits interactifs Galaxy](../create-new-tutorial-tours/tutorial.html)
> 1. [Construire un Docker flavor](../create-new-tutorial-docker/tutorial.html)
> 1. [Soumettre le nouveau tutoriel au dépôt GitHub](../../../dev/tutorials/github-contribution/slides.html)
{: .agenda}
