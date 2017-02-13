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

> **_//==============================================================\\_**
>
> **_.GITIGNORE AND README.MD_**
>
> **_\\==============================================================//_**

01. ) Start with an empty folder

01. ) Create README.md file and write the following.
  
   01. ) describe every step taken.
  
   01. ) every file created.
  
   01. ) every code written, new or updated and which file it was written in.
  
   01. ) every issue encountered why ti happened if possible and how it was solved with references and links.

   01. ) Create .gitignore with the following content:

```
node_modules
dist
build
```

> **_//==============================================================\\_**
>
> **_EDITORS AND CONFIGURATION | EDITORCONFIG_**
>
> **_\\==============================================================//_**

To make sure everyone is using the same editor setting we will enforce these setting through the editor config file.

01. ) Create the file .editorconfig in the root directory with the following content, All future files created will be formatted based on the settings in this file.

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

01. ) Go to <www.editorconfig.org> to download and install your editor's plugin, now your editor will enforce the setting in the .editorconfig.

> **_//==============================================================\\_**
>
> **_INSTALL NODE, NPM, GIT, BASH AND NSP_**
>
> **_\\==============================================================//_**

01. ) install node.js from: <https://nodejs.org/en/>

01. ) npm is part of the node.js installation, however, you can install it from the command line:

```
npm install npm -g
```

01. ) Install Git from: <https://git-scm.com/> this will also install Git Bash command line

01. ) Using Git Bash terminal within VS Code: <https://code.visualstudio.com/docs/editor/integrated-terminal>

01. ) Use the package.json found here: <bit.ly/jsdevpackagejson> and save it to the root of the project directory, then run:

```
npm install
```

to install all the dependencies in the package.json.

01. ) To scan all the dependencies in the package.json file we can use Node Security Platform, to install it run this command: run the command:

```
npm install nsp -g
```

then to run the security check run this command:

```
nsp check
```

> **_//==============================================================\\_**
>
> **_EXPRESS AS OUR DEVELOPMENT WEB SERVER_**
>
> **_\\==============================================================//_**

01. ) Express is already installed in our project as it is one of th emany packages included in the package.json file, to install it as a dev dependency run this command:

  ```
  npm install express --save-dev
  ```

  We will just need to configure it as follows:

01. ) Create a directory called src in the root, inside it create index.html with this code:

  ```
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <title></title>
      <meta charset="UTF-8">
    </head>
    <body>
      <h1>Hello World!</h1>
    </body>
  </html>
  ```

01. ) It is best to keep all the build tools in a single directory called buildScripts in the root of our project, inside the directory create the file srcServer.js
  in it put this code:
  
  ```
  var express = require('express');
  var path = require('path');
  var open = require('open');

  var port = 3000;
  var app = express();

  app.get('/', function(req, res) {
    res.sendFile(path.join(__dirname, '../src/index.html'));
  });

  app.listen(port, function(err) {
    if (err) {
      console.log(err);
    } else {
      open('http://localhost:' + port);
    }
  });
  ```

  now to run this file run this from the command line:

  ```
  node buildScripts/srcServer.js
  ```

  Express will open the browser with the page we just created, now we know we configured express correctly since it is listening to and serving our requests.

> **_//==============================================================\\_**
>
> **_SHARING OUR WORK IN PROGRESS WITH LOCALTUNNEL_**
>
> **_\\==============================================================//_**

01. ) Install localtunnel globally:

  ```
  npm install -g localtunnel
  ```

01. ) Run our app:

  ```
  node buildScripts/srcServer.js
  ```

  THe ap will open in the browser, Leave the app running

01. ) Open another command line and run localtunnel from there:

  ```
  lt --port 3000
  ```

  localtunnel will return a url such as: <https://tbwsccjuzv.localtunnel.me/> from which we can access our app, you can provide this url to anyone to share yuor work in progress, 
  we can even use this command:

  ```
  lt --port 3000 --subdomain asimtestapp
  ```

  It should return <https://asimtestapp.localtunnel.me/> that we can use.

  > **_//==============================================================\\_**
>
> **_AUTOMATION USING NPM SCRIPTS_**
>
> **_\\==============================================================//_**

npm scripts allows you to: make command line call, utilize npm packages, call separate scripts that use node, call separate files, create, update and remove files and directories
, which is very useful in creating a reliable build process, we can create npm scripts in the "script" section of the package.json.

also, with npm script we do not need to install npm modules globally to run them, when we run "npm install" to install all the packages listed in our package.json file they get added
to a ".bin" folder inside the "node_modules" folder of our root, this makes them available to our project, all those modules in the .bin folder are automatically in path when we call
 them from the command line in our root project folder.

01. ) This is how we create the "start" script in the package.json file:

  ```
  {
    "name": "javascript-development-environment",
    "version": "1.0.0",
    "description": "JavaScript development environment Pluralsight course by Cory House",
    "scripts": {
      "start": "node buildScripts/srcServer.js"
    },
    "author": "Cory House",
    "license": "MIT",
    "dependencies": {
      "whatwg-fetch": "1.0.0"
    },
    "devDependencies": {
      "babel-cli": "6.16.0",
      "babel-core": "6.17.0",
      "babel-loader": "6.2.5",
      "babel-preset-latest": "6.16.0",
      "babel-register": "6.16.3",
      "chai": "3.5.0",
      "chalk": "1.1.3",
      "cheerio": "0.22.0",
      "compression": "1.6.2",
      "cross-env": "3.1.3",
      "css-loader": "0.25.0",
      "eslint": "3.8.1",
      "eslint-plugin-import": "2.0.1",
      "eslint-watch": "2.1.14",
      "express": "4.14.0",
      "extract-text-webpack-plugin": "1.0.1",
      "html-webpack-plugin": "2.22.0",
      "jsdom": "9.8.0",
      "json-schema-faker": "0.3.6",
      "json-server": "0.8.22",
      "localtunnel": "1.8.1",
      "mocha": "3.1.2",
      "nock": "8.1.0",
      "npm-run-all": "3.1.1",
      "nsp": "2.6.2",
      "numeral": "1.5.3",
      "open": "0.0.5",
      "rimraf": "2.5.4",
      "style-loader": "0.13.1",
      "webpack": "1.13.2",
      "webpack-dev-middleware": "1.8.4",
      "webpack-hot-middleware": "2.13.0",
      "webpack-md5-hash": "0.0.5"
    }
  }
  ```
  now to run this script we run this in the command line:

  ```
  npm run start
  ```

  or

  ```
  npm start
  ```

  The same applies for "npm test", all other npm scripts must be used with the "run" key word.

01. ) Creating a script that displays a message when running the app:

  we do this by creating a startMessage.js file in the buildScripts folder with the following code:

  ```
  var chalk = require('chalk');
  console.log(chalk.green('Starting app in dev mode...'));
  ```

  then we write an npm script to run it before our app runs, this is done with the prefix "pre", there is also a "post" prefix, these are called hooks, 
  observe the script section of the package.json:

  ```
  {
    "name": "javascript-development-environment",
    "version": "1.0.0",
    "description": "JavaScript development environment Pluralsight course by Cory House",
    "scripts": {
      "prestart": "node buildScripts/startMessage.js",
      "start": "node buildScripts/srcServer.js"
    },
    "author": "Cory House",
    "license": "MIT",
    "dependencies": {
      "whatwg-fetch": "1.0.0"
    },
    "devDependencies": {
      "babel-cli": "6.16.0",
      "babel-core": "6.17.0",
      "babel-loader": "6.2.5",
      "babel-preset-latest": "6.16.0",
      "babel-register": "6.16.3",
      "chai": "3.5.0",
      "chalk": "1.1.3",
      "cheerio": "0.22.0",
      "compression": "1.6.2",
      "cross-env": "3.1.3",
      "css-loader": "0.25.0",
      "eslint": "3.8.1",
      "eslint-plugin-import": "2.0.1",
      "eslint-watch": "2.1.14",
      "express": "4.14.0",
      "extract-text-webpack-plugin": "1.0.1",
      "html-webpack-plugin": "2.22.0",
      "jsdom": "9.8.0",
      "json-schema-faker": "0.3.6",
      "json-server": "0.8.22",
      "localtunnel": "1.8.1",
      "mocha": "3.1.2",
      "nock": "8.1.0",
      "npm-run-all": "3.1.1",
      "nsp": "2.6.2",
      "numeral": "1.5.3",
      "open": "0.0.5",
      "rimraf": "2.5.4",
      "style-loader": "0.13.1",
      "webpack": "1.13.2",
      "webpack-dev-middleware": "1.8.4",
      "webpack-hot-middleware": "2.13.0",
      "webpack-md5-hash": "0.0.5"
    }
  }
  ```

  the script "prestart" will run before the "start" script, to see this in action run this command:

  ```
  npm start
  ```

