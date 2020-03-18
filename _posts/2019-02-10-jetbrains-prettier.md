---
layout: article
title:  "JetBrains: Prettier"
date:   2019-02-10 06:35:17 +0700
tags: jetbrains prettier webstorm
---

# Prettier

[Prettier](https://prettier.io/) is a tool to format `.js`, `.ts`, `.css`, `.less`, `.scss`, `.vue`, and `.json` code. With WebStorm, you can format selected code fragments as well as entire files or directories using the **Reformat with Prettier** action. WebStorm adds this action as soon as you install Prettier as a dependency in your project or globally on your computer.

## To install Prettier

- Open the embedded Terminal (`⌥F12`).

- At the command prompt, type `npm install --save-dev --save-exact prettier` or `npm install --global prettier`. Learn more about installation modes from the [Prettier](https://prettier.io/docs/en/install.html) official website. 

## To configure Prettier in WebStorm

- In the **Settings > Preferences** dialog (`⌘,`), click **JavaScript** under **Languages and Frameworks**, and then click **Prettier**.

- On the **Prettier** page, that opens, specify the path to the `prettier` package and choose the Node.js interpreter to use. This can be a [local Node.js interpreter](https://www.jetbrains.com/help/webstorm/developing-node-js-applications.html#ws_node_configure_local_node_interpreter) or a [Node.js on Windows Subsystem for Linux](https://www.jetbrains.com/help/webstorm/developing-node-js-applications.html#ws_node_wsl).

## To reformat code with Prettier

- Select the code fragment to reformat in the editor or select a file or a folder in the **Project** tool window and press `⌥⇧⌘P` or choose **Reformat with Prettier** on the context menu of the selection.

- Alternatively, press `⇧⌘A` and click **Reformat with Prettier** in the **Find Action** list.

WebStorm can apply the key code style rules from the Prettier's configuration to the WebStorm Code Style settings so that generated code (e.g. after refactoring or quick-fix) and the code that is already processed with Prettier are formatted consistently.

## To apply Prettier code style rules

In the project where Prettier is enabled, open `package.json` and click **Yes** in the pane at the top of the tab.

Source: [Prettier](https://www.jetbrains.com/help/webstorm/prettier.html)
