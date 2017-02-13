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
>
> **_.GITIGNORE AND README.MD_**
>
> \\==============================================================//

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

> //==============================================================\\
>
> **_EDITORS AND CONFIGURATION | EDITORCONFIG_**
>
> \\==============================================================//

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

> //==============================================================\\
>
> **_INSTALL NODE, NPM, GIT, BASH AND NSP_**
>
> \\==============================================================//

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

> //==============================================================\\
>
> **_EXPRESS AS OUR DEVELOPMENT WEB SERVER_**
>
> \\==============================================================//

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

> //==============================================================\\
>
> **_SHARING OUR WORK IN PROGRESS WITH LOCALTUNNEL_**
>
> \\==============================================================//

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

  localtunnel will return a url such as: <https://tbwsccjuzv.localtunnel.me/> from which we can access our app, you can provide this url to anyone to share yuor work in progress, we can even use this command:

  ```
  lt --port 3000 --subdomain asimtestapp
  ```

  It should return <https://asimtestapp.localtunnel.me/> that we can use.









