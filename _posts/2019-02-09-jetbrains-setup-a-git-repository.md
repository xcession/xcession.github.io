---
layout: article
title:  "JetBrains: Setup a Git Repository"
date:   2019-02-09 21:06:56 +0700
tags: jetbrains git repository
---

## Check out a project from a remote host (clone)

WebStorm allows you to check out (in Git terms **clone**) an existing repository and create a new project based on the data you've downloaded.

- From the main menu, choose **VCS | Checkout from Version Control**, or, if no project is currently opened, click **Get from Version Control** on the **Welcome** screen.

- In the **Get from Version Control** dialog, specify the URL of the remote repository you want to clone (you can click **Test** to make sure that connection to the remote can be established), or select one of the VCS hosting services on the left. If you are already logged in to the selected hosting service, completion will suggest the list of available repositories that you can clone.

- Click **Clone**. If you want to create a WebStorm project based on the sources you have cloned, click **Yes** in the confirmation dialog. Git root mapping will be automatically set to the project root directory.

## Put an existing project under Git version control

You can create a local Git repository based on an existing project sources.

### Associate the entire project into a single Git repository

- Open the project that you want to put under Git.

- Choose **Enable Version Control Integration** from the **VCS Operations Popup** `⌃V` or from the main **VCS** menu.

- Choose **Git** as the version control system and click **OK**.

- After VCS integration is enabled, WebStorm will ask you whether you want to share project settings files via VCS. You can choose **Always Add** to synchronize project settings with other repository users who work with WebStorm.

> Note, that this only applicable to Git and Mercurial.

### Associate different directories within the project with different Git repositories

- Open the project that you want to put under Git.

- From the main menu, choose **VCS | Import into Version Control | Create Git Repository**.

- In the dialog that opens, specify the directory where a new Git repository will be created.

> Git does not support external paths, so if you choose a directory that is outside your project root, make sure that the folder where the repository is going to be created also contains the project root.

- If you are creating multiple Git repositories inside the project structure, repeat the previous steps for each directory.

### Add files to the local repository

