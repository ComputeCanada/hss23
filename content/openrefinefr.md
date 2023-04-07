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

-----

## Préparation pour l'atelier

Les instructions ci-dessous proviennent de l'atelier
[Data Carpentry: OpenRefine for Social Science Data](https://datacarpentry.org/openrefine-socialsci/setup.html).

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
[SAFI_openrefine.csv](https://ndownloader.figshare.com/files/11502815).
* **Notez bien l'endroit** où vous avez sauvegardé ce fichier dans votre
  ordinateur, car il faudra le charger dans OpenRefine pendant l'atelier.
* **À propos des données** : ce fichier est tiré du tutoriel Data Carpentry.
  Il est conçu pour l'enseignement, c'est-à-dire que son contenu est
  une version réduite et intentionnellement modifiée de la base de données
  du projet *Studying African Farmer-Led Irrigation (SAFI)*.

## Tutoriel Data Carpentry

Cet atelier est une version écourtée du tutoriel en ligne
[OpenRefine for Social Science Data](https://datacarpentry.org/openrefine-socialsci/).

Les chapitres et les concepts d'OpenRefine que nous verrons
sont listés dans les sections ci-dessous.

## 1- Introduction à OpenRefine
=> [Matériel Data Carpentry - Chapitre 1](https://datacarpentry.org/openrefine-socialsci/01-introduction/index.html)

* Pourquoi un atelier sur OpenRefine?
  * Faciliter le nettoyage des données
  * Reproduire et publier la méthode
* Qu'est-ce que OpenRefine?
  * Application locale via un navigateur Web
  * Préservation des données brutes
  * Aperçu des données
  * Trouver et résoudre des inconsistences
  * Division de valeurs multiples
  * Fusion avec des données externes
  * Annulation d'opérations au besoin
  * Réutilisation de recette de nettoyage

## 2. Travailler avec OpenRefine

=> [Matériel Data Carpentry - Chapitre 2](https://datacarpentry.org/openrefine-socialsci/02-working-with-openrefine/index.html)

### Création d'un projet

* Démarrage d'OpenRefine
* Importation d'un fichier
  ([Image](https://datacarpentry.org/OpenRefine-ecology-lesson/fig/openrefine-create-project.png))
  * Formats pris en charge :
    CSV, TSV, Excel (xls, xlsx), JSON, XML, Google Spreadsheets.
* Valider la séparation des colonnes
  ([Image](https://datacarpentry.org/openrefine-socialsci/fig/OR_01_parse_options.png))
  * Nettoyer les espaces de début et de fin

### Facettes de données

* Regrouper des enregistrements selon les valeurs d'une colonne
* *Text facet* sur la colonne `village`
  ([Aperçu des options](https://datacarpentry.org/OpenRefine-ecology-lesson/fig/ORFacetMenu.png))
  * Tri par le nom et le décompte
    ([Exemple de facette](https://datacarpentry.org/OpenRefine-ecology-lesson/fig/ORFacetedScientificName.png))
  * Édition d'un groupe de valeurs
* Facettes numériques, de dates et heures, personnalisées
* **Exercice en groupe**
  * Trouver le nombre de différentes `interview_date` avec une facette
  * Convertir en dates : `Edit cells` > `Common transforms` > `To date`
  * Trouver la période ayant le plus d'enregistrements avec `Timeline facet`

Référence : https://docs.openrefine.org/manual/facets

### Grappes de valeurs semblables

* Facette textuelle de `village` => Bouton `Cluster`
* Méthode `key collision` et clé de fonction `metaphone3`
  ([Exemple d'analyse](https://datacarpentry.org/OpenRefine-ecology-lesson/fig/openrefine-clustering.png))
* Activer la fusion des valeurs, fusionner et refaire le calcul des grappes
* Test d'autres [méthodes et clés de fonction](https://openrefine.org/docs/manual/cellediting#clustering-methods)
* Corrections manuelles lorsqu'aucune grappe ne se trouve facilement

Référence : https://openrefine.org/docs/manual/cellediting#cluster-and-edit

### Transformation des données avec GREL

* Colonne `items_owned` > `Edit Cells` > `Transform...`
  ([Image](https://datacarpentry.org/openrefine-socialsci/fig/OR_02_Transform.png))
  * `value.replace("[", "")` et OK
* **Exercice en groupe**
  * Répéter avec `value.replace("]", "")`, `value.replace("'", "")` et
    `value.replace(" ", "")`
* Colonne `items_owned` > `Facet` > `Custom text facet...`
  * Expression : `value.split(";")`
* Cliquer sur l'onglet `Undo / Redo`, voir les changements
  * En annuler et tous les refaire

## 3. Filtrer avec OpenRefine

=> [Matériel Data Carpentry - Chapitre 3](https://datacarpentry.org/openrefine-socialsci/03-filter-sort/index.html)

Note : puisque le tri peut se faire via les facettes,
nous sauterons les sections à ce sujet.

* Filtre de texte
  * Colonne `respondent_roof_type` > `Text filter`
  * **Exercice en groupe**
    * Tenter une sélection avec `mabat`
    * Observer la table et la facette
    * Modifier la vue pour avoir jusqu'à 50 rangées
    * Rajouter deux lettres (`ip`, par exemple)
    * Remettre à `mabat`
* Inclusion et exclusion des valeurs sur les facettes
  * Vis-à-vis une des deux valeurs, cliquer sur `include`
  * Noter le nombre de rangées qui change
  * Tester différents `include` / `exclude`, cliquer sur une valeur
* Facette == aperçu, filtre == sélection

## 4. Examiner les nombres

=> [Matériel Data Carpentry - Chapitre 4](https://datacarpentry.org/openrefine-socialsci/04-numbers/index.html)

* Gestion des nombres
  * Enlever toutes les facettes de texte
  * Colonne `years_farm` > `Edit cells` > `Commont Transforms...` > `To number`
  * **Exercice en groupe**
    * Transformer `no_membrs`, `years_liv`, `buildings_in_compound`
      et `villange` en nombres
    * Cliquer sur l'onglet `Undo / Redo` et voir les changements
* Facette numérique
  * Colonne `gps_Altitude` > `Facet` > `Numeric Facet`
  * Trier dans la facette pour identifier les valeurs manquantes
  * **Exercice en groupe**
    * Colonne `years_liv` :
      * Remplacer un nombre par `abc`
      * Remplacer un autre nombre par rien (laisser vide)
    * Obtenir une facette numérique sur la colonne
    * Activer et désactiver la vue des valeurs
      `Numeric`, `Non-numeric`, `Blank` et `Error`
    * Fermer la facette
    * Annuler tous ces derniers changements dans `Undo / Redo`

## 5. Réutiliser les étapes de nettoyage

=> [Matériel Data Carpentry - Chapitre 5](https://datacarpentry.org/openrefine-socialsci/05-scripts/index.html)

* Exporter les transformations
  ([Image](https://datacarpentry.org/openrefine-socialsci/fig/history.png))
  * `Undo / Redo` > `Extract ...` > Sélection des étapes
  * Copier le code dans un éditeur texte et sauvegarder (fichier `*.txt`)
* Importer les transformations
  * Démarrer un nouveau projet (nouveau nom), même fichier CSV
  * `Undo / Redo` > `Apply` > Coller le contenu du fichier `*.txt`
  * Cliquer sur `Perform operations`; valider le nettoyage
* Science reproductible
  * [Gestion des changements](https://swcarpentry.github.io/git-novice/)
    du fichier `*.txt`
  * Publication des données et des étapes de changement

## 6. Exporter les données et le projet

=> [Matériel Data Carpentry - Chapitre 6](https://datacarpentry.org/openrefine-socialsci/06-saving/index.html)

* Exporter les données nettoyées
  * `Export` > choix du type de fichier (TSV ou CSV)
  * Comme le téléchargement d'un fichier `*.tsv` ou `*.csv`
* Sauvegarde automatique du projet
* Exporter un projet - `Export` > `OpenRefine project archive to file`
  * Comme le téléchargement d'un fichier `*.tar.gz`
  * Contient un dossier `history` pour les données transformées
    et un fichier `data.zip` contenant les données initiales.
  * Importation via `Open...` > `Import Project` > fichier `*.tar.gz`

### 7. Ressources supplémentaires

=> [Matériel Data Carpentry - Chapitre 7](https://datacarpentry.org/openrefine-socialsci/07-resources/index.html)

<br>
{{< youtube ByP9qHav9Gw >}}
