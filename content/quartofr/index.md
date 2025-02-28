---
title: Créer des documents scientifiques dynamiques avec Markdown et Quarto
slug: quartofr
execute:
  error: true
format: hugo-md
---

**16 février 2023, 15h à 15h55 HNE**

**Présenté par**: Pier-Luc St-Onge

**Durée**: 55 minutes

**Description**: Cet atelier vous montrera comment créer aisément des documents scientifiques (page HTML, site
Web, document PDF, livre, etc.) constitués de textes formatés, de codes dynamiques et de figures, le tout à
partir de blocs de texte et de code. Pour ce faire, nous utiliserons Quarto, un outil à code ouvert combinant
la puissance de Jupyter ou knitr à celle de Pandoc.

**Prérequis techniques**: Les participantes et participants devront installer
Quarto, R, Python et quelques autres outils sur leur ordinateur.
Les [**instructions d'installation**](#installation) se trouvent dans une
section du matériel ci-dessous et seront aussi fournies par courriel.

Inscrivez-vous <a href="https://www.eventbrite.ca/e/510984316847" target="_blank">ici</a>

The same workshop [in English](/quarto).

#### Biographie

Diplômé au baccalauréat et à la maîtrise en génie logiciel et génie informatique, **Pier-Luc St-Onge** a
travaillé pendant cinq ans pour différents laboratoires de recherche avant de rejoindre Calcul Québec en
mai 2013. Dans son projet de recherche, il s'était spécialisé en vision par ordinateur avec OpenCV. À Calcul
Québec, il fait partie de l'équipe d'analystes offrant du soutien aux utilisateurs des ressources de calcul.

{{<br>}}

------------------------------------------------------------------------

## Le balisage et Markdown

### Langages de balisage

Les langages de balisage contrôlent le formatage de documents textuels.
Ils offrent plusieurs possibilités, mais en ajoutant un certain degré de complexité :
le texte à la source (avant qu'il soit transformé en version formatée)
est visuellement encombré et relativement difficile à lire.

LaTeX et HTML sont deux exemples de langages de balisage :

-   LaTeX (une extension du langage TeX) est communément utilisé pour créer des PDF.

{{<ex>}}
Exemple de texte en code LaTeX :
{{</ex>}}

``` latex
\documentclass{article}
\title{Mon titre}
\author{Prénom Nom}
\usepackage{datetime}
\newdate{date}{24}{11}{2022}
\date{\displaydate{date}}

\begin{document}
 \maketitle
 \section{Première section}
 Du texte dans cette première section.
\end{document}
```

-   HTML (souvent avec des fichiers CSS ou SCSS pour définir des règles de formatage) est utilisé pour créer des pages Web.

{{<ex>}}
Exemple de texte en code HTML :
{{</ex>}}

``` html
<!DOCTYPE html>
<html lang="fr-CA">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <title>Mon titre</title>
  </head>
  <body>
    <address class="author">Prénom Nom</address>
    <input type="date" value="2022-11-24" />

    <h1>Première section</h1>
    <p>Du texte dans cette première section.</p>
  </body>
</html>
```

### Markdown

Un certain nombre de langages de balisage légers ont heureusement été conçus
pour réduire le plus possible l'encombrement et la complexité du texte brut à
la source d'un document formaté.
<a href="https://fr.wikipedia.org/wiki/Markdown" target="_blank">Markdown</a>
(notez le calembour avec "markup" en anglais),
créé en 2004, est le plus populaire d'entre eux.
Dû à sa simplicité, il est devenu quasi-omniprésent.
Différents compilateurs de Markdown existent, ce qui amène un nombre variable
d'éléments syntaxiques additionnels, car un langage de balisage simple est
aussi plutôt limité.

En pratique, les fichiers Markdown sont des fichiers texte réguliers dont
l'extension est `.md`.

### Syntaxe de base de Markdown

<a href="https://daringfireball.net/projects/markdown/" target="_blank">À l’origine</a>,
Markdown est principalement conçu et utilisé pour créer des pages Web.
De ce fait, des balises HTML peuvent aussi être utilisées lorsque la syntaxe de
Markdown ne permet pas d'obtenir le résultat voulu.

<a href="https://www.markdownguide.org/basic-syntax/" target="_blank">Ce guide en ligne</a>
donne un aperçu des principales règles syntaxiques qui sont prises en charge
par une majorité d'applications.

### Pandoc et sa syntaxe étendue de Markdown

Alors que la syntaxe de base est suffisante pour générer des fichiers HTML,
elle reste très limitée pour d'autres formats.

<a href="https://pandoc.org/" target="_blank">Pandoc</a> est un convertisseur de formats
de balisage qui est à la fois gratuit et à code-source ouvert.
Il prend en charge <a href="https://quarto.org/docs/authoring/markdown-basics.html" target="_blank">une syntaxe étendue de Markdown</a>
avec des fonctionnalités additionnelles pour les figures, les tables, les
légendes, les équations mathématiques en code LaTeX, les citations et les blocs
de métadonnées YAML.
Bref, tout ce qui est nécessaire pour la création de documents scientifiques!

De tels fichiers texte restent aussi lisibles que les fichiers Markdown de base
(ce qui respecte la philosophie Markdown), mais ils peuvent également être
transformés en PDF, livres, sites Web complets, documents Word, etc.

Et bien sûr, ces fichiers texte peuvent également être gérés par un
gestionnaire de versions tel que <a href="https://git-scm.com/" target="_blank">Git</a>.

{{<ex>}}
Voici l'exemple précédent réécrit avec la syntaxe Markdown étendue de Pandoc :
{{</ex>}}

``` markdown
---
title: Mon titre
author: Prénom Nom
date: 2022-11-24
---
# Première section
Du texte dans cette première section.
```

## Programmation lettrée

La <a href="https://fr.wikipedia.org/wiki/Programmation_lettr%C3%A9e" target="_blank">programmation lettrée</a>
est une approche de la programmation qui combine des bouts de code et des bouts
de texte (formatés ou non).
Malgré une introduction en 1984, cette approche de création de documents a
surtout gagné en popularité dans les dernières années grâce au développement
de nouveaux outils tels que
<a href="https://r4ds.had.co.nz/r-markdown.html" target="_blank">R Markdown</a> et,
par la suite, <a href="https://jupyter.org/" target="_blank">Jupyter notebooks</a>.

## Quarto

### Comment ça fonctionne

1.  Les fichiers Quarto utilisent l'extension `.qmd` plutôt que `.md`,
    mais ils restent des fichiers texte relativement semblables au Markdown.
2.  Ils sont d'abord transformés en Markdown étendu Pandoc par Jupyter,
    lorsqu'utilisé avec Julia ou Python, ou par knitr, lorsqu'utilisé avec R.
3.  Enfin, Pandoc compile les fichiers Markdown dans le format de votre choix.

{{<ex>}}
Julia et Python utilisent le moteur Jupyter :
{{</ex>}}
{{<img src="/img/quarto/qmd_jupyter.png" title="" width="90%" line-height="1.0rem">}}
Image tirée de la <a href="https://quarto.org/docs/get-started/hello/text-editor.html#rendering" target="_blank">documentation sur Quarto</a>
{{</img>}}

{{<ex>}}
R utilise le moteur knitr :
{{</ex>}}
{{<img src="/img/quarto/qmd_knitr.png" title="" width="98%" line-height="0.2rem">}}
Image tirée de la <a href="https://quarto.org/docs/faq/rmarkdown.html#quarto-sounds-similar-to-r-markdown.-what-is-the-difference-and-why-create-a-new-project" target="_blank">documentation sur Quarto</a>
{{</img>}}

-   Si vous programmez en R, vous pouvez utiliser Quarto directement à partir de
    RStudio; Quarto est simplement une nouvelle version améliorée de R Markdown.
-   Si vous programmez en Julia ou en Python, vous pouvez utiliser Quarto
    directement à partir d'un notebook Jupyter (avec l'extension `.ipynb`).

{{<ex>}}
Fonctionnement de Quarto à partir d'un notebook Jupyter :
{{</ex>}}
{{<img src="/img/quarto/ipynb.png" title="" width="80%" line-height="1.7rem">}}
Image tirée de la <a href="https://github.com/quarto-dev/quarto-web/blob/main/docs/get-started/hello/images/ipynb-how-it-works.png" target="_blank">documentation sur Quarto</a>
{{</img>}}

Dans cet atelier, nous allons voir la méthode la plus générique,
c'est-à-dire celle qui utilise un éditeur texte.

### Langages de programmation et formats pris en charge

Quarto génère de la coloration syntaxique pour d'innombrables langages de
programmation et génère même une vue dynamique pour les blocs de code en :

-   Julia
-   Python
-   R
-   Observable JavaScript

Vous pouvez générer des documents dans une grande variété de formats :

{{<accordion title="Cliquez ici pour afficher la liste">}}
- AsciiDoc
- **Beamer**
- CommonMark
- ConTeXt
- Docusaurus
- DokuWiki
- ePub
- **GitHub Markdown**
- GNU
- Groff
- Hugo
- **HTML**
- JATS
- Jira Wiki
- **Jupyter**
- Markua
- MediaWiki
- MS **PowerPoint**
- MS **Word**
- Muse
- **OpenOffice**
- Org-Mode
- **PDF**
- reST
- **reveal.js**
- RTF
- XWiki
- ZimWiki
{{</accordion>}}

### Installation

1.  Téléchargez Quarto
    <a href="https://quarto.org/docs/get-started/" target="_blank">ici</a> et installez-le.
2.  Si ce n'est pas déjà fait, téléchargez le compilateur du langage (Julia,
    Python ou R) que vous voulez utiliser avec Quarto, de même que leur moteur
    correspondant (Jupyter pour Julia et Python, sinon knitr pour R).
    Voir ci-dessous les instructions spécifiques pour chacun.
