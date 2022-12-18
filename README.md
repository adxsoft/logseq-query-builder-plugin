# logseq-query-builder-plugin
A logseq plugin that generates advanced queries from simple commands
<div id="top"></div>
# Logseq Query Builder Plugin


- [Installation](#installation)
- [How to Use](#how-to-use)
- [Simple Commands](#simple-commands)

## How to use
The [Simple Commands](#simple-commands) are entered into a logseq code block<br>
````
```
- commandname
    - argument
    - argument
- commandname
    - argument
    - argument
```
````
Optionally arguments can begin with any of these words
```
and
or
not
```

For here is an example that selects pages in namespace physics with page property pagetype 'fluids'
```
title: Example Commands
- pages
    - *
- pageproperties
    - pagetype, "fluids"
- namespace
    - physics 
```

You can include a title for the generated query like this
```
title: your text for the query title
```
You can request comments describing the generated query lines by adding this line at the start of the code block
```
option: includecomments
```
<p align="right">(<a href="#top">back to top</a>)</p>

## Installation

### Preparation

- Click the 3 dots in the righthand corner and go to **Settings**.
- Go to **Advanced** and enable **Plug-in system**.
- Restart the application.
- Click 3 dots and go to Plugins (or `Esc t p`).

### Install plugin from the Marketplace (recommended) 

- Click the `Marketplace` button and then click `Plugins`.
- Find the plugin and click `Install`.

### Install plugin manually

- Download a released version assets from Github.
- Unzip it.
- Click `Load unpacked plugin`, and select destination directory to the unzipped folder.

<p align="right">(<a href="#top">back to top</a>)</p>

## Simple Commands

### Main extraction commands
- [pages](#pages) - select pages by wildcards
- [blocks](#blocks) - select logseq blocks by wildcards

### Properties
- [pageproperties](#pageproperties) - select pages by page properties
- [blockproperties](#blockproperties) - select blocks by property values

### Tags
- [pagetags](#pagetags) - select pages by tag
- [blocktags](#blocktags) - select blocks by tag

### Tasks
- [tasks](#tasks) - select tasks

### Journals
- [journalonly](#journalonly) - only select journal pages
- [journalsbetween](#journalsbetween) - only select journal pages in a date range

### Deadline
- [deadline](#deadline) - select pages or blocks that have a deadline
- [deadlinebetween](#deadlinebetween) - select pages or blocks that have a deadline in a date range

### Scheduled
- [scheduled](#scheduled) - select pages or blocks that are scheduled
- [scheduledbetween](#scheduledbetween) - select pages or blocks that are scheduled in a date range     

### Namespaces
- [namespace](#namespace) - select pages or blocks within a namespace

### Links
- [pagelinks](#pagelinks) - select blocks that have links to pages<br>- note. Journal page link is your chosen format in your settings. For example <i>Dec 25th, 2022</i>

### Query Result Format
- [collapse](#collapse) - collapse query results
- [expand](#collapse) - expand query results
- [showbreadcrumbs](#showbreadcrumbs) - show query breadcrumbs
- [hidebreadcrumbs](#hidebreadcrumbs) - hide query breadcrumbs

### Query optioins
- [option](#option) - options for generated query

<p align="right">(<a href="#top">back to top</a>)</p>

## Simple Command - Detailed Examples
### pages
A page is a special block of its own that contains page-specific information including page tags, page properties etc. It is a parent to any blocks that belong to the page
```
title: pages command - select all pages
- pages
    - *

```
```
title: pages command - specific pages
- pages
    - testpage001
    - testpage002

```
```
title: pages command - pages by wildcards
- pages
    - testpage00*

```
```
title: pages command - pages by wildcards
- pages
    - *002

```
```
title: pages command - pages by wildcards
- pages
    - *page00*

```
```
title: pages command - ignore pages (including wildcards)
- pages
    - not testpage*
    - not Queries*

```
### blocks
```
title: select all blocks
- blocks
    - *
```
```
title: select blocks by wildcards using *
- blocks
    - startingtext*
    - *endingtext
    - *textanywhere*
```
```
title: blocks command - ignore blocks using wildcards
- blocks
    - not And sir dare view*
    - not *here leave merit enjoy forth.
    - not *roof gutters*

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### blockproperties
```
title: select and exclude blocks with block properties
- blocks
    - *
- blockproperties
    - category, "b-thriller"
    - category, "b-western"
    - grade, "b-fiction"

```
```
title: block property combinations using and and or
- blocks
    - *
- blockproperties
    - category, "b-fiction"
    - or grade, "b-western"
    - and category, "b-travel"

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### blocktags
```
title: blocktags - select and exclude block level tags
- blocks
    - *
- blocktags
    - tagA
    - tagD
    - not tagB

```
```
title: blocktags and pages don't mix
- pages
    - testpage00*
- blocktags
    - tagA
    - not tagB

```
```
title: block tag combinations using and and or
- blocks
    - *
- blocktags
    - tagA
    - or tagB
    - and tagD

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### deadline
```
title: find blocks with deadlines
- blocks
    - *
- deadline

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### deadlinebetween
```
title: find blocks with deadlines in a date range
- blocks
    - *
- deadlinebetween
    - :120d-before :30d-after

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### journalsbetween
```
title: find journal in a date range
- pages
    - *
- journalsbetween
    - :today :30d-after

```
```
title: find journals between dates
- blocks
    - *
- journalsbetween
    - :30d-before :today

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### journalonly
```
title: find journals
- pages
    - *
- journalonly

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### namespace
```
title: only search pages in specific namespace
- pages
    - *
- namespace
    - physics

```
```
title: find block properties in a namespace
- blocks
    - *
- namespace
    - tech/python
- blockproperties
    - grade, "b-fiction"

```
```
title: find scheduled blocks in a namespace
- blocks
    - *
- namespace
    - physics
- scheduled

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### pageproperties
```
title: select and exclude pages with page properties
- pages
    - *
- pageproperties
    - pagetype, "p-major"
    - pagetype, "p-minor"
    - not pagetype, "p-advanced"

```
```
title: page property combinations using and and or
- pages
    - *
- pageproperties
    - pagecategory, "p-minor"
    - or pagecategory, "p-minimum"
    - and pagetype, "p-type1"

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### pagetags
```
title: pagetags - page level tags
- pages
    - testpage*
- pagetags
    - classA

```
```
title: pagetags and pages
- pages
    - *dynamics*
- pagetags
    - classB

```
```
title: page tag combinations using and and or
- pages
    - *
- pagetags
    - classA
    - or classB
    - and classH

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### pagelinks
```
title: select blocks with links to journals
- blocks
    - *
- pagelinks
    - Dec 25th, 2022
    - Jan 1st, 2019

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### tasks
```
title: select and exclude task types
- tasks
    - TODO
    - not DOING

```
```
title: select and exclude task types
- pages
    - testpage00*
- tasks
    - TODO
    - not DOING

```
```
title: task and or combintions
- blocks
    - *
- tasks
    - TODO
    - and WAITING
    - or LATER
    - not DOING

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### scheduled
```
title: find scheduled blocks
- blocks
    - *
- scheduled
```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### scheduledbetween
```
title: scheduled - find scheduled blocks in a date range
- blocks
    - *
- scheduledbetween
    - :20d-before :20d-after

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### option
```
title: option - includecommandcomments
option: includecommandcomments
- blocks
    - *
- pagelinks
    - Dec 25th, 2022
    - Jan 1st, 2019

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### collapse 

```
title: collapse results
- pages
    - testpage00*
- collapse

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### expand 
```
title: expand results
- pages
    - testpage00*
- expand

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### showbreadcrumbs 
```
title: show breadcrumbs
- pages
    - testpage00*
- showbreadcrumb

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### hidebreadcrumbs 
```
title: hide breadcrumbs
- pages
    - testpage00*
- hidebreadcrumb

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>
