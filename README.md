<!-- This README file goes with the plugin distribution and is what is displayed within Logseq when the plugin help is requested -->
# Logseq Query Builder Plugin

* builds advanced logseq queries from [Simple Commands](#simple-commands) contained in a logseq code block. 
* Choosing **Advanced Query Builder** in the code blocks menu (right click on block's bullet)
    * will generate an advanced query in a **new** child block
    * You can alter the code block and generate another query which will add another new child block. 
    * In this way you can experiment with generating multiple advanced queries.
## Detailed Documentation

Can be found [here](https://github.com/adxsoft/docs-logseq-query-builder-plugin)

## Installation
### Preparation
* Click the 3 dots in the righthand corner and go to **Settings**.
* Go to **Advanced** and enable **Plug-in system**.
* Restart the application.
* Click 3 dots and go to Plugins (or `Esc t p`).

### Install plugin from the Marketplace (recommended) 
* Click the `Marketplace` button and then click `Plugins`.
* Find the plugin and click `Install`.

### Install plugin manually
* Click the green Code button above and download the zip
* Unzip it into a folder
* Click `Load unpacked plugin`, and select the folder where the plugin code was unzipped


## Technical Information
* Originally the online tool was developed using pyscript and redeveloped in javascript. 
* To ensure consistency between the online tool and the plugin the javascript code is shared.
    * A variable called **_mode_** is set to _logseq-plugin_, _website_ or _local_.
    * All modes use index.js as common code
    * **mode _logseq-plugin_**
            * will operate as a logseq plugin
            * has its own _index.html_ and _package.json_ file
            * files are contained in the _plugin-dist_ folder
    * **mode _website_**
            * will operate as the online tool
            * has its own _index.html_ and _package.json_ file
            * files are contained in the _website-dist_ folder
    * **mode _local_**
            * will operate locally
            * has its own _index.html_ and _package.json_ file
            * files are contained in the main folder
            * has a _index.test.js_ file which is used for unit testing with the Jest Testing Library - the index.test.js file is contained in the repository for the online tool at 


## Releases
- v0.1
    - Original release - Dec 30th 2022
- v0.7
    - First release to the logseq marketplace 23rd Feb 2023
