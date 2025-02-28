---
title: Moissonnage du Web avec R
slug: webscrapingfr
execute:
  cache: false
  error: true
format: hugo-md
---

**16 février 2023, 13h30 à 14h50 HNE**

**Présenté par**: Pier-Luc St-Onge

**Durée**: 80 minutes

**Description**: Internet est non seulement un trésor riche en informations, mais une grande portion y est
accessible publiquement, ce qui est propice à une utilisation pour la recherche. Cependant, extraire
l'information de pages Web et la formater pour analyse peut rapidement devenir une tâche fastidieuse. Les
outils de moissonnage du Web permettent d'automatiser en partie ce processus et le langage R est populaire
pour réaliser cette tâche. Dans cet atelier, nous allons donc vous guider à travers un exemple simple
utilisant le module rvest.

Inscrivez-vous <a href="https://www.eventbrite.ca/e/512943125697" target="_blank">ici</a>

The same workshop [in English](/webscraping).

#### Biographie

Diplômé au baccalauréat et à la maîtrise en génie logiciel et génie informatique, **Pier-Luc St-Onge** a
travaillé pendant cinq ans pour différents laboratoires de recherche avant de rejoindre Calcul Québec en
mai 2013. Dans son projet de recherche, il s'était spécialisé en vision par ordinateur avec OpenCV. À Calcul
Québec, il fait partie de l'équipe d'analystes offrant du soutien aux utilisateurs des ressources de calcul.

{{<br>}}

------------------------------------------------------------------------

## À propos

Le matériel ci-dessous est une traduction et adaptation du matériel original
<a href="https://mint.westdri.ca/r/webscraping.html" target="_blank"><em>Web scraping with R</em></a>
de Marie-Hélène Burle sur le
<a href="https://mint.westdri.ca/" target="_blank">site d’ateliers de WestDRI</a>.

Pour cet atelier, nous allons utiliser un serveur RStudio éphémère.
Pour y accéder, il faut se connecter à un portail JupyterHub;
les détails sont donnés en atelier.

Le serveur RStudio est déjà configuré avec les deux modules suivants :

-   <a href="https://cran.r-project.org/web/packages/rvest/index.html" target="_blank">rvest</a>
-   <a href="https://cran.r-project.org/web/packages/tibble/index.html" target="_blank">tibble</a>

Si vous préférez exécuter les exemples sur votre propre ordinateur,
vous devez les installer avec `install.packages()`.

## Introduction

### HTML et CSS

Le <a href="https://fr.wikipedia.org/wiki/Hypertext_Markup_Language" target="_blank"><em>HyperText Markup Language</em></a>
(ou HTML) est le langage de balisage standard pour représenter des pages Web.
Il permet, entre autres, d'encoder la structure d'une page Web et
le formatage de son contenu.
Pour ce qui est des règles de formatage réutilisées par plusieurs
pages HTML, il est possible de les sauvegarder dans des fichiers
<a href="https://fr.wikipedia.org/wiki/Feuilles_de_style_en_cascade" target="_blank"><em>Cascading Style Sheets</em></a>
(ou CSS).

Le HTML utilise des balises de la forme suivante :

``` html
<balise>Du contenu</balise>
```

Certaines balises ont aussi des attributs :

``` html
<balise nom_attribut="valeur attribut">Du contenu</balise>
```

{{<ex>}}
Exemples réels :
{{</ex>}}

Structure du site :

``` html
<h2 id="ancre">Ceci est un titre de niveau 2</h2>
<p>Ceci est un paragraphe. Cliquez ce
  <a href="https://une.adresse/page.html#ancre">lien</a>.
</p>
```

Formatage :

``` html
<p class="texte_rouge">
  <strong>Pour du texte en caractères gras</strong>
</p>
```

### Moissonnage du Web

Le moissonnage du Web consiste à utiliser un ensemble d'outils afin
d'extraire automatiquement de l'information directement d'Internet.

Alors que la plupart des données sur Internet sont disponibles
publiquement, il peut être illégal de moissonner certains sites.
En effet, vous devriez toujours regarder la politique d'utilisation d'un
site Web avant de tenter toute extraction d'information par moissonnage.
Notez aussi que certains sites peuvent vous bloquer si vous leur envoyez
un trop grand nombre de requêtes HTTP dans une courte période de temps.
Par conséquent, si vous planifiez effectuer du moissonnage à grande
échelle, vous devriez considérer l'utilisation du module R
<a href="https://dmi3kno.github.io/polite/" target="_blank"><code>polite</code></a>.

### Un site Web en exemple

Nous allons utiliser
<a href="https://trace.tennessee.edu/utk_graddiss/index.html" target="_blank"><strong>ce site Web</strong></a>
de <a href="https://www.utk.edu/" target="_blank">l’Université du Tennessee</a>,
car il présente une interface de base de données
dont le code HTML est facile à décortiquer.
**Notre objectif consiste donc à extraire de ce site la date de publication,
le département de recherche et le nom du directeur ou de la directrice de
recherche pour chacune des thèses de doctorat de cette université.**
Ces informations doivent ensuite être colligées dans un *data frame*.

> Note : pour cet atelier, nous nous limiterons à la première
> page qui contient les liens des 100 thèses les plus récentes.
> Si vous vouliez extraire les données de toutes les thèses, il vous
> faudrait envoyer une requête HTTP pour chaque page de la base de données.

## Méthodologie

Avant de se lancer dans la programmation, il est recommandé
de réfléchir aux grandes étapes de notre moissonnage.
Étant donné la structure du site Web, la création du *data frame* avec
les données des thèses de la première page se fera en deux étapes :

1.  À partir de
    <a href="https://trace.tennessee.edu/utk_graddiss/index.html" target="_blank">la première page</a>
    de la base de données, nous voulons colliger une liste
    d'hyperliens menant vers les pages de chaque thèse.
2.  Avec ces hyperliens, nous voulons moissonner les pages
    correspondantes afin d'y extraire la valeur des champs
    *Date of Award*, *Major* et *Major Professor* de chaque thèse.

### Utiliser un module R spécialisé

Pour les deux grandes étapes ci-dessus, nous allons utiliser le module R
<a href="https://cran.r-project.org/web/packages/rvest/index.html" target="_blank"><code>rvest</code></a>
qui fait partie du <a href="https://www.tidyverse.org/" target="_blank">tidyverse</a>,
un ensemble moderne de modules R.
Il s'agit d'un module influencé par le populaire module Python
<a href="https://en.wikipedia.org/wiki/Beautiful_Soup_(HTML_parser)" target="_blank">Beautiful Soup</a>
et qui facilite le moissonnage du Web via le langage R.

Chargeons-le dans notre session R :

``` r
library(rvest)
```

### Obtenir les données HTML brutes

Tel que mentionné ci-dessus, notre site en exemple est la
<a href="https://trace.tennessee.edu/utk_graddiss/index.html" target="_blank">base de données de thèses de doctorat</a>
de l'Université du Tennessee.

Assignons l'adresse du site (une chaîne de caractères) à une variable :

``` r
adresse <- "https://trace.tennessee.edu/utk_graddiss/index.html"
```

L'étape suivante consiste à obtenir les données HTML de cette page :

``` r
html <- read_html(adresse)
```

Regardons un aperçu de ces données HTML encore à l'état brut :

``` r
html
```

## Extraction des données pertinentes

### Inspection du code HTML

Le code HTML contient bel et bien les données qui nous intéressent,
mais elles sont mélangées avec plusieurs balises HTML, des instructions
de formatage et d'autres données inutiles pour notre objectif.
Nous devons donc extraire ces données et les regrouper dans un format pratique.

