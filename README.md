<div id="top"></div>

## Logseq Query Builder Plugin

This plugin is an implementation of the function of the online tool _Logseq Advanced Query Builder_. The underlying software for both the online tool and this plugin are shared so all commands work consistently. 

## This plugin
- recognises [Simple Commands](#simple-commands) contained in a logseq code block. 
- Choosing **Advanced Query Builder** in the code blocks menu
    - will generate an advanced query in a **new** child block
    - You can alter the code block and generate another query which will add another new child block. 
    - In this way you can experiment with generating multiple advanced queries.
<p>

- [Installing the plugin](#installation)
- [How to Use the plugin](#how-to-use-this-plugin)
- [Simple Commands](#simple-commands)
- [Releases](#releases)
- [Technical Information](#technical-information)


## Online tool
Currently plugins are not supported in the mobile versions of Logseq. However you can use the online tool to buid advanced queries from a mobile browser 
- See the FAQ at https://adxsoft.github.io/logseqadvancedquerybuilder/ for detailed instructions for using the online tool.  

- The online tool has many examples you can review.


## How to use this plugin
The [Simple Commands](#simple-commands) are entered into a logseq code block in the structure shown below. _Note the three backticks surround the commands_<br>
<pre>
```
- commandname
    - argument
    - argument
- commandname
    - argument
    - argument
```
</pre>
Optionally arguments can begin with any of these words
```
and
or
not
```

Here is an example that selects pages in namespace physics with page property pagetype 'fluids'
<pre>
```
title: Example Commands
- pages
    - *
- pageproperties
    - pagetype, "fluids"
- namespace
    - physics 
```
</pre>
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

Commands are designed to be simple to use. 
Most commands have one or more arguments
<pre>
```
- commandname
    - argument
    - argument
- commandname
    - argument
    - argument
```
</pre>
Optionally arguments can begin with any of these words
```
and
or
not
```
#### Important Concept 
Queries filter in two ways - pages or blocks

<b>pages</b> command retrieves the special blocks that have ONLY the page information<br> such as name, page tags, page properties<br>
<small><i>- these page blocks are placed into the ?block variable</i></small><br><br>
<b>blocks</b> command retrieves every single block in the graph including the special page blocks<br>
<small><i>- these page blocks are placed into the ?block variable and the page this block belongs to is placed in the ?page variable</i></small><br><br>
You must choose a <b>pages</b> command <b>OR</b> a <b>blocks</b> command (you cannot use both together) 
                   
#### Wildcards
Wildcards can be full name or partial name using \* character<br>
test\* - starts with text 'test'
\*end - ends with text 'end'
\*tax\* - contains text 'tax'

Note.
- Wildcards are used with pages or blocks command at this stage
- Unfortunately Logseq Advanced queries do not yet support partial strings for properties
    - see (https://github.com/logseq/logseq/issues/7410). 
    Once this is implemented in Logseq I will be able to have wildcards for  _pageproperties_ and _blockproperties_ commands
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

### Query Results commands
- [collapse](#collapse) - collapse query results
- [expand](#collapse) - expand query results
- [showbreadcrumbs](#showbreadcrumbs) - show query breadcrumbs
- [hidebreadcrumbs](#hidebreadcrumbs) - hide query breadcrumbs

### Query options
- [option](#option) - options for generated query

<p align="right">(<a href="#top">back to top</a>)</p>

## Simple Commands - Detailed Examples
### pages
A page is a special block of its own that contains page-specific information including page tags, page properties etc. It is a parent to any blocks that belong to the page. Each page has a title and you can choose pages using their full title or wildcards patterns of their title.
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
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### blocks
Blocks are the basic unit of information in Logseq. 
- Blocks can contain text, tags, properties, links to other pages or blocks.
- Each block has a content property and you can choose blocks using their content or wildcards patterns of their content.
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
Every Logseq block can contains user properties which consist of the property name and the property value. Property name cannot contains spaces. Values can be a string (in double quotes) or a number. 
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
Every Logseq block can contain tags. Tags can be selected by their full name (excluding #) or by wildcards of the tag full name.
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
Every Logseq block can contain a deadline date. Include this command to select only these blocks.
```
title: find blocks with deadlines
- blocks
    - *
- deadline

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### deadlinebetween
Every Logseq block can contain a deadline date. Include this command to select only these blocks whose deadline date falls within a from and to date. Dates are specified as :today or :ddd-xxxxxx where ddd is no of days and xxxxxx is before or after.
```
title: find blocks with deadlines in a date range
- blocks
    - *
- deadlinebetween
    - :120d-before :30d-after

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### journalsbetween
Every Logseq journal belongs to a specific date. Include this command to select only those journals which fall within a from and to date. Dates are specified as :today or :ddd-xxxxxx where ddd is no of days and xxxxxx is before or after.
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
Use this command to limit the query results to journals only, pages get excluded.
```
title: find journals
- pages
    - *
- journalonly

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### namespace
use this command to restrict query results to one of more namespaces. Note pages or blocks have to exist at the specified level of the namespace in order for you see any results. 
_(Note. If you only have one page which is physics/fluids and no page exists called physics then using physics as the namespace will not find physics/fluids page you must specify physics/fluid to see it in the query results. This behaviour will hopefully change one day to show all lower level pages under physics.)_
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
Every Logseq page can contains user properties which belong to the page. Page properties are not block properties, they belong only to the page. Page properties consist of the property name and the property value. Property name cannot contains spaces. Values can be a string (in double quotes) or a number. 
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
Every Logseq page can contains tags which belong to the page. Page tags are not block tags, they belong only to the page. Page tags can be selected by their full name (excluding #) or by wildcards of the tag full name.
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
Every logseq block can contain links to other pages or journals. This command will restrict query results to blocks that contains one or more link references. Note the date format to link to journals should be in the same format the journal titles are set in Logseq settings. 
```
title: select blocks with links to journals that use the default date setting for journals
- blocks
    - *
- pagelinks
    - Dec 25th, 2022
    - Jan 1st, 2019

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### tasks
Every Logseq block can contains one or more tasks. This command will restrict results to include (or exclude) specific task types
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
Every Logseq block can contain a schedule date. Include this command to select only these blocks.
```
title: find scheduled blocks
- blocks
    - *
- scheduled
```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### scheduledbetween
Every Logseq block can contain a schedule date. Include this command to select only these blocks whose schedule date falls within a from and to date. Dates are specified as :today or :ddd-xxxxxx where ddd is no of days and xxxxxx is before or after.
```
title: scheduled - find scheduled blocks in a date range
- blocks
    - *
- scheduledbetween
    - :20d-before :20d-after

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### option
Currently there is only one option available. 
_includecomments_ option will include a comment line which explains the generated query line.
```
title: option - include comments for each generated query line
option: includecomments
- blocks
    - *
- pagelinks
    - Dec 25th, 2022
    - Jan 1st, 2019

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### collapse 
This command will cause the query results to be collapsed.
```
title: collapse results
- pages
    - testpage00*
- collapse

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### expand 
This command will cause the query results to be expanded fully.
```
title: expand results
- pages
    - testpage00*
- expand

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### showbreadcrumbs 
Show breadcrumb trail (parent levels in the outline) of the retrieved blocks in query results
```
title: show breadcrumbs
- pages
    - testpage00*
- showbreadcrumb

```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

### hidebreadcrumbs 
Hide the breadcrumb trail (parent levels in the outline) of the retrieved blocks in query results
```
title: hide breadcrumbs
- pages
    - testpage00*
- hidebreadcrumb
```
<p align="right">(<a href="#simple-commands">back to Simple Commands</a>)</p>

## Technical Information

- Originally the online tool was developed using pyscript and redeveloped in javascript. 
- To ensure consistency between the online tool and the plugin the javascript code is shared.
    - A variable called **_mode_** is set to _logseq-plugin_, _website_ or _local_.
    - All modes use index.js as common code
    - **mode _logseq-plugin_**
            - will operate as a logseq plugin
            - has its own _index.html_ and _package.json_ file
            - files are contained in the _plugin-dist_ folder
    - **mode _website_**
            - will operate as the online tool
            - has its own _index.html_ and _package.json_ file
            - files are contained in the _website-dist_ folder
    - **mode _local_**
            - will operate locally
            - has its own _index.html_ and _package.json_ file
            - files are contained in the main folder
            - has a _index.test.js_ file which is used for unit testing with the Jest Testing Library

## Releases
- v0.1
    - Original release - Dec 23rd 2022