# vuepress-jsdoc

[![npm](https://img.shields.io/npm/v/vuepress-jsdoc.svg)](https://www.npmjs.com/package/vuepress-jsdoc)

This npm package is a command line script, which scans your JavaScript, Vue or Typescript source code and generates markdown files for vuepress with the help of [jsdoc-to-markdown](https://github.com/jsdoc2md/jsdoc-to-markdown).

## How to use?

```bash
yarn i vuepress-jsdoc -g
```

**Example:**

```bash
# search code in src and move it to code (./documentation/code) in your vuepress folder (./documentation)
vuepress-jsdoc --source=./src --dist=./documentation --folder=code --title=API
```

### Options

| name      | default         | description                                                  |
| --------- | --------------- | ------------------------------------------------------------ |
| --source= | ./src           | Source folder with .js or .ts files                          |
| --dist=   | ./documentation | Destination folder                                           |
| --folder= | ./code          | Folder inside destination folder. Gets overwritten everytime |
| --title=  | API             | Title of your documentation                                  |

### config.js

Inside your generated folder, you can find a `config.js`.
This file includes a complete filetree and an vuepress sidebar tree.

## How to configure vuepress

[Vuepress](https://vuepress.vuejs.org/) is a static site generator by Evan You.
You can add all generated documentation files to your existing vuepress project or create a new one.

```bash
# First install vuepress
npm i vuepress -g

# Run the CLI
vuepress-jsdoc

# Run vuepress dev server
vuepress dev ./documentation

# Run vuepress build, if you want to ship it
vuepress build ./documentation
```

**Access it via:** http://localhost:8080/code/

Now you need the sidebar.
Create a `.vuepress` folder inside the `documentation` folder and add the following `config.js`.

**config.js:**

```javascript
// auto generated sidebar
const { sidebarTree } = require('../code/config');

module.exports = {
  dest: 'dist',
  locales: {
    '/': {
      title: 'vuepress-jsdoc',
      description: 'Generate jsdoc markdown files for vuepress'
    }
  },
  themeConfig: {
    editLinks: true,
    sidebarDepth: 4,
    docsDir: 'code',
    locales: {
      '/': {
        nav: [
          {
            text: 'Home',
            link: '/'
          }
        ],
        // Add the generated sidebar
        sidebar: Object.assign({}, sidebarTree)
      }
    }
  }
};
```

## @vuepress comment block

You can add custom meta data to your pages
Simply add:

```javascript
/*
 * @vuepress
 * ---
 * title: You Custom Title
 * ---
 */
```

More inromation: https://vuepress.vuejs.org/guide/markdown.html#front-matter


## Example

The `./example` folder includes a full working vuepress-jsdoc example.

```bash
# Install dependencies
yarn

# Run the CLI
vuepress-jsdoc

# Generate docs
yarn run docs

# Run dev server
yarn run dev

# Generate dist folder
yarn run build
```

## ToDo

- [ ] Update description README.md
- [ ] Custom README.md
- [x] Custom meta data