La première étape consiste à trouver les branches de balises,
souvent enrichies de [sélecteurs CSS](#points-à-retenir),
qui contiennent les données que nous voulons.
Pour ce faire, vous pouvez utiliser l'inspecteur intégré
de votre navigateur Web sur la page de thèses.
Par exemple, en pointant un hyperlien avec la souris :

-   **Firefox** : bouton droit de la souris et *Inspecter*
    -   L'arborescence se trouve au bas de la fenêtre
-   **Google Chrome** : bouton droit de la souris et *Inspecter*
    -   L'arborescence se trouve à la droite de la fenêtre
-   **Microsoft Edge** : bouton droit de la souris et *Inspecter*
    -   L'arborescence se trouve à la droite de la fenêtre
-   **Safari** : bouton droit de la souris et *Inspecter l'élément*
    -   Note: il faut au préalable activer le menu *Développement* dans les
        paramètres avancés.

> Voir aussi le <a href="https://selectorgadget.com/" target="_blank">SelectorGadget</a>.

On remarque donc que toutes les adresses qui nous intéressent se trouvent
dans l'attribut `href` des balises `<a>` qui sont elles-même dans des
paragraphes `<p>` dont la classe CSS porte le nom `article-listing`.

### Extraction d'une seule adresse

Puisqu'il est recommandé de tester l'extraction d'information sur
un seul élément avant d'effectuer un moissonnage sur toute la page,
essayons uniquement d'obtenir l'adresse de la première thèse.

La fonction `html_element()` du module `rvest` retourne le premier
élément HTML qui correspond aux sélecteurs CSS donnés en paramètre.
Pour les paragraphes `<p>` de classe `article-listing`, nous ferons une
recherche avec `p.article-listing` et sauvegarderons le résultat dans `test`.

``` r
test <- html %>% html_element("p.article-listing")
```

> Note : `%>%` est un opérateur de redirection du module tidyverse
> <a href="https://magrittr.tidyverse.org/" target="_blank">magrittr</a>.
> Cet opérateur transmet l'objet résultant de l'expression de gauche
> à l'appel de fonction de droite comme premier argument.
> En fait, nous aurions pu écrire `html_element(html, "p.article-listing")`,
> mais l'opérateur `%>%` permet d'enchaîner élégamment
> plusieurs appels similaires.

Affichons l'objet obtenu qui représente le paragraphe sélectionné :

``` r
test
```

L'adresse voulue s'y trouve, donc nous avons isolé le bon élément.
Cependant, nous devons poursuivre le nettoyage de notre extraction.

Comme vous pouvez le voir dans l'affichage de `test`,
l'adresse se trouve dans un élément `<a>`.
Utilisons à nouveau `html_element()`, mais avec `"a"` seulement :

``` r
test_a <- test %>% html_element("a")
test_a
```

> Note : nous aurions pu utiliser la fonction `html_children()`
> pour aller chercher les éléments enfant du paragraphe :
> `test %>% html_children()`.
> Par contre, il y a un risque d'obtenir une liste de plusieurs éléments.

Finalement, à partir de ce dernier objet,
nous pouvons extraire la valeur de l'attribut `href` :

``` r
test_addr <- test_a %>% html_attr("href")
test_addr
```

C'est bien l'adresse voulue et elle est stockée en mémoire
sous la forme d'une chaîne de caractères, ce qui est parfait!

### Extraire les données de la page de thèse

Maintenant que nous avons l'adresse de la page d'information de la
première thèse, nous voulons extraire la date de publication, le département
de recherche et le nom du directeur ou de la directrice de recherche.

Nous venons de voir que `test_addr` est une chaîne de caractères
représentant une adresse et nous savons comment l'utiliser.
Comme nous avions fait pour la page de la base de données, nous allons
lire les données HTML brutes et les assigner à une nouvelle variable :

``` r
test_html <- read_html(test_addr)
test_html
```

Maintenant, nous voulons extraire la date de publication :

-   Celle-ci se trouve dans une balise `<p>` dont le parent est identifié par
    `#publication_date`. Or, la syntaxe du sélecteur nous permet d'isoler
    directement le paragraphe enfant en utilisant `#publication_date p`.
-   Ensuite, à partir de la sortie de `html_element()`,
    au lieu d'aller chercher la valeur d'un attribut,
    nous voulons plutôt extraire le texte de notre paragraphe.
    Dans ce cas, nous devons utiliser la fonction `html_text2()` qui
    extrait le texte et ajoute des sauts de ligne `\n` lorsque requis.

``` r
test_date <- test_html %>% html_element("#publication_date p") %>% html_text2()
```

> Note : dans la page de la base de données, si nous avions utilisé
> `html_text2()` au lieu de `html_attr("href")`, nous aurions eu
> le texte de l'hyperlien, c'est-à-dire le titre de la thèse.

Vérifions maintenant le contenu de notre date (de format `"M-AAAA"`) :

``` r
test_date
```

Nous pouvons utiliser la même méthode pour extraire le département de
recherche, sauf que nous devons utiliser le sélecteur `#department p` :

``` r
test_department <- test_html %>% html_element("#department p") %>% html_text2()
test_department
```

Enfin, pour le nom du directeur ou de la directrice de recherche,
nous devons utiliser le sélecteur `#advisor1 p` :

``` r
test_direction <- test_html %>% html_element("#advisor1 p") %>% html_text2()
test_direction
```

{{<ex>}}
Exercice - Extraire le titre "Abstract" et le texte de tous ses paragraphes
{{</ex>}}

Voici la solution attendue, soit une seule longue chaîne de caractères :

    [1] "Abstract\n\n..."

Maintenant que nous avons nos trois informations, nous pouvons créer un tuple
avec ces trois valeurs en les passant comme arguments à la fonction `cbind()` :

``` r
test_resultat <- cbind(test_date, test_department, test_direction)
test_resultat
```

### Extraire toutes les adresses

Maintenant que nous avons testé notre code sur la première thèse, nous pouvons
l'utiliser sur les 100 thèses de la première page de la base de données.
Or, au lieu d'utiliser `html_element()`, nous allons utiliser `html_elements()`
pour extraire *tous* les éléments qui correspondent au sélecteur :

``` r
les_p <- html %>% html_elements("p.article-listing")
les_p
```

``` r
typeof(les_p)
length(les_p)
les_p[[2]]
```

Pour extraire la liste de toutes les adresses, nous allons utiliser
une boucle qui va refaire les étapes que nous avons faites pour la
[première thèse](#extraction-dune-seule-adresse).
Mais avant de lancer la boucle, il est important d'initialiser cette liste
d'adresses, ce qui est plus efficace que de l'allonger à chaque itération :

``` r
liste_addr <- vector("list", length(les_p))
```

Et si on regarde l'un des éléments de la liste (le deuxième, par exemple) :

``` r
liste_addr[[2]]
```

Nous pouvons maintenant exécuter notre boucle pour noter les adresses :

``` r
for (i in seq_along(les_p)) {
  liste_addr[[i]] <- les_p[[i]] %>% html_element("a") %>% html_attr("href")
}
```

Affichons à nouveau le second élément de notre liste pour vérifier :

``` r
liste_addr[[2]]
```

Nous obtenons donc l'adresse sous la forme de chaîne de caractères.
Ainsi, `liste_addr` est bel et bien une liste d'adresses telle qu'attendue.

### Extraire les données des 100 thèses

Nous allons maintenant extraire les données (date, département et nom)
pour chaque adresse dans notre liste.
Encore une fois, avant de lancer la boucle principale,
il est préférable d'initialiser notre liste :

``` r
liste_donnees <- vector("list", length(liste_addr))
```

La boucle suivante contient essentiellement toutes les étapes que nous avons
testées deux sections plus haut. Le tuple généré à chaque itération est stocké
dans notre `liste_donnees` qui contiendra les informations des 100 thèses.
Finalement, pour éviter de se faire bloquer par le site Web, chaque itération
fera une courte pause de 0.1 seconde avant de lancer une nouvelle requête HTTP.

``` r
for (i in seq_along(liste_addr)) {
  html <- read_html(liste_addr[[i]])

  date <- html %>% html_element("#publication_date p") %>% html_text2()
  dept <- html %>% html_element("#department p") %>% html_text2()
  nom <- html %>% html_element("#advisor1 p") %>% html_text2()

  liste_donnees[[i]] <- cbind(date, dept, nom)
  Sys.sleep(0.1)  # Une courte pause de 0.1 seconde
}
```

Affichons le deuxième tuple pour vérifier que le moissonnage est complété :

``` r
liste_donnees[[2]]
```

Tout semble normal. Il reste à transformer la liste en *data frame* :

``` r
resultat <- do.call(rbind.data.frame, liste_donnees)
```

L'objet `resultat` est un long *data frame* de 100 enregistrements,
alors affichons uniquement les quelques premiers enregistrements :

``` r
head(resultat)
```

Le *data frame* peut aussi être converti en objet *tibble* :

``` r
resultat <- resultat %>% tibble::as_tibble()
```

> Note : la notation `tibble::as_tibble()` veut dire que
> nous utilisons la fonction `as_tibble()` du module R
> <a href="https://tibble.tidyverse.org/" target="_blank">tibble</a>.
> Un *tibble* est la version
> <a href="https://www.tidyverse.org/" target="_blank">tidyverse</a>
> d'un *data frame*. Un de ses avantages est d'afficher seulement
> 10 rangées par défaut au lieu d'afficher toutes les rangées,
> ce qui nous évite de devoir utiliser la fonction `head()`.

``` r
resultat
```

On peut aussi renommer facilement les entêtes de colonne :

``` r
names(resultat) <- c("Date", "Département", "Nom")
```

Et voici le résultat final :

``` r
resultat
```

## Points à retenir

**Les sélecteurs CSS :**

| Sélecteurs      | Recherche pour ...                                         |
|---------------------------------|---------------------------------------|
| `balise`        | Tous les éléments de ce type de balise                     |
| `.classe`       | Tous les éléments ayant cette classe                       |
| `balise.classe` | Tous les éléments de ce type de balise ayant cette classe  |
| `#identifiant`  | L'élément ayant cet identifiant unique                     |
| `#id balise`    | Tous les éléments de ce type de balise avec le parent `id` |

-   Référence :
    <a href="https://www.w3.org/TR/selectors/#overview" target="_blank">W3C - Selectors</a>

**Les fonctions du module `rvest` :**

| Fonctions         | Pour obtenir ...                            |
|-------------------|---------------------------------------------|
| `html_attr()`     | La valeur d'un attribut                     |
| `html_children()` | Les éléments enfant                         |
| `html_element()`  | Le premier élément selon les sélecteurs CSS |
| `html_elements()` | Tous les éléments selon les sélecteurs CSS  |
| `html_text2()`    | Le texte de l'élément                       |
| `read_html()`     | Le code HTML d'une page                     |

-   Référence :
    <a href="https://rvest.tidyverse.org/reference/index.html" target="_blank">rvest - Function reference</a>

<br>
{{< youtube qjdTQt371MI >}}