After you have [initialized a Git repository](https://www.jetbrains.com/help/webstorm/set-up-a-git-repository.html#put-existing-project-under-Git) for your project, you need to add project data to it.

- Open the **Version Control** tool window `⌘9` and switch to the **Local Changes** tab.

- Put any files in the **Unversioned Files** changelist under version control by pressing `⌥⌘A` or selecting **Add to VCS** from the context menu. You can either add the entire changelist, or select separate files.

You can also add files to your local Git repository from the Project tool window — select the files you want to add, and press `⌥⌘A` or choose **Git | Add** from the context menu.

When Git integration is enabled in your project, WebStorm suggests adding each newly created file under Git. You can change this behavior in the **Settings/Preferences** dialog `⌘,` under **Version Control | Confirmation**). If you want certain files to always remain unversioned, you can [configure Git to ignore them](https://www.jetbrains.com/help/webstorm/set-up-a-git-repository.html#ignore-files).

## Exclude files from version control (ignore)

Sometimes you may need to leave files of certain types unversioned. These can be VCS administration files, artifacts of utilities, backup copies, and so on. You can ignore files through WebStorm, and the IDE will not suggest adding them to Git and will highlight them as ignored.

You can only ignore __unversioned__ files, that is files that you see in the **Unversioned Files** changelist. If a file is [added to Git](https://www.jetbrains.com/help/webstorm/set-up-a-git-repository.html#add-new-files) but not [committed](https://www.jetbrains.com/help/webstorm/commit-and-push-changes.html), you can right-click it in the **Local Change** tab of the **Version Control** tool window `⌘9` and choose **Rollbal**.

Git lets you ignored the file patterns in two kinds of configuration files:

- `.git/info/exclude` file.
    Pattern listed in this file only apply to the local copy of the repository.

    This file is created automatically when you initialize or check out a Git repository.

- One or more `.gitignore` files in the VCS root directory and it's subdirectories.
    These files are checked into the repository so that the ignore patterns in them are available to the entire team. Therefore, it is a most common place to store the ignore file patterns.

    If there is no `.gitignore` files in the VCS root directory, you can right-click anywhere in the Project window, choose **New | File** and type `.gitignore` in the **New File** dialog.

### Add files to .gitignore or .git/info/exclude

- Decide what [kind of Git configuration file](https://www.jetbrains.com/help/webstorm/set-up-a-git-repository.html#add_gitignore) you are going to use to ignore files. If in doubt, use `.gitignore`.

- Locate the unversioned file or folder you want to ignore in the **Local Changes** tab of the **Version Control** tool window `⌘9` or in Project tool window. [File colors in these views](https://www.jetbrains.com/help/webstorm/file-status-highlights.html) help you identify the status of the file.

- Right clickk the selection and choose **Git | Add to .gitignore** or **Git | Add to .git/info/exclude**. [File colors in these views](https://www.jetbrains.com/help/webstorm/file-status-highlights.html) help you identify the status of the file.

## Check project status

WebStorm allows you to check the status of your local working copy compared to the repository version of the project. It uses [specific colors](https://www.jetbrains.com/help/webstorm/file-status-highlights.html) to let you see which files have been modified, which new files have been added to the VCS, and which files are not being tracked by Git.

Open the **Version Control** tool window `⌘9` and switch to the **Local Changes** tab.

- The **Default** changelist shows all files that have been modified since you last synchronized with the remote repository (highlighted in blue), and all new files that have been added to the VCS but have not been committed yet (highlighted in green).

- The **Unversioned Files** changelist shows all files that have been added to your project, but that are not being tracked by Git.

If there were conflicts during a merge that were not resolved, the **Merge Conflicts** node will appear in the corresponding changelist with a link to [resolve](https://www.jetbrains.com/help/webstorm/resolve-conflicts.html) them.

For more info on changelists, see [Group changes into different changelists](https://www.jetbrains.com/help/webstorm/work-on-several-features-simultaneously.html#changelists).

### Track changes to a file in the editor

You can also track changes to a file as you modify it in the editor. All changes are highlighted with **change markers** that appear in the left gutter next to the modified lines, and show the type of changes introduced since you last [synchronized with the repository](https://www.jetbrains.com/help/webstorm/sync-with-a-remote-repository.html). When you commit changes to the repository, change markers disappear.

The changes you introduce to the text are color-coded:

- [green] line added.

- [blue] line changed.

> You can customize the default colors for line statuses in the **Preferences** dialog `⌘,` under **Editor | Color Scheme | VCS**.

When you delete a line, the following marker appears in the gutter: ►.

You can manage changes using a toolbar that appears when you hover the mouse cursor over a change marker and then click it. The toolbar is displayed together with a frame showing the previous contents of the modified line:

You can rollback changes by clicking the **Rollback** icon and explore the differences between the current and the repository version of the current line by clicking the **Diff** icon.

Instead of reverting the whole file, you can copy any part of the contents of this popup and paste it into the editor.

## Add a remote repository

To be able to collaborate on your Git project, you need to configure remote repositories that you [fetch](https://www.jetbrains.com/help/webstorm/sync-with-a-remote-repository.html#fetch) data from and [push](https://www.jetbrains.com/help/webstorm/commit-and-push-changes.html) to when you need to share your work.

If you have [cloned a remote Git repository](https://www.jetbrains.com/help/webstorm/set-up-a-git-repository.html#clone-repo), for example from [GitHub](https://github.com/), the remote is configured automatically and you do not have to specify it when you want to synchronize with it (in other words, when you perform a [pull](https://www.jetbrains.com/help/webstorm/sync-with-a-remote-repository.html#pull) or a [push](https://www.jetbrains.com/help/webstorm/commit-and-push-changes.html) operation). The default name Git gives to the remote you've cloned from is **origin**.

However, if you [created a Git repository](https://www.jetbrains.com/help/webstorm/set-up-a-git-repository.html#put-existing-project-under-Git) based on local sources, you need to add a remote repository for other contributors to be able to push their changes to it, and for you to be able to share the results of your work.

### Define a remote

- Create an empty repository on any Git hosting, such as [Bitbucket](https://bitbucket.org/) or [Github](https://github.com/).

- Invoke the **Push** dialog when you are ready to push your commits by selecting **VCS | Git | Push** from the main menu, or press `⇧⌘K`.

- If you haven't added any remotes so far, the **Define remote** link will appear instead of a remote name. Click it to add a remote.

- In the dialog that opens, specify the remote name and the URL where it will be hosted, and click **OK**.

In some cases, you also need to add a second remote repository. This may be useful, for example, if you have cloned a repository that you do not have write access to, and you are going to push changes to your own [fork](https://www.jetbrains.com/help/webstorm/contribute-to-projects.html#fork) of the original project. Another common scenario is that you have cloned your own repository that is somebody else's project fork, and you need to synchronize with the original project and fetch changes from it.

### Add a second remote

- From the main menu, choose **VCS | Git | Remotes**. The **Git Remotes** dialog will open.

- Click the **Add +** button on the toolbar or press `⌘N`.

- In the dialog that opens, specify the remote name and URL and click **OK**.

To edit a remote (for example, to change the name of the original project that you have cloned), select it in the **Git Remotes** dialog and click the **Edit** button on the toolbar, or press `⏎`.

> You can also edit a remote from the [Push Dialog](https://www.jetbrains.com/help/webstorm/push-dialog-mercurial-git.html?keymap=secondary_default_for_macos&section=macOS) by clicking its name.

To remove a repository that is no longer valid, select it in the **Git Remotes** dialog and click the **Remove -** button on the toolbar, or press `⌘⌦`.

Source:

- [Set up a Git repository](https://www.jetbrains.com/help/webstorm/set-up-a-git-repository.html)
- [How do I start working with Open Source and GitHub?](https://www.youtube.com/watch?v=lyiBnyPPnG4)
