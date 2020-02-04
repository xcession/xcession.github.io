---
layout: article
title:  "VSCode: Launch VSCode from macOS Terminal"
date:   2018-08-23 01:32 +0700
tags: vscode macos terminal commandline
---

## Launching VSCode from Terminal

You can also run VSCode from the terminal by typing `code` after adding it to the path:

- Launch VSCode.
- Open the **Command Palette** (`⇧⌘P`) and type `shell command` to find the **Shell Command: Install 'code' command in PATH** command.
- Restart the terminal for the new `$PATH` value to take effect. You'll be able to type `code .` in any folder to start editing files in that folder.

> **Note:** If you still have the old `code` alias in your `.bash_profile` (or equivalent) from an early VS Code version, remove it and replace it by executing the **Shell Command: Install 'code' command in PATH** command.

To manually add VS Code to your path:

```
cat << EOF >> ~/.bash_profile
# Add Visual Studio Code (code)
export PATH="\$PATH:/Applications/Visual Studio Code.app/Contents/Resources/app/bin"
EOF
```

Start a new terminal to pick up your `.bash_profile` changes.

> **Note:** The leading slash `\` is required to prevent `$PATH` from expanding during the concatenation. Remove the leading slash if you want to run the export command directly in a terminal.

Source: [Running VS Code on macOS](https://code.visualstudio.com/docs/setup/mac)
