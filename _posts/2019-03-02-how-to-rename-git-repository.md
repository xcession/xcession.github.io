---
layout: article
title:  "Git: How to Rename Git Repository"
date:   2019-03-02 02:22 +0700
tags: git vcs rename
---

## Rename Git Repository

There are various possible interpretations of what is meant by renaming a git repository: the displayed name, the repository directory, or the remote repository name. Each requires different steps to rename.

### Displayed Name

Rename the displayed name (e.g., shown by `gitweb`):

- Edit `.git/description` to contain the repository's name.
- Save the file.

### Repository Directory

Git does not reference the name of the directory containing the repository, as used by `git clone master child`, so we can simply rename it:

- Open a command prompt (or file manager window).
- Change to the directory that contains the repository directory (i.e., do not go into the repository directory itself).
- Rename the directory (e.g., using `mv` from the command line or the `F2` hotkey from a GUI).

### Remote Repository

Rename a remote repository as follows:

- Go to the remote host (e.g., https://github.com/User/project.
- Follow the host's instructions to rename the project (will differ from host to host, but usually **Settings** is a good starting point).
- Go to your local repository directory (i.e., open a command prompt and change to the repository's directory).
- Determine the new URL (e.g., `git@github.com:User/project-new.git`)
- Set the new URL using git:

```
git remote set-url origin git@github.com:User/project-new.git
```

Source: [How to rename a git repository?](https://stackoverflow.com/questions/2041993/how-to-rename-a-git-repository)
