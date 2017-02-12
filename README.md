---
# SETTINGUP A JAVASCRIPT DEVELOPMENT ENVIRONMENT
---

* This markdown file was written based on the guidlines [here](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

* You can also use: <https://stackedit.io> to create a .md file in a WYSIWYG fashion.

* git repo: https://github.com/zonender/settingup-js-dev-env

* Author: [Asim Abdelgadir](https://github.com/zonender)

01. Start with an empty folder

02. Create README.md file and write the following:

    ⋅⋅01. describe every step taken
    ⋅⋅02. every file created
    ⋅⋅03. every code written, new or updated and which file it was written in.
    ⋅⋅04. every issue encountered why ti happened if possible and how it was solved with references and links.

03. Create .gitignore with the following content:

```
node_modules
dist
build
```

> _//==============================================================\\_**
> _EDITORS AND CONFIGURATION_** _| EDITORCONFIG_**
> _\\==============================================================//_**

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