3.  Afin de pouvoir générer des documents PDF, vous aurez besoin d'une
    distribution TeX. Si TeX n'est pas installé sur votre ordinateur, vous
    pouvez lancer la commande suivante :

``` bash
quarto install tinytex
```

Pour référence :
<a href="https://quarto.org/docs/get-started/" target="_blank">Quarto - Get Started</a>

#### Quarto avec Julia

Veuillez compléter votre environnement logiciel selon ce qui vous manque :

-   Téléchargez le compilateur Julia
    <a href="https://julialang.org/downloads/" target="_blank">ici</a> et installez-le.
-   À partir de la ligne de commande Julia, installez les modules
    <a href="https://github.com/JuliaLang/IJulia.jl" target="_blank">IJulia</a> et
    <a href="https://github.com/timholy/Revise.jl" target="_blank">Revise</a> :

``` julia
] add IJulia Revise
# <Backspace>
```

-   Ensuite, l'appel de la fonction `notebook()` du module `IJulia` permet
    d'installer Jupyter si vous ne l'aviez pas déjà :

``` julia
using IJulia
notebook()  # Pour installer une distribution minimale de Python+Jupyter
```

Pour référence :
<a href="https://quarto.org/docs/computations/julia.html#installation" target="_blank">Quarto - Using Julia</a>