01. ) Creating a script that runs the security check in parallel to the start script when the app starts, observe the "script section":

  ```
  {
    "name": "javascript-development-environment",
    "version": "1.0.0",
    "description": "JavaScript development environment Pluralsight course by Cory House",
    "scripts": {
      "prestart": "node buildScripts/startMessage.js",
      "start": "npm-run-all --parallel security-check open:src",
      "open:src": "node buildScripts/srcServer.js",
      "security-check": "nsp check"
    },
    "author": "Cory House",
    "license": "MIT",
    "dependencies": {
      "whatwg-fetch": "1.0.0"
    },
    "devDependencies": {
      "babel-cli": "6.16.0",
      "babel-core": "6.17.0",
      "babel-loader": "6.2.5",
      "babel-preset-latest": "6.16.0",
      "babel-register": "6.16.3",
      "chai": "3.5.0",
      "chalk": "1.1.3",
      "cheerio": "0.22.0",
      "compression": "1.6.2",
      "cross-env": "3.1.3",
      "css-loader": "0.25.0",
      "eslint": "3.8.1",
      "eslint-plugin-import": "2.0.1",
      "eslint-watch": "2.1.14",
      "express": "4.14.0",
      "extract-text-webpack-plugin": "1.0.1",
      "html-webpack-plugin": "2.22.0",
      "jsdom": "9.8.0",
      "json-schema-faker": "0.3.6",
      "json-server": "0.8.22",
      "localtunnel": "1.8.1",
      "mocha": "3.1.2",
      "nock": "8.1.0",
      "npm-run-all": "3.1.1",
      "nsp": "2.6.2",
      "numeral": "1.5.3",
      "open": "0.0.5",
      "rimraf": "2.5.4",
      "style-loader": "0.13.1",
      "webpack": "1.13.2",
      "webpack-dev-middleware": "1.8.4",
      "webpack-hot-middleware": "2.13.0",
      "webpack-md5-hash": "0.0.5"
    }
  }
  ```

  If you get too much info in the console, use:

  ```
  npm start -s
  ```

  which will run the script in silent mode.

01. ) Creating a script that runs localtunnel in parallel to the start script when the app starts, observe the "script section":

  ```
  {
    "name": "javascript-development-environment",
    "version": "1.0.0",
    "description": "JavaScript development environment Pluralsight course by Cory House",
    "scripts": {
      "prestart": "node buildScripts/startMessage.js",
      "start": "npm-run-all --parallel security-check open:src",
      "open:src": "node buildScripts/srcServer.js",
      "security-check": "nsp check",
      "localtunnel": "lt --port 3000",
      "share": "npm-run-all --parallel open:src localtunnel"
    },
    "author": "Cory House",
    "license": "MIT",
    "dependencies": {
      "whatwg-fetch": "1.0.0"
    },
    "devDependencies": {
      "babel-cli": "6.16.0",
      "babel-core": "6.17.0",
      "babel-loader": "6.2.5",
      "babel-preset-latest": "6.16.0",
      "babel-register": "6.16.3",
      "chai": "3.5.0",
      "chalk": "1.1.3",
      "cheerio": "0.22.0",
      "compression": "1.6.2",
      "cross-env": "3.1.3",
      "css-loader": "0.25.0",
      "eslint": "3.8.1",
      "eslint-plugin-import": "2.0.1",
      "eslint-watch": "2.1.14",
      "express": "4.14.0",
      "extract-text-webpack-plugin": "1.0.1",
      "html-webpack-plugin": "2.22.0",
      "jsdom": "9.8.0",
      "json-schema-faker": "0.3.6",
      "json-server": "0.8.22",
      "localtunnel": "1.8.1",
      "mocha": "3.1.2",
      "nock": "8.1.0",
      "npm-run-all": "3.1.1",
      "nsp": "2.6.2",
      "numeral": "1.5.3",
      "open": "0.0.5",
      "rimraf": "2.5.4",
      "style-loader": "0.13.1",
      "webpack": "1.13.2",
      "webpack-dev-middleware": "1.8.4",
      "webpack-hot-middleware": "2.13.0",
      "webpack-md5-hash": "0.0.5"
    }
  }
  ```

  This way we avoided opening two terminals at the same time like we did before when setting up localtunnel.










