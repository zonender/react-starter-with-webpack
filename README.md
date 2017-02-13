---
# SETTINGUP A JAVASCRIPT DEVELOPMENT ENVIRONMENT
---

* Start Date: 12 Feb 2017 

* This markdown file was written based on the guidlines [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

* You can also use: <https://stackedit.io> to create a .md file in a WYSIWYG fashion.

* git repo: https://github.com/zonender/settingup-js-dev-env

* Author: [Asim Abdelgadir](https://github.com/zonender)

* OS: Windows 10 (64-bit)

* Browser: Chrome Version 56.0.2924.87 (64-bit)

* Editor: Visual Studio Code version 1.9.1

* VS CODE File Icon theme: Go to the plugins side menu: type: vscode-icons, locate the plugin, install it, reload, then goto File > Preferences > select "File Icon Theme".

* Node version: 7.5.0

* npm version: 4.2.0

* Command language (SHELL): Git Bash version: 2.11.1 (64-bit)

* Version control: Git version: 2.11.1 (64-bit) and <www.github.com>

> //==============================================================\\
> _.GITIGNORE AND README.MD_**
> \\==============================================================//

01. Start with an empty folder

02. Create README.md file and write the following:
    ⋅⋅01. describe every step taken.
    ⋅⋅02. every file created.
    ⋅⋅03. every code written, new or updated and which file it was written in.
    ⋅⋅04. every issue encountered why ti happened if possible and how it was solved with references and links.

03. Create .gitignore with the following content:

```
node_modules
dist
build
```

> //==============================================================\\
> _EDITORS AND CONFIGURATION_** _| EDITORCONFIG_**
> \\==============================================================//

To make sure everyone is using the same editor setting we will enforce these setting through the editor config file.

01. Create the file .editorconfig in the root directory with the following content, All future files created will be formatted based on the settings in this file.

```
# editorconfig.org
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.md]
trim_trailing_whitespace = false
```

02. Go to <www.editorconfig.org> to download and install your editor's plugin, now your editor will enforce the setting in the .editorconfig.

> //==============================================================\\
> _INSTALL NODE, NPM, GIT, BASH AND NSP_**
> \\==============================================================//

01. install node.js from: <https://nodejs.org/en/>

02. npm is part of the node.js installation, however, you can install it from the command line:

```
npm install npm -g
```

03. Install Git from: <https://git-scm.com/> this will also install Git Bash command line

04. Using Git Bash terminal within VS Code: <https://code.visualstudio.com/docs/editor/integrated-terminal>

05. Use the package.json found here: <bit.ly/jsdevpackagejson> and save it to the root of the project directory, then run:

```
npm install
```

to install all the dependencies in the package.json.

06. To scan all the dependencies in the package.json file we can use Node Security Platform, to install it run this command: run the command:

```
npm install nsp -g
```

then to run the security check run this command:

```
nsp check
```

> //==============================================================\\
> _DEVELOPMENT WEB SERVER_**
> \\==============================================================//

07. Using 

```

```