#### Quarto avec Python

Veuillez compléter votre environnement logiciel selon ce qui vous manque :

-   Téléchargez le compilateur Python 3
    <a href="https://www.python.org/downloads/" target="_blank">ici</a> et installez-le.
-   Pour installer JupyterLab, ouvrez un terminal et lancez la commande :

``` bash
python3 -m pip install jupyter  # Si vous êtes sur Linux ou MacOS
python -m pip install jupyter   # Si vous êtes sur Windows
```

Pour référence :
<a href="https://quarto.org/docs/computations/python.html#installation" target="_blank">Quarto - Using Python</a>

#### Quarto avec R

Veuillez compléter votre environnement logiciel selon ce qui vous manque :

-   Téléchargez le compilateur R
    <a href="https://cran.r-project.org/" target="_blank">ici</a> et installez-le.
-   À partir de la ligne de commande R, installez le module `rmarkdown` :

``` r
install.packages("rmarkdown")
```

Pour référence :
<a href="https://quarto.org/docs/computations/r.html#installation" target="_blank">Quarto - Using R</a>

### Structure et syntaxe d'un fichier Quarto

#### Entête de fichier

Écrit en <a href="https://fr.wikipedia.org/wiki/YAML" target="_blank">YAML</a>
(pour *Yet Another Markup Language*), l'entête de fichier permet de définir
différentes options pour le document généré. Voyons quelques exemples.

