---
layout: article
title:  "Node.js: ESlint + Prettier"
date:   2019-02-10 23:13:01 +0700
tags: eslint node.js prettier
---

# ESLint meets Prettier

We will begin with introducing Prettier to your ESLint. It would be perfect to setup it in such a way that not interested team members will not even know about it’s existence. Fortunately we have plugin for that: [eslint-plugin-prettier](https://github.com/prettier/eslint-plugin-prettier). It will add Prettier’s rules to ESLint configuration and allow ESLint to use Prettier as a code formatter with `--fix` command. There is also the second piece of this puzzle: [eslint-config-prettier](https://github.com/prettier/eslint-config-prettier). This config will disable all the ESLint rules that are in conflict with Prettier opinion, so there sould be no conflicts between them.

# Install ESLint and Prettier plugin and config

- In project directory:

```
$ npm install --save-dev eslint prettier eslint-plugin-prettier eslint-config-prettier
```

- To create and initialize ESLint configuration file `.eslintrc` run `eslint` command.

```
$ ./node_modules/.bin/esling --init
```

- Follow the instruction and choose **JASON** as configuration file type.

- Edit `.eslintrc` add `"prettier"` and `"plugin:prettier/recommended"` into **"extends"** section.

From this:
```
"extends": [
    "eslint:recommended"
],
```

To this:
```
"extends": [
    "prettier",
    "eslint:recommended",
    "plugin:prettier/recommended"
],
```

Source:

- [Your last ESLint config](https://medium.com/@netczuk/your-last-eslint-config-9e35bace2f99)
- [Configure ESLint, Prettier, and Flow in VS Code for React Development](https://medium.com/@sgroff04/configure-eslint-prettier-and-flow-in-vs-code-for-react-development-c9d95db07213)
- [Configuring ESLint](https://eslint.org/docs/user-guide/configuring)
