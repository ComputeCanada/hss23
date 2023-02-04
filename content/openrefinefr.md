+++
title = "Introduction à OpenRefine"
slug = "openrefinefr"
+++
**14 février 2023, 15h à 16h20 HNE**

**Présenté par**: Pier-Luc St-Onge

**Durée**: 80 minutes

**Description**: Un essentiel pour les personnes spécialisées en sciences humaines et sociales, ainsi que pour
les professionnels des bibliothèques et de l’information, cet atelier adapté de Data Carpentry est une
introduction au nettoyage des données avec OpenRefine. Ce puissant outil peut être utilisé pour uniformiser et
nettoyer des fichiers de données tabulaires, que ce soit en format CSV (séparation par des virgules) ou TSV
(séparation par des espaces de tabulation). Il permet de réaliser un diagnostic de l’état des données, de
résoudre des inconsistances, de subdiviser certains champs contenant une séquence de valeurs, etc. À la fin de
cet atelier, vous devriez avoir une bonne idée de ce que OpenRefine permet de faire et de comment l’utiliser
pour vos fichiers de données. Aucune expérience préalable n’est requise.

**Prérequis techniques**: Les participantes et participants devront installer
Java et OpenRefine sur leur ordinateur.
Les [**instructions d'installation**](#préparation-pour-latelier) se trouvent
dans une section du matériel ci-dessous et seront aussi fournies par courriel.

Inscrivez-vous {{<a "https://www.eventbrite.ca/e/510901348687" "ici">}}

The same workshop [in English](/openrefine).

#### Biographie

Diplômé au baccalauréat et à la maîtrise en génie logiciel et génie informatique, **Pier-Luc St-Onge** a
travaillé pendant cinq ans pour différents laboratoires de recherche avant de rejoindre Calcul Québec en
mai 2013. Dans son projet de recherche, il s’était spécialisé en vision par ordinateur avec OpenCV. À Calcul
Québec, il fait partie de l’équipe d’analystes offrant du soutien aux utilisateurs des ressources de calcul.

<!-- {{< vimeo 690948795 >}} -->
<!-- <br> -->

<!-- - [Watch this session on Vimeo](https://vimeo.com/690948795) -->
-----

## Préparation pour l'atelier

Les instructions ci-dessous proviennent de l'atelier
[Data Carpentry: Data Cleaning with OpenRefine for Ecologists](https://datacarpentry.org/OpenRefine-ecology-lesson/setup.html).

### Installation

1. Télécharger OpenRefine
   [ici](https://openrefine.org/download.html)
2. Si Java n'est pas inclus avec l'installateur d'OpenRefine, il faudra
   [installer cette dépendance](https://openrefine.org/docs/manual/installing#system-requirements).
3. Installer OpenRefine selon les instructions
   [ici](https://openrefine.org/docs/manual/installing#installing-or-upgrading).

Veuillez nous demander de l'aide sur Slack si vous avez des problèmes avec
ces étapes d'installation.

### Les données

Pour cet atelier, nous utiliserons ce fichier CSV :
[Portal_rodents_19772002_scinameUUIDs.csv](https://ndownloader.figshare.com/files/7823341).
* **Notez bien l'endroit** où vous avez sauvegardé ce fichier dans votre
  ordinateur, car il faudra le charger dans OpenRefine pendant l'atelier.
* **À propos des données** : ce fichier est tiré du tutoriel Data Carpentry.
  Il est conçu pour l'enseignement, c'est-à-dire que son contenu est
  une version réduite et intentionnellement modifiée du
  [Portal Project Teaching Database](https://figshare.com/articles/dataset/Portal_Project_Teaching_Database/1314459).

## Tutoriel Data Carpentry

Cet atelier est une version écourtée du tutoriel en ligne
[Data Cleaning with OpenRefine for Ecologists](https://datacarpentry.org/OpenRefine-ecology-lesson/).

Les chapitres et les concepts d'OpenRefine que nous verrons sont :

### 1- Introduction à OpenRefine
=> [Matériel Data Carpentry - Chapitre 1](https://datacarpentry.org/OpenRefine-ecology-lesson/01-getting-started/index.html)

* Pourquoi un atelier sur OpenRefine?
  * Faciliter le nettoyage des données
  * Reproduire et publier la méthode
* Qu'est-ce que OpenRefine?
  * Application locale via un navigateur Web
  * Préservation des données brutes
  * Aperçu des données
  * Résoudre des inconsistences
  * Division de valeurs multiples
  * Fusion avec des données externes
  * Annulation d'opérations au besoin
  * Réutilisation de recette de nettoyage

### 2. Exploration des données

=> [Matériel Data Carpentry - Chapitre 2](https://datacarpentry.org/OpenRefine-ecology-lesson/02-exploring-data/index.html)

* Création d'un projet
  * Démarrage d'OpenRefine
  * Importation d'un fichier
    ([Image](https://datacarpentry.org/OpenRefine-ecology-lesson/fig/openrefine-create-project.png))
    * Formats pris en charge :
      CSV, TSV, Excel (xls, xlsx), JSON, XML, Google Spreadsheets.
  * Valider la séparation des colonnes
    ([Image](https://datacarpentry.org/OpenRefine-ecology-lesson/fig/openrefine-data-import.png))
* Facettes de données ([Référence](https://docs.openrefine.org/manual/facets))
  * Regrouper des enregistrements selon les valeurs d'une colonne
  * *Text facet*
    ([Image](https://datacarpentry.org/OpenRefine-ecology-lesson/fig/ORFacetMenu.png))
    * Tri par le nom et le décompte
    * Édition d'un groupe de valeurs
  * Facettes numériques, de dates et heures, personnalisées
  * **Exercice en groupe**
    * Trouver le nombre d'années différentes avec une facette
    * Trouver les années ayant le plus et le moins d'enregistrement
    * Changer le format de `yr` en valeurs numériques
      et obtenir une facette numérique.