{{<ex>}}
Pour générer un fichier HTML :
{{</ex>}}

``` yaml
---
title: "Mon titre"
author: "Mon nom"
format: html
---
```

{{<ex>}}
Pour générer un fichier HTML avec une table des matières et des styles
personnalisés :
{{</ex>}}

``` yaml
---
title: "Mon titre"
author: "Mon nom"
format:
  html:
    toc: true
    css: <mes_styles>.css
---
```

L'exemple ci-dessus fonctionne si vous n'utilisez aucun bloc de code
ou bien si vous utilisez uniquement des blocs de code R.
Cependant, si vous utilisez du code Julia ou Python, vous devez ajouter
l'option `jupyter` avec le nom de la commande qui devrait exécuter le
code dans Jupyter.

{{<ex>}}
Pour générer un document MS Word avec des blocs de code Python :
{{</ex>}}

``` yaml
---
title: "Mon titre"
author: "Mon nom"
format: docx
jupyter: python3
---
```

{{<ex>}}
Pour générer un document reveal.js avec des blocs de code Julia et
quelques options additionnelles :
{{</ex>}}

``` yaml
---
title: "Mon titre"
subtitle: "Un sous-titre"
institute: "Université XYZ"
date: "2022-11-24"
execute:
  error: true
  echo: true
format:
  revealjs:
    theme: [default, custom.scss]
    highlight-style: monokai
    code-line-numbers: false
    embed-resources: true
jupyter: julia-1.8
---
```

Voir <a href="https://quarto.org/docs/guide/" target="_blank">le guide de Quarto</a>
pour une liste exhaustive des options pour tous les formats.

#### Sections de texte

Les sections de texte sont écrites en
<a href="https://quarto.org/docs/authoring/markdown-basics.html" target="_blank">Markdown étendu Pandoc</a>.

#### Blocs de code

Si tout ce que vous voulez est une **coloration syntaxique** d'un bloc de
code, utilisez la syntaxe :

```` markdown
```{.langage}
<bloc de code>
```
````

Si vous voulez la **coloration syntaxique** et **permettre l'exécution**
d'un bloc de code, utilisez la syntaxe suivante à la place :

```` markdown
```{langage}
<bloc de code>
```
````

Des options peuvent aussi être ajoutées individuellement aux blocs de code :

```` markdown
```{langage}
#| <une option>: <valeur>

<bloc de code>
```
````

### Compilation de fichiers Quarto

Pour compiler un fichier Quarto, il y a deux commandes possibles
à exécuter dans un terminal :

``` bash
quarto render <fichier>.qmd   # Pour générer le document final
quarto preview <fichier>.qmd  # Aperçu du document final pendant son édition
```

## Un premier exercice

Créez un fichier appelé `test.qmd` avec l'éditeur texte de votre choix.

{{<ex>}}
Exemple:
{{</ex>}}

