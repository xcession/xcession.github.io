---
layout: article
title:  "JetBrains: Manage Project Hosted on GitHub"
date:   2019-02-09 19:21:13 +0700
tags: jetbrains github vcs
---

# Check out a project (clone)

You can clone a repository that you want to contribute to directly from WebStorm and create a new project based on it.

- From the main menu, choose **VCS > Checkout from Version Control > Git**.

- In the **Clone Repository** dialog, specify the URL of the repository that you want to clone. You can select a repository from the list of all GitHub projects associated with your account and the organization that your account belongs to.

- In the **Directory** field, enter the path to the folder where your local Git repository will be created.

- Click **Clone**. If you want to create a project based on these sources, click Yes in the confirmation dialog. WebStorm will automatically set Git root mapping to the project root directory.

# Share a project on GitHub

You can add a remote GitHub repository for a project you are developing locally, so that others can view it or contribute to it.

- Open the project you want to share.

- From the main menu, choose **VCS > Import into Version Control > Share Project on GitHub**.

    If you have already [registered your GitHub account](https://www.jetbrains.com/help/webstorm/github.html#register-account) in WebStorm, connection will be established using these credentials.

    If you have not registered your account in WebStorm, the **Login to GitHub** dialog opens. Specify your access token or request a new one with your login and password.

- When connection to GitHub has been established, the **Share Project on GitHub** dialog opens. Specify the new repository name, the name of the remote, and enter a description of your project.

    You can select the **Private** option if you do not want to allow public access to your repository for other GitHub users (note that this option is unavailable for free accounts).

- Click **Share** to initiate a new repository and upload project sources to it.

# Jump to the GitHub version of a file

You can jump from WebStorm to the GitHub version of a file. WebStorm detects which branch is currently active as well as the latest revision of the file, and opens the GitHub copy of the selected file in the corresponding commit in your web browser. If you are opening the GitHub file version from the editor, the file will be also automatically scrolled to the current line.

- Select a file in the editor or in the Project view, and choose **Open on GitHub** from the context menu or from the `⇧⌘A` popup. The remote version of the file will open in the browser.

    If the file points to more than one remote, you will be prompted to select the appropriate repository.

Source: [Manage projects hosted on GitHub](https://www.jetbrains.com/help/webstorm/manage-projects-hosted-on-github.html)
