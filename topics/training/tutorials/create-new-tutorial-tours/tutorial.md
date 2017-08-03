---
layout: tutoriel de prise en mains
topic_name: formation
tutorial_name: créer un nouveau tutoriel de tour interactif
---

# Introduction
{:.no_toc}

Galaxy est une excellente solution pour former aux concepts de la bio-informatique.

- de nombreux outils de bioinformatique sont disponibles (près de 5000 dans le ToolShed)
- il peut être utilisé par des personnes qui n'ont pas de compétences particulières en informatique
- il forme à utiliser ces outils, en décrivant les moyens et les efforts mis en oeuvre pour les rendre accessibles aux chercheurs
- il est évolutif

En 2016, le galaxy Training Network décide de mettre en place une nouvelle infrastructure pour fournir facilement du matériel de formation Galaxy. L'idée était de développer quelque chose d'ouvert et en ligne basé sur un effort de la communauté, comme la plupart du temps dans Galaxy.

Nous nous inspirons de [Software Carpentry](https://software-carpentry.org). Nous avons tout rassembler sur un répertoire GitHub: [https://github.com/galaxyproject/training-material ](https://github.com/galaxyproject/training-material). Nous avons choisi une structure basée sur des didacticiels pratiques adaptées à la fois à l'auto-apprentissage en ligne et aux ateliers regroupés en thèmes. Chaque tutoriel suit la même structure et dispose d'un support technique pour pouvoir s'exécuter.

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

# Un tout interactif sur Galaxy

Un tour interactif sur Galaxy est un moyen de parcourir une analyse complète, étape par étape, à l'intérieur de Galaxy, d'une manière interactive et exploratoire pédagogique d'exécuter le didacticiel directement à l'intérieur de Galaxy. 

![Demonstration d'un tour interactif](../../../dev/images/galaxy_tour_demo.gif "Demonstration d'un tour interactif")

Un tour est un fichier YAML comme: 

```
id: galaxy_iu
name: Galaxy IU
description: Une introduction à l'interface utilisateur Galaxy
title_default: "Bienvenue dans Galaxy"

steps:
    - title: "Bienvenue dans Galaxy"
      content: "Ce courThis short tour will guide you through Galaxy's user interface.<br>
                Vous pouvez naviguer avec votre You can navigate with vos touches directionnelles et quitter le tour à  
                nimporte quel moment avec 'échapper' ou le bouton 'fin de tour'.
      backdrop: vrai

    - title: "télécharger vos données"
      element: ".upload-button"
      intro: "Galaxy prend en charge de nombreuses façons d'obtenir vos données.<br>
              Utiliser ce bouton pour télécharger vos données."
      position: "droite"
      postclick:
        - ".upload-button"
```

- en haut des métadonnées liées au tour:
    - `id`: ID du tour
    - `name`: nom du tour
    - `description`: une courte description du tour
    - `title_default`: un titre
- plusieurs étapes correpondantes à différentes boites

   Chaque étape commence par un tiret `-` et avec des arguments possibles

    Argument | Description
    ---  | ---
    `title`  | En-tête de chaque conteneur-étape
    `content` | Texte qui s'affiche à l'utilisateur
    `element` | [JQuery Selector](https://api.jquery.com/category/selectors/) of the element you want to describe / click
    `placement` | Placement of the text box relative to the selected element
    `preclick` or `postclick` | Elements that recieve a click() event before (`preclick`) or after (`postclick`) the step is shown
    `textinsert` | Text to insert if element is a text box (e.g. tool search or upload)
    `backdrop` | `true/false`:  Show a dark backdrop behind the popover and its element, highlighting the current step

    [Full reference of the properties](https://bootstraptour.com/api/)

The YAML file of a tour can be integrated in a Galaxy instance by placing the YAML file in the `config/plugins/tours` directory of the Galaxy code and restarting the Galaxy instance

# Creating a Galaxy Interactive Tour

[A Web browser plugin](https://github.com/TailorDev/galaxy-tourbuilder) is available to help the creation and the test (on the fly) of an interactive tour.

<blockquote class="imgur-embed-pub" lang="en" data-id="a/0YVvz"><a href="//imgur.com/a/0YVvz">Galaxy Tour Builder by TailorDev</a></blockquote><script async src="//s.imgur.com/min/embed.js" charset="utf-8"></script>

> ### :pencil2: Hands-on: Install and start the plugin
>
> 1. Install [node.js](https://nodejs.org/en/)
> 2. Clone the [plugin GitHub repository](https://github.com/TailorDev/galaxy-tourbuilder)
> 3. Run `npm install`
> 4. Run `npm run build`
> 5. Load the extension in your Web browser
>    - Load the extension in Chrome & Opera
>       - Open Chrome/Opera browser and navigate to chrome://extensions
>       - Select "Developer Mode" and then click "Load unpacked extension..."
>       - From the file browser, choose to `galaxy-tourbuilder/build/chrome` or (`galaxy-tourbuilder/build/opera`)
>    - Load the extension in Firefox
>       - Open Firefox browser and navigate to about:debugging
>       - Click "Load Temporary Add-on" and from the file browser, choose `galaxy-tourbuilder/build/firefox`
> 6. Load the webpage of any Galaxy instance
> 7. Start the plugin by clicking on the icon on the right
{: .hands_on}

We can now create easily a Galaxy Interactive Tour and test it on the fly.

> ### :pencil2: Hands-on: Create a Galaxy Interactive Tour
>
> 1. Create a Galaxy Interactive Tour for "BLAST" tutorial
> 2. Test it with the plugin
> 3. Copy the YAML content and add it to a file
> 2. Add the file to the `tours` directory of the tutorial
> 3. Test it on a local Galaxy instance
{: .hands_on}

# Conclusion
{:.no_toc}

> ### Developing GTN training material
>
> This tutorial is part of a series to develop GTN training material, feel free to also look at:
>
> 1. [Writing content in markdown](../create-new-tutorial-content/tutorial.html)
> 1. [Defining metadata](../create-new-tutorial-metadata/tutorial.html)
> 1. [Setting up the infrastructure](../create-new-tutorial-jekyll/tutorial.html)
> 1. [Creating Interactive Galaxy Tours](../create-new-tutorial-tours/tutorial.html)
> 1. [Building a Docker flavor](../create-new-tutorial-docker/tutorial.html)
> 1. [Submitting the new tutorial to the GitHub repository](../../../dev/tutorials/github-contribution/slides.html)
{: .agenda}