``` bash
nano test.qmd
```

Ajoutez une entête minimale avec un format de sortie.

{{<ex>}}
Exemple:
{{</ex>}}

``` yaml
---
title: "Titre accrocheur"
format: revealjs
---
```

Dans un second terminal, naviguez avec `cd` vers le répertoire
contenant le fichier `test.qmd` et exécutez la commande :

``` bash
quarto preview test.qmd
```

Ceci ouvrira le document généré dans votre navigateur Web.

Pour la suite, nous allons jouer avec ce fichier `test.qmd` et voir
comment il est compilé par Quarto en fonction de nos modifications.

## Exemples complets

Vous trouverez ci-dessous quelques exemples de fichiers Quarto
et leur version compilée respective.

### Diapositives avec reveal.js

{{<accordion title="Cliquez ici pour faire afficher le code">}}

``` markdown
---
title: "Mon titre"
author: "Mon nom"
institute: "Université XYZ"
format:
  revealjs:
    highlight-style: monokai
    code-line-numbers: false
    embed-resources: true
---

## Première section

En compilant dans le format reveal.js, chaque section de second niveau,
c'est-à-dire qui débute par `## <titre>`,
correspond à une nouvelle diapositive et son titre.

Ce comportement par défaut peut être changé dans les options en entête.

---

Une nouvelle diapositive **sans titre** peut être créée avec `---`
sur une nouvelle ligne de texte.

# Utiliser `# <titre>` pour un titre de chapitre

## Texte formaté

Le texte peut être formaté *en italique*, **en gras** et
[en souligné]{.underline}.

On peut aussi faire des exposants^2^, des indices~m,n~, ~~barrer du texte~~ et
inclure une courte `ligne de code`.

> Ceci est une citation.

## Colonnes

:::: {.columns}
::: {.column width="30%"}
Une première colonne.
:::

::: {.column width="70%"}
On peut configurer leur largeur respective.
:::
::::

## Listes animées

Une liste peut apparaître un item à la fois :

::: {.incremental}
- Comme
- ça!
:::

## Listes statiques

Ou apparaître d'un seul coup :

* Pas de
    + surprise!
        - :-)

## Listes ordonnées

1. Item 1
    a) Oeufs
2. Item 2
    a) Pain
    b) Confiture
3. Item 3
    a) Jus d'orange

## Images

![Compilation via Jupyter](../img/quarto/qmd_jupyter.png)

## Tables

| Col 1 | Col 2 | Col 3 |
|-------|-------|-------|
| a     | 4     | rouge |
| b     | 6     | jaune |
| c     | 7     | bleu  |

:::{.callout-note}
Les tables peuvent être complètement personnalisées
(ou sinon vous pouvez utiliser du HTML)
:::

## Équations LaTeX

$$
\frac{\partial \mathrm C}{ \partial t } +
\frac{1}{2} \sigma^{2} \mathrm S^{2}
\frac{\partial^{2} \mathrm C}{\partial \mathrm C^2} +
r \mathrm S \frac{\partial \mathrm C}{\partial \mathrm S}\ =
r \mathrm C
$$
```

{{</accordion>}}

-   <a href="/quartofr/revealjs.html" target="_blank"><strong>Afficher le résultat précompilé</strong></a>

### PDF

{{<notes>}}
Rappel : TeX est requis pour produire des PDF. Voir les [instructions d'installation ici](#installation).
{{</notes>}}

{{<accordion title="Code">}}

``` markdown
---
title: "Mon titre"
author: "Mon nom"
format:
  pdf:
    toc: true
---

# Chapitre 1

Une introduction ...

## Section 1.1

Plus d'explications ...

## Texte formaté

Le texte peut être formaté *en italique*, **en gras** et
[en souligné]{.underline}.

On peut aussi faire des exposants^2^, des indices~m,n~, ~~barrer du texte~~ et
inclure une courte `ligne de code`.

> Ceci est une citation.

