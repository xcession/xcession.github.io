---
layout: article
title:  "Manage Dotfiles with a Bare Git Repository"
date:   2020-02-03 23:34:59 +0700
tags: dotfiles git github
---

## Setup

Git is the only dependency. The following four lines will set up the bare repository.

```
git init --bare $HOME/.dotfiles.git
echo 'alias dotfiles="/usr/bin/git --git-dir=$HOME/.dotfiles.git --work-tree=$HOME"' >> $HOME/.zshrc
source ~/.zshrc
dotfiles config --local status.showUntrackedFiles no
```

1. Create a git bare repository at `~/.dotfiles.git` to track files.
2. Add alias setting to shell configuration file. (In this case zsh so it's `.zshrc`. For bash, it'd be `.bashrc`.)
3. Reload the shell setting.
4. Prevent untracked files from showing up when we call `dotfiles status`.

That finishes the setup. Use the aliased command from the home directory to manage files, and use git remote repo if you want to manage the files online.

```
dotfiles status
dotfiles add .vimrc
dotfiles commit -m "Add vimrc"
dotfiles remote add origin https://www.github.com/username/repo.git
dotfiles push origin master
```

## Installing dotfiles to another system

It just needs two shell commands before fetching the remote repo.

```
echo 'alias dotfiles="/usr/bin/git --git-dir=$HOME/.dotfiles.git --work-tree=$HOME"' >> $HOME/.zshrc
source ~/.zshrc
echo ".dotfiles.git" >> .gitignore
git clone --bare https://www.github.com/username/repo.git $HOME/.dotfiles.git
dotfiles checkout
dotfiles config --local status.showUntrackedFiles no
```

1. Create alias to ensure that the git bare repository works without problem.
2. Reload the shell setting to use that alias.
3. Add `.dotfiles.git` directory to `.gitignore` to prevent recursion issues.
4. Clone the repo.
5. Check if it works fine.
6. If you already have configuration files with identical names, checkout will fail. Backup and remove those files. Skip backup if you don't need them.
7. Prevent untracked files from showing up on `dotfiles status`.

Source:
- [Manage Dotfiles With a Bare Git Repository](https://harfangk.github.io/2016/09/18/manage-dotfiles-with-a-git-bare-repository.html)
- [What is a bare git repository?](http://www.saintsjd.com/2011/01/what-is-a-bare-git-repository/)
- [The best way to store your dotfiles: A bare Git repository](https://www.atlassian.com/git/tutorials/dotfiles)
