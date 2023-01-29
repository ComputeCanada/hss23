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

**Prérequis techniques**: Les participantes et participants devront installer Quarto, R, Python et quelques
autres outils sur leur ordinateur. Les instructions seront fournies par courriel et ajoutées au site Web avant
la semaine d'ateliers.

Inscrivez-vous <a href="https://www.eventbrite.ca/e/510984316847" target="_blank">ici</a>

The same workshop [in English](/quarto).

#### Biographie

Diplômé au baccalauréat et à la maîtrise en génie logiciel et génie informatique, **Pier-Luc St-Onge** a
travaillé pendant cinq ans pour différents laboratoires de recherche avant de rejoindre Calcul Québec en
mai 2013. Dans son projet de recherche, il s'était spécialisé en vision par ordinateur avec OpenCV. À Calcul
Québec, il fait partie de l'équipe d'analystes offrant du soutien aux utilisateurs des ressources de calcul.

<!-- {{< vimeo 690948795 >}} -->
<!-- <br> -->
<!-- - [Watch this session on Vimeo](https://vimeo.com/690948795) -->

{{<br>}}

------------------------------------------------------------------------

## Le balisage et Markdown

### Les langages de balisage

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
2.  Ils sont d'abord transformés en Markdown étendu par Jupyter,
    lorsqu'utilisé avec Julia ou Python, ou par knitr, lorsqu'utilisé avec R.
3.  Enfin, Pandoc compile les fichiers Markdown dans le format de votre choix.

{{<ex>}}
Julia et Python utilisent le noyau Jupyter :
{{</ex>}}
{{<img src="/img/quarto/qmd_jupyter.png" title="" width="90%" line-height="1.0rem">}}
Image tirée de la <a href="https://quarto.org/docs/get-started/hello/text-editor.html#rendering" target="_blank">documentation sur Quarto</a>
{{</img>}}

{{<ex>}}
R utilise le noyau knitr :
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
- Revealjs
- RTF
- XWiki
- ZimWiki
{{</accordion>}}

### Installation

1.  Download Quarto <a href="https://quarto.org/docs/get-started/" target="_blank">here</a>.

2.  Download the language(s) (R, Python, or Julia) you will want to use with Quarto as well as their corresponding engine (knitr for R; Jupyter for Python and Julia):

<u>If you want to use Quarto with R, you will need:</u>

-   R (download <a href="https://cran.r-project.org/" target="_blank">here</a> if you don't have R already on your system),
-   the `rmarkdown` package. For this, launch R and run:

``` r
install.packages("rmarkdown")
```

<u>If you want to use it with Python, you will need:</u>

-   Python 3 (download <a href="https://www.python.org/downloads/" target="_blank">here</a> if don't have it on your system),
-   JupyterLab. For this, open a terminal and run:

``` bash
python3 -m pip install jupyterlab  # if you are on MacOS or Linux
py -m pip install jupyterlab       # if you are on Windows
```

<u>Finally, if you want to use Quarto with Julia, you will need:</u>

-   Julia (download <a href="https://julialang.org/downloads/" target="_blank">here</a> if you don't have Julia),
-   the <a href="https://github.com/JuliaLang/IJulia.jl" target="_blank">IJulia</a> and <a href="https://github.com/timholy/Revise.jl" target="_blank">Revise</a> packages. For this, launch Julia and run:

``` julia
] add IJulia Revise
# <Backspace>
using IJulia
notebook()      # to install a minimal Python+Jupyter distribution
```

Running `notebook()` allows you to install Jupyter if you don't already have it.

### Document structure and syntax

#### Front matter

Written in YAML. Sets the options for the document. Let's see a few examples.

{{<ex>}}
HTML output:
{{</ex>}}

``` yaml
---
title: "My title"
author: "My name"
format: html
---
```

{{<ex>}}
HTML output with a few options:
{{</ex>}}

``` yaml
---
title: "My title"
author: "My name"
format:
  html:
    toc: true
    css: <my_file>.css
---
```

The above examples would work if you don't use any code blocks or if you use R code blocks. If you use Python or Julia however, you need to add a `jupyter` entry with the name of the language that should run in Jupyter.

{{<ex>}}
MS Word output with Python code blocks:
{{</ex>}}

``` yaml
---
title: "My title"
author: "My name"
format: docx
jupyter: python3
---
```

{{<ex>}}
revealjs output with some options and Julia code blocks:
{{</ex>}}

``` yaml
---
title: "Some title"
subtitle: "Some subtitle"
institute: "Simon Fraser University"
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

See <a href="https://quarto.org/docs/guide/" target="_blank">the Quarto documentation</a> for an exhaustive list of options for all formats.

#### Written sections

Written sections are written in <a href="https://quarto.org/docs/authoring/markdown-basics.html" target="_blank">Pandoc’s extended Markdown</a>.

#### Code blocks

If all you want is **syntax highlighting** of the code blocks, use this syntax:

```` markdown
```{.language}
<some code>
```
````

If you want **syntax highlighting** of the blocks and **for the code to run**, use instead:

```` markdown
```{language}
<some code>
```
````

In addition, options can be added to individual code blocks:

```` markdown
```{language}
#| <some option>: <some option value>

<some code>
```
````

### Rendering

Using Quarto is very simple: there are only two commands you need to know.

In a terminal, simply run either of:

``` bash
quarto render <file>.qmd     # this will render the document
quarto preview <file>.qmd    # this will display live preview as you work on your document
```

## Let's give this a try

Create a file called `test.qmd` with the text editor of your choice.

{{<ex>}}
Example:
{{</ex>}}

``` bash
nano test.qmd
```

Add a minimal front matter with the output format.

{{<ex>}}
Example:
{{</ex>}}

``` yaml
---
title: "Some title"
format: revealjs
---
```

Then open a new terminal, `cd` to the location of the file, and run the command:

``` bash
quarto preview test.qmd
```

This will open the rendered document in your browser.

We will play with this `test.qmd` file and see how it is rendered by Quarto as we go.

## Examples

Below are a few basic example files and their outputs.

### Revealjs presentation

{{<accordion title="Code">}}

``` markdown
---
title: "My title"
author: "My name"
institute: "Simon Fraser University"
format:
  revealjs:
    highlight-style: monokai
    code-line-numbers: false
    embed-resources: true
---

## First section

When exporting to revealjs, second level sections mark the start of new slides,
with a slide title.

This can be changed in options.

---

New slides can be started without titles this way.

# There are title slides

## Formatting

Text can be rendered *in italic* or **in bold** as well as [underlined]{.underline}.

You can use superscripts^2^, subscripts~test~, ~~strikethrough~~, and `inline code`.

> This is a quote.

## Columns

:::: {.columns}
::: {.column width="30%"}
You can create columns.
:::

::: {.column width="70%"}
And you can set their respective width.
:::
::::

## Lists

::: {.incremental}
- List can happen one line at a time
- like
- this
:::

## Lists

- Or all at the same time
- like
- that

## Ordered lists

1. Item 1
2. Item 2
3. Item 3

## Images

![Example image](/home/marie/parvus/prog/tcl/static/img/quarto/qmd_jupyter.png)

## Tables

| Col 1 | Col 2 | Col 3  |
|------ |-------|--------|
| a     | 1     | red    |
| b     | 2     | orange | 
| c     | 3     | yellow |

:::{.callout-note}
Tables can be fully customized (or you could use raw html).
:::

## Equations

$$
\frac{\partial \mathrm C}{ \partial \mathrm t } + \frac{1}{2}\sigma^{2} \mathrm S^{2}
\frac{\partial^{2} \mathrm C}{\partial \mathrm C^2}
  + \mathrm r \mathrm S \frac{\partial \mathrm C}{\partial \mathrm S}\ =
  \mathrm r \mathrm C 
$$
```

{{</accordion>}}

{{<accordion title="Rendered document (click on the image to open the document in a new tab)">}}
<a href="https://hss23.netlify.app/quarto/revealjs.html" target="_blank"><img src="../..\quarto/revealjs.png" /></a>
{{</accordion>}}

### pdf

{{<accordion title="Code">}}

``` markdown
---
title: "My title"
author: "My name"
format:
  pdf:
    toc: true
---

# Header 1

Some text.

## Header 2

More text.

## Formatting

Text can be rendered *in italic* or **in bold** as well as [underlined]{.underline}.

You can use superscripts^2^, subscripts~test~, ~~strikethrough~~, and `inline code`.

> This is a quote.

## Lists

### Unordered

- Item 1
- Item 2
- Item 3

### Ordered

1. Item 1
2. Item 2
3. Item 3

## Images

![Example image](/home/marie/parvus/prog/tcl/static/img/quarto/qmd_jupyter.png)

## Tables

| Col 1 | Col 2 | Col 3  |
|------ |-------|--------|
| a     | 1     | red    |
| b     | 2     | orange | 
| c     | 3     | yellow |

:::{.callout-note}
Tables can be fully customized (or you could use raw html).
:::

## Equations

$$
\frac{\partial \mathrm C}{ \partial \mathrm t } + \frac{1}{2}\sigma^{2} \mathrm S^{2}
\frac{\partial^{2} \mathrm C}{\partial \mathrm C^2}
  + \mathrm r \mathrm S \frac{\partial \mathrm C}{\partial \mathrm S}\ =
  \mathrm r \mathrm C 
$$
```

{{</accordion>}}

{{<accordion title="Rendered document (click on the image to open the document in a new tab)">}}
[![](../..\quarto/pdf.png)](/quarto/pdf.pdf)
{{</accordion>}}

{{<notes>}}
Note: in order to export to pdf, you need a TeX distribution. You probably already have one installed on your machine, so you should first try to render or preview a document to pdf to see whether it works. If it doesn't work, you can install the minimalist distribution TinyTex by running in your terminal:
{{</notes>}}

``` bash
quarto install tool tinytex
```

### HTML with R code blocks

{{<accordion title="Code">}}

```` markdown
---
title: "My title"
author: "My name"
institute: "Simon Fraser University"
format: html
---

# Header 1

## Header 2

Some text.

## Formatting  {#sec-formatting}

::: aside
Note that each header automatically creates an anchor,
making it easy to link to specific sections of your documents.
:::

Text can be rendered *in italic* or **in bold** as well as [underlined]{.underline}.

You can use superscripts^2^, subscripts~test~, ~~strikethrough~~, and `inline code`.

> This is a quote.

## Columns

:::: {.columns}
::: {.column width="30%"}
You can create columns.
:::

::: {.column width="70%"}
And you can set their respective width.
:::
::::

## Lists

- Item 1
- Item 2
- Item 3

## Ordered lists

1. Item 1
2. Item 2
3. Item 3

## Images

![Example image](qmd_jupyter.png)

## Tables

| Col 1 | Col 2 | Col 3  |
|------ |-------|--------|
| a     | 1     | red    |
| b     | 2     | orange | 
| c     | 3     | yellow |

:::{.callout-note}
Tables can be fully customized (or you could use raw html).
:::

## Equations

$$
\frac{\partial \mathrm C}{ \partial \mathrm t } + \frac{1}{2}\sigma^{2} \mathrm S^{2}
\frac{\partial^{2} \mathrm C}{\partial \mathrm C^2}
  + \mathrm r \mathrm S \frac{\partial \mathrm C}{\partial \mathrm S}\ =
  \mathrm r \mathrm C 
$$

## Cross-references

See @sec-formatting.

*Note that you can add bibliographies, flow charts, the equivalent of HTML "div",
and just so much more. Remember that this is a tiny overview.*

## Let's try some code blocks now

```{r}
# This is a block that runs
2 + 3
```

::: aside
Did you notice that the content of your code blocks can be copied with a click?
Of course, this is customizable.
:::

```{.r}
# This is a block that doesn't run
2 + 3
```

```{r}
#| echo: false
# And this is a block showing only the output
data.frame(
  country = c("Canada", "USA", "Mexico"),
  var = c(2.9, 3.1, 4.5)
)
```

## Plots

```{r}
plot(cars)
```

<br>
You can play with options to add a title:

```{r}
#| fig-cap: "Stopping distance as a function of speed in cars"

plot(cars)
```

<br>
You can have more complex multi-plot layouts:

```{r}
#| layout-ncol: 2
#| fig-cap: 
#|   - "Stopping distance as a function of speed in cars"
#|   - "Vapor pressure of mercury as a function of temperature"

plot(cars)
plot(pressure)
```

For those who have `ggplot2`[^1], you can try that too:

```{r}
library(ggplot2)

ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = class)) + 
  geom_smooth()
```

[^1]: You can install it with:
    ```{.r}
    install.packages("ggplot2")
    ```
````

{{</accordion>}}

{{<accordion title="Rendered document (click on the image to open the document in a new tab)">}}
<a href="https://hss23.netlify.app/quarto/html.html" target="_blank"><img src="../..\quarto/html.png" /></a>
{{</accordion>}}

### Beamer with Python code blocks

Beamer is LaTeX presentation framework: a way to create beautiful pdf slides.

{{<accordion title="Code">}}

```` markdown
---
title: "Some title"
author: "Some name"
format: beamer
jupyter: python3
---

## First slide

With some content

## Formatting

Text can be rendered *in italic* or **in bold** as well as [underlined]{.underline}.

You can use superscripts^2^, subscripts~test~, ~~strikethrough~~, and `inline code`.

## Lists

- Item 1
- Item 2
- Item 3

## Ordered lists

1. Item 1
2. Item 2
3. Item 3

## Images

![Example image](qmd_jupyter.png)

## Tables

| Col 1 | Col 2 | Col 3  |
|------ |-------|--------|
| a     | 1     | red    |
| b     | 2     | orange | 
| c     | 3     | yellow |

:::{.callout-note}
Tables can be fully customized (or you could use raw html).
:::

## Equations

$$
\frac{\partial \mathrm C}{ \partial \mathrm t } + \frac{1}{2}\sigma^{2} \mathrm S^{2}
\frac{\partial^{2} \mathrm C}{\partial \mathrm C^2}
  + \mathrm r \mathrm S \frac{\partial \mathrm C}{\partial \mathrm S}\ =
  \mathrm r \mathrm C 
$$

## Some basic code block

```{python}
#| echo: true

2 + 3
```

## Some plot

```{python}
import matplotlib.pyplot as plt
import numpy as np

# Data for plotting
t = np.arange(0.0, 2.0, 0.01)
s = 1 + np.sin(2 * np.pi * t)

fig, ax = plt.subplots()
ax.plot(t, s)

ax.set(xlabel='time (s)', ylabel='voltage (mV)',
       title='Here goes the title')
ax.grid()

fig.savefig("test.png")
plt.show()
```
````

{{</accordion>}}

{{<accordion title="Rendered document (click on the image to open the document in a new tab)">}}
[![](../..\quarto/beamer.png)](/quarto/beamer.pdf)
{{</accordion>}}