## Listes

### Liste de points

* Un item
* Un autre item
    + Un sous-item
        - Une caractéristique

### Liste ordonnée

1. Item 1
    a) Oeufs
2. Item 2
    a) Pain
    b) Confiture
3. Item 3
    a) Jus d'orange

## Images

![Compilation via Jupyter](../img/quarto/qmd_jupyter.png)

## Tables

| Col 1 | Col 2 | Col 3 |
|-------|-------|-------|
| a     | 4     | rouge |
| b     | 6     | jaune |
| c     | 7     | bleu  |

:::{.callout-note}
Les tables peuvent être complètement personnalisées
(ou sinon vous pouvez utiliser du HTML)
:::

## Équations LaTeX

$$
\frac{\partial \mathrm C}{ \partial t } +
\frac{1}{2} \sigma^{2} \mathrm S^{2}
\frac{\partial^{2} \mathrm C}{\partial \mathrm C^2} +
r \mathrm S \frac{\partial \mathrm C}{\partial \mathrm S}\ =
r \mathrm C
$$
```

{{</accordion>}}

-   <a href="/quartofr/exemple_pdf.pdf" target="_blank"><strong>Afficher le résultat précompilé</strong></a>

### HTML avec des blocs de code R

{{<accordion title="Code">}}

```` markdown
---
title: "Mon titre"
author: "Mon nom"
institute: "Université XYZ"
format:
  html:
    embed-resources: true
number-sections: true
---

# Premier chapitre

Une introduction ...

## Première section

Plus d'explications ...

## Texte formaté  {#sec-format}

::: aside
Notez que chaque titre de chapitre ou section crée une ancre, ce qui permet
de citer des sections spécifiques de votre document.
:::

Le texte peut être formaté *en italique*, **en gras** et
[en souligné]{.underline}.

On peut aussi faire des exposants^2^, des indices~m,n~, ~~barrer du texte~~ et
inclure une courte `ligne de code`.

> Ceci est une citation.

## Colonnes

:::: {.columns}
::: {.column width="30%"}
Une première colonne plus étroite à gauche.
:::

::: {.column width="70%"}
On peut configurer leur largeur respective.
:::
::::

## Listes

### Liste de points

* Un item
* Un autre item
    + Un sous-item
        - Une caractéristique

### Liste ordonnée

1. Item 1
    a) Oeufs
2. Item 2
    a) Pain
    b) Confiture
3. Item 3
    a) Jus d'orange

## Images

![Compilation via Jupyter](../img/quarto/qmd_jupyter.png)

## Tables

| Col 1 | Col 2 | Col 3 |
|-------|-------|-------|
| a     | 4     | rouge |
| b     | 6     | jaune |
| c     | 7     | bleu  |

:::{.callout-note}
Les tables peuvent être complètement personnalisées
(ou sinon vous pouvez utiliser du HTML)
:::

## Équations LaTeX

$$
\frac{\partial \mathrm C}{ \partial t } +
\frac{1}{2} \sigma^{2} \mathrm S^{2}
\frac{\partial^{2} \mathrm C}{\partial \mathrm C^2} +
r \mathrm S \frac{\partial \mathrm C}{\partial \mathrm S}\ =
r \mathrm C
$$

## Références croisées

Voir @sec-format.

*Notez que vous pouvez ajouter des bibliographies, des organigrammes,
un équivalent aux `div` HTML et bien plus.
Rappelez-vous que cet exemple n'est qu'un aperçu des possibilités.*

## Essayons avec des blocs de code R

```{r}
# Ce code sera exécuté à la compilation
2 + 3
```

::: aside
Avez-vous remarqué que le contenu de la cellule de code peut être
copié en un seul clic sur l'icône qui apparaît?
:::

```{.r}
# Ce code ne sera pas exécuté
2 + 3
```

Afficher uniquement un résultat de calcul, c'est pratique pour cacher
les longs blocs de code.

```{r}
#| echo: false
# Seule la sortie sera affichée
data.frame(
  country = c("Canada", "USA", "Mexico"),
  var = c(2.9, 3.1, 4.5)
)
```

## Graphiques

```{r}
plot(cars)
```

<br>
Les options d'affichage permettent, entre autres, d'ajouter un titre de figure
sous le graphique :

```{r}
#| fig-cap: "Distance d'arrêt selon la vitesse de l'automobile"

