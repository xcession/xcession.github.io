---
layout: article
title:  "JetBrains: ESLint"
date:   2019-02-10 07:05:59 +0700
tags: jetbrains eslint webstorm
---

## ESLint

WebStorm integrates with [ESLint](http://eslint.org/) which brings a wide range of linting rules that can also be extended with plugins. WebStorm shows warnings and errors reported by ESLint right in the editor, as you type. With ESLint, you can also use [JavaScript Standard Style](https://standardjs.com/).

To view the description of a problem, hover over the highlighted code.

### Installing, enabling, and configuring ESLint in WebStorm

- Open the built-in WebStorm **Terminal** (`⌥F12`) and type `npm install eslint --save-dev` or `npm install eslint -g` at the command prompt.

- Optionally, install additional plugins, for example, [eslint-plugin-react](https://www.npmjs.com/package/eslint-plugin-react) to lint React applications.

- In the **Settings > Preferences** dialog (`⌘,`), choose **JavaScript** under **Languages and Frameworks** and then choose **ESLint** under **Code Quality Tools**. On the **ESLint page** page that opens, select the **Enable** checkbox. After that the controls on the page become available.

- In the **Node Interpreter** field, specify the path to Node.js. If you followed the standard installation procedure, WebStorm detects the path and fills in the field itself.

- In the **ESLint Package** field, specify the location of the `eslint` or `standard` package.

- Choose the configuration to use.
    - With **Automatic search**, WebStorm looks for a `.eslintrc` file or tries to detect a configuration defined under `eslintConfig` in a `package.json`. WebStorm first looks for a `.eslintrc` or `package.json` in the folder with the file to be linted, then in its parent folder, and so on up to the project root.

    - Choose **Configuration File** to use a custom file and specify the file location in the **Path** field.

- Optionally:

    - In the **Extra ESLint Options** field, specify additional command line options to run ESLint with, use spaces as separators.

    - In the **Additional Rules Directory** field, specify the location of the files with additional code verification rules. These rules will be applied after the rules from `.eslintrc` or the above specified custom configuration file and accordingly will override them.

### Configuring highlighting for ESLint

By default, WebStorm marks the detected errors and warnings based on the severity levels from the ESLint configuration. For example, errors are highlighted with a red squiggly line, while warnings are marked with a yellow background.

#### To change the severity level of a rule in the ESLint configuration

In `.eslintrc` or under **eslintConfig** in `package.json`, locate the rule you want to edit and set its ID to **1 (warn)** or to **2 (error)**. Learn more from the [ESLint](https://eslint.org/docs/user-guide/configuring#configuring-rules) official website.

#### To ignore the severity levels from the configuration

- In the **Settings > Preferences** dialog (`⌘,`), select **Editor > Inspections**. The [Inspections page](https://www.jetbrains.com/help/webstorm/inspection-settings.html) opens.

- In the central pane, go to **JavaScript > Code quality tools > ESLint**.

- In the right-hand pane, clear the **Use rule severity from the configuration file** checkbox and select the severity level to use instead of the default one.

### Importing code style from ESLint

You can import some of the [ESLint code style rules](http://eslint.org/docs/rules/) to the WebStorm [JavaScript code style settings](https://www.jetbrains.com/help/webstorm/settings-code-style-javascript.html). That enables WebStorm to use more accurate code style options for your project when auto-completing, generating, or refactoring the code or adding import statements. When you use the Reformat action, WebStorm will then no longer break properly formatted code from the ESLint perspective.

WebStorm understands ESLint configurations in all official formats: `.eslintrc` JSON files, `package.json` files with the **eslintConfig** field, as well as JavaScript and YAML configuration files.

- When you open your project for the first time, WebStorm imports the code style from the project ESLint configuration automatically.

- If your ESLint configuration is updated (manually or from your version control), open it in the editor and choose **Apply ESLint Code Style Rules** on the context menu:

Alternatively, just answer **Yes** to the "**Apply code style from ESLint?**" question on top of the file:

The list of applied rules is shown in the Event log tool window:

Source: [ESLint](https://www.jetbrains.com/help/webstorm/eslint.html)
