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

01. ) Start with an empty folder in your desktop and call it "settingup-js-dev-env", this is going to be your root directory, and we will call it your root.

01. ) Create README.md file in your root and write the following in it:
  
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

01. ) Create the file .editorconfig in your root with the following content, All future files created will be formatted based on the settings in this file.

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

01. ) Go to <www.editorconfig.org> to download and install your editor's plugin, now your editor will enforce the setting in the .editorconfig, 
don't forget to enable the plugin after you installed it. 

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

01. ) Install Git from: <https://git-scm.com/> this will also install Git Bash command line.

01. ) To Use Git Bash terminal within VS Code: <https://code.visualstudio.com/docs/editor/integrated-terminal>, this is very convenient.

01. ) Create a file called package.json in your root and paste the content of this [package.json](http://bit.ly/2kCyGv6) inside the package.json you just created, 
save it, then run:

```
npm install
```

For your convenience and just incase you were unable to get the package.json from the link above, copy and paste the following code inside the package.json file:

```
{
  "name": "javascript-development-environment",
  "version": "1.0.0",
  "description": "JavaScript development environment Pluralsight course by Cory House",
  "scripts": {
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

THis will install all the dependencies in the package.json to our project.

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
> **_SETTING UP EXPRESS AS A DEVELOPMENT WEB SERVER_**
>
> **_\\==============================================================//_**

01. ) Express is already installed in our project as it is one of the many packages included in the package.json file, to install it as a dev dependency run this command:

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

> **_//==============================================================\\_**
>
> **_TRANSPILING - BABEL_**
>
> **_\\==============================================================//_**

Transpiling means changing ES6 code (ES2015) into ES5 to ensure our JS code runs in the browsers that do not yet fully support the latest version of JS, we will now be 
using ES5 and Babel will transpile our code to ES5, we already installed Babel when we first ran "npm install" it is one of the many packages
included in our package.json, so we just have to configure it:

To configure babel:

01. ) Creating a .babelrc file in our root, then put this code in that file and save it:

  ```
  {
  "presets": [
    "latest"
    ]
  }
  ```

  here we are saying we want to use all the latest JS features, this is all it takes to have babel transpile our code.

  to test this:
   
01. ) Change our code from the current CommonJS module to ES6, lets start with the startMessage.js file, we will change it as follows:

    
    ```
    import chalk from 'chalk';

    console.log(chalk.green('Starting app in dev mode...'));
    ```

    Now to run this new ES6 code we have to change our npm script in the package.json to use babel to transpile the code before running it, 
    to do this we have to use the command "babel-node" instande of "node", so our package.json becomes:

    Observe the "prestart" script.

    ```
    {
      "name": "javascript-development-environment",
      "version": "1.0.0",
      "description": "JavaScript development environment Pluralsight course by Cory House",
      "scripts": {
        "prestart": "babel-node buildScripts/startMessage.js",
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

    If the app runs it means we have configured babel correctly and it is transpiling the ES6 code.

  > Note: If you keep getting errors attempt to install babel-cli globally by running the command: "npm install -g babel-cli"

01. ) Lets change all our node commands to use babel, by changing the npm scripts in the package.json file we will set our app up to use babel and ES6, observe 
  the changes in the scripts sections:

  ```
  {
    "name": "javascript-development-environment",
    "version": "1.0.0",
    "description": "JavaScript development environment Pluralsight course by Cory House",
    "scripts": {
      "prestart": "babel-node buildScripts/startMessage.js",
      "start": "npm-run-all --parallel security-check open:src",
      "open:src": "babel-node buildScripts/srcServer.js",
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
      "babel-cli": "^6.16.0",
      "babel-core": "^6.17.0",
      "babel-loader": "^6.2.5",
      "babel-preset-latest": "^6.16.0",
      "babel-register": "^6.16.3",
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

> **_//==============================================================\\_**
>
> **_WEBPACK - BUNDLING_**
>
> **_\\==============================================================//_**

01. ) Before we configure webpack, we will have to create an app that does something simple for demonstration purposes, to do this
 we will create a simple app that has several js files that webpack will bundle together into a single file called bundle.js, webpack will also bundle any css,
 and images into the bundle.js file, then webpack will inject this file in the index.html file, so now let's prepare things for webpack before we start using it.

01. ) We already have an index.html file, so let us add the following js files:

  01. ) Create an index.js file with the following code and save it under src:

    ```
    import talk from './talktoconsole';
    console.log(talk(1, 2));

    const button = document.createElement('button');
    button.innerText = 'Click me';
    button.onclick = () => {
        System.import('./image_viewer').then(module => {
            module.default();
        });
    };

    document.body.appendChild(button);
    ```

  01. ) Create the file talkToConsole.js with the following code:
    
    ```
    import numeral from 'numeral';

    const talk = (a, b) =>numeral(a + b).format('$0.0.00');

    export default talk;
    ```
  01. ) Create the file image_viewer.js with the following code:
  
    ```
    import small from '../assets/small.jpg';
    import big from '../assets/big.jpg';
    import './styles/image_viewer.css';

    export default () => {

        const smallImageDescription = document.createElement('p');
        smallImageDescription.innerText = 'This is a small Image that was small enough to be bundled into bundle.js';
        document.body.appendChild(smallImageDescription);

        const smallImage = document.createElement('img');
        smallImage.src = small;
        document.body.appendChild(smallImage);

        const bigImageDescription = document.createElement('p');
        bigImageDescription.innerText = 'This is a big Image, because it is large it was not bundled in bundle.js';
        document.body.appendChild(bigImageDescription);

        const bigImage = document.createElement('img');
        bigImage.src = big;
        document.body.appendChild(bigImage);

        const randomImageDescription = document.createElement('p');
        randomImageDescription.innerText = 'This is a random image generated from http://lorempixel.com/';
        document.body.appendChild(randomImageDescription);

        const randomImage = document.createElement('img');
        randomImage.src = 'http://lorempixel.com/400/200/';
        document.body.appendChild(randomImage);
    };
    ```

  01. ) Create a styles folder in the src folder, within the styles folder create a css file called style.css with the following css code:

  ```
  img {
      border: 10px solid red;
  }
  ```
  01. ) Create an asstes folder in the root directory and save the following images into them:

  http://lorempixel.com/200/200/ - call this small.jpg

  http://lorempixel.com/1200/1200/ - call this big.jpg

01. ) Now that we have a working app, we can now configure webpack, we also installed it when we first ran npm install, so now we just have to configure it, we will first have to create
  the file: webpack.config.js and add the following code to it:

  For more on the configuration of webpack 2: https://github.com/webpack/docs/wiki/configuration
  For more on webpack's cli commands: https://webpack.github.io/docs/cli.html

  ```
  const webpack = require('webpack');
  const path = require('path');
  const htmlWebpackPlugin = require('html-webpack-plugin');

  //our app third party dependencies
  const VENDOR_LIBS = [
    'faker', 'lodash', 'react', 'react-dom', 'react-input-range', 'react-redux',
    'react-router', 'redux', 'redux-form', 'redux-thunk', 'whatwg-fetch'
  ];

  const config = {
    //The entry point for the bundle.
    entry: {
      bundle: path.resolve(__dirname, 'src/index'),
      vendor: VENDOR_LIBS
    },
    output: {
      path: path.join(__dirname, 'build'),
      publicPath: '/',
      filename: '[name][chunkhash].js'
    },
    module: {
      rules: [
        {
          use: 'babel-loader', //here we are selecting the loader
          test: /\.js$/, //and here we specify which file the loader will process
          exclude: /node_modules/
        },
        {
          test: /\.css$/,
          use: ['style-loader', 'css-loader'],
        },
        {
          test: /\.(jpe?g|png|gif|svg)$/,
          use: [
            {
              loader: 'url-loader',
              options: { limit: 40000 }
            },
            'image-webpack-loader'
          ]
        }
      ]
    },
    plugins: [
        //this plugin will make sure there is no duplicate modules between vendor.js and bundle.js if there are it will remove them from bundle.js and put them in vendor.js
        new webpack.optimize.CommonsChunkPlugin({
              names: ['vendor', 'manifest']
        }),
        //this plugin will insert the script tags for bundle.js and vendor.js in our index.html
        new htmlWebpackPlugin({
              template: 'src/index.html' //if we do not specifiy a template, it will use the default one
        }),
        //when reactjs runs it looks for this window scoped variable called process.env.NODE_ENV,
        //if the value of this varaible is production react will not do too many error checking procedures,
        //which also takes too long to run.
        new webpack.DefinePlugin({
          'process.env.NODE_ENV': JSON.stringify(process.env.NODE_ENV)
        }),
        new webpack.LoaderOptionsPlugin({
          options: {
              noInfo: false,
              debug: true,
              devtool: 'inline-source-map',
              target: 'web',
          }
        })
    ]
  };

  module.exports = config;
  ```

With this configuration we can also use webpack as our dev server, to run the project using webpack dev server run this command:

```
webpack-dev-server
```

We can also still run our app through express using the command:

```
babel-node buildScripts/srcServer.js
```

01. ) Now we can modify our npm scripts to accomoodate the new functionality we have added:

```
{
  "name": "setting-up-javascript-react-development-environment",
  "version": "1.0.0",
  "description": "Setting up a React development environment with webpack",
  "scripts": {
    "prestart": "babel-node buildScripts/startMessage.js",
    "start": "npm-run-all --parallel security-check open:src",
    "open:src": "babel-node buildScripts/srcServer.js",
    "security-check": "nsp check",
    "localtunnel": "lt --port 3000",
    "share": "npm-run-all --parallel open:src localtunnel",
    "clean": "rimraf build",
    "serve": "webpack-dev-server"
  },
  "author": "Asim Abdelgadir",
  "license": "MIT",
  "dependencies": {
    "whatwg-fetch": "1.0.0",
    "faker": "^3.1.0",
    "lodash": "^4.17.2",
    "react": "^15.4.1",
    "react-dom": "^15.4.1",
    "react-input-range": "^0.9.2",
    "react-redux": "^4.4.6",
    "react-router": "^3.0.0",
    "redux": "^3.6.0",
    "redux-form": "^6.3.2",
    "redux-thunk": "^2.1.0"
  },
  "devDependencies": {
    "babel-cli": "^6.23.0",
    "babel-core": "^6.17.0",
    "babel-loader": "^6.2.5",
    "babel-preset-latest": "^6.16.0",
    "babel-preset-react": "^6.16.0",
    "babel-register": "^6.16.3",
    "chai": "3.5.0",
    "chalk": "1.1.3",
    "cheerio": "0.22.0",
    "compression": "1.6.2",
    "cross-env": "3.1.3",
    "css-loader": "^0.26.1",
    "eslint": "3.8.1",
    "eslint-plugin-import": "2.0.1",
    "eslint-watch": "2.1.14",
    "express": "4.14.0",
    "extract-text-webpack-plugin": "1.0.1",
    "html-webpack-plugin": "^2.28.0",
    "image-webpack-loader": "^3.2.0",
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
    "url-loader": "^0.5.7",
    "webpack": "2.2.0-rc.0",
    "webpack-dev-middleware": "1.8.4",
    "webpack-dev-server": "^2.3.0",
    "webpack-hot-middleware": "2.13.0",
    "webpack-md5-hash": "0.0.5"
  }
}
```
  