plot(cars)
```

<br>
Vous pouvez aussi faire afficher plusieurs graphiques dans une même figure :

```{r}
#| layout-ncol: 2
#| fig-cap: 
#|   - "Distance d'arrêt selon la vitesse de l'automobile"
#|   - "Pression de la vapeur de mercure selon la température"

plot(cars)
plot(pressure)
```

Si vous avez installé `ggplot2`[^1], vous pouvez essayer ceci :

```{r}
library(ggplot2)

ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = class)) + 
  geom_smooth()
```

[^1]: Pour installer `ggplot2` :
    ```{.r}
    install.packages("ggplot2")
    ```
````

{{</accordion>}}

-   <a href="/quartofr/exemple_r.html" target="_blank"><strong>Afficher le résultat précompilé</strong></a>

### Beamer avec des blocs de code Python

Beamer est l'outil de référence pour créer des présentations en LaTeX ;
c'est donc un moyen de créer de jolies diapositives en PDF.

{{<accordion title="Code">}}

```` markdown
---
title: "Mon titre"
author: "Mon nom"
format: beamer
jupyter: python3
---

## Première diapositive

En compilant dans le format Beamer, chaque section de second niveau,
c'est-à-dire qui débute par `## <titre>`,
correspond à une nouvelle diapositive et son titre.

## Texte formaté

Le texte peut être formaté *en italique*, **en gras** et
[en souligné]{.underline}.

On peut aussi faire des exposants^2^, des indices~m,n~, ~~barrer du texte~~ et
inclure une courte `ligne de code`.

> Ceci est une citation.

## Listes

### Liste de points

* Un item
* Un autre item
    + Un sous-item
        - Une caractéristique

### Liste ordonnée

1. Item 1
    a) Oeufs
2. Item 2
    a) Pain
    b) Confiture
3. Item 3
    a) Jus d'orange

## Images

![Compilation via Jupyter](../img/quarto/qmd_jupyter.png)

## Tables

| Col 1 | Col 2 | Col 3 |
|-------|-------|-------|
| a     | 4     | rouge |
| b     | 6     | jaune |
| c     | 7     | bleu  |

:::{.callout-note}
Les tables peuvent être complètement personnalisées
(ou sinon vous pouvez utiliser du HTML)
:::

## Équations LaTeX

$$
\frac{\partial \mathrm C}{ \partial t } +
\frac{1}{2} \sigma^{2} \mathrm S^{2}
\frac{\partial^{2} \mathrm C}{\partial \mathrm C^2} +
r \mathrm S \frac{\partial \mathrm C}{\partial \mathrm S}\ =
r \mathrm C
$$

## Un bloc de code simple

Forcer l'affichage du code et du résultat :

```{python}
#| echo: true

2 + 3
```

## Générer un graphique avec Numpy et Matplotlib

```{python}
import matplotlib.pyplot as plt
import numpy as np

# Données pour le graphique
t = np.arange(0.0, 2.0, 0.01)
s = 1 + np.sin(2 * np.pi * t)

fig, ax = plt.subplots()
ax.plot(t, s)

ax.set(xlabel='Temps (s)', ylabel='Voltage (mV)',
       title='Note: le code reste caché')
ax.grid()

plt.show()
```
````

{{</accordion>}}

-   <a href="/quartofr/beamer.pdf" target="_blank"><strong>Afficher le résultat précompilé</strong></a>

<br>
{{< youtube 90CrIOtLrCU >}}
