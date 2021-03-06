# Developers Guide

## Getting the environment setup

1. Get the [latest release of Sia](TODO)
2. Download [atom-shell](https://github.com/atom/atom-shell/releases)
3. Extract atom-shell (optionally add it to your path, the `atom` executable within the directory is what you use to run atom-shell applications)
3. Clone Sia-UI `git clone https://github.com/NebulousLabs/Sia-UI.git`
4. Install Sia-UI Dependencies
```
# With ubuntu
sudo apt-get install ruby-haml node-less
```
5. Make the project using `make` in the sia-ui directory
5. Execute `/path/to/atom-shell/atom /path/to/sia-ui`

## Project Structure

This is a quick walk through the structure of the project.

### Root Directory

At the top level of the project there are two directories...

`lib`
`site`

`lib` contains scripts used at in the atom-shell layer known as the "browser script" layer. This is the layer of the application where window management takes place. The layer that actually manipulates the page/DOM elements is called the "client scripts" layer.

`site` contains all the assets for the "client scripts" and the markup for the web application. This is where the bulk of the code is.

There are also several files in the root directory of the project that are important...

`Makefile` this contains the commands to build the sia-ui project. You can build the project by running `make`, you'll have to do this anytime you make changes to the `site` directory.

`main.js` This is where the entire program begins, the code executed here is executed in the "browser scripts" layer and opens the initial application windows.

The `site` directory is essentially a website, however, atom-shell allows scripts to call on NodeJS modules which allows the website access to the file system, shell and other native functions that you would normally not have access to in a web application.

### Site Directory

Within the `site` directory there are several important folders and files...

`index.html` This is where the web application begins, this file should never be editted as it is generated from the markup directory (if you don't have this file, you need to build the application using `make`)

`assets` contains static data for the site (images etc.)
`libraries` external javascript/css libraries (jquery, font awesome...)

`markup` contains all the markup/elements that make up the application

`scripts` contains all the scripts and logic used to run the application

`stylesheets` contains all the styles to make the application pretty

### Organization of application windows/tabs

Each tab of the application (i.e. money, mining, hosting etc.) has it's own markup, script and stylesheet.

For example, the money/wallet tab has a script in `scripts/ui/views/money.js`, markup in `markup/pages/money.haml` and stylesheet in `stylesheets/money.less`. All the application windows/tabs are organized in this manner, so it should be relatively easy to make edits to any individual view.
