---
layout: article
title:  "JetBrains: Developing Mobile Apps with React Native in WebStorm"
date:   2019-02-08 05:25:25 +0700
tags: jetbrains webstorm react react-native
---

# Install React Native CLI

Make sure you have a React Native CLI installed on your machine. To install it, run the following command in the Terminal:

```
$ npm install -g react-native-cli
```

The list of tools you need to install to get started with React Native depends on your OS and the mobile platform you’re going to target your app at. Check out [React Native’s Getting Started guide](https://facebook.github.io/react-native/docs/getting-started.html) for detailed installation instructions.

# Creating a new project

Now you can create a new React Native project right from the IDE Welcome screen:

- click **Create new project**, select React Native from the list on the left, enter a project name and click OK.

WebStorm will run a project generator and install all the required dependencies.

Of course you can also open an existing project or check one out from version control.

We recommend that you exclude **android** and **ios** folders from the project. To do that, right-click on a folder in the Project view and select **Mark as Excluded**.

# Running and debugging the app

Now that we have our app’s code in the IDE, let’s run it.

We’ll need to create a new **React Native run/debug configuration**. In the Run menu, select **Edit configurations…**, click the + button and select **React Native** from the list.

To start your React Native app for the first time, you need to do two things: run React Native bundler/packager and then build and launch an app on a simulator or a device using the `react-native run-ios` or `react-native run-android` command. Only after that, you can start debugging it.

With the **Build and Launch Application** option checked, WebStorm will do all that for you – you just need to select the target platform, iOS or Android, make sure the path to the React Native CLI package is correct and click Ok.

If you’re going to run your app on Android, don’t forget to start the [Android Virtual Device](https://facebook.github.io/react-native/docs/getting-started.html#starting-the-android-virtual-device) first. You can also run your app on a real [Android device connected via USB](https://facebook.github.io/react-native/docs/running-on-device.html#running-your-app-on-android-devices) (for that don’t forget to [enable USB debugging](https://developer.android.com/training/basics/firstapp/running-app.html)).

Now let’s run the created configuration – click the green debug icon next to the configuration name in the IDE toolbar. WebStorm will start the [React Native packager](https://github.com/facebook/react-native/tree/master/packager) first in a new React Native tool window and then will run the `react-native run-ios` or `react-native run-android` command, depending on the selected target platform.

If the build is successful, you’ll see your app in an emulator.

Once the emulator opens for the first time, go to the [in-app developer menu](https://facebook.github.io/react-native/docs/debugging.html#accessing-the-in-app-developer-menu) and select **Remote JS Debugging**.

WebStorm’s built-in debugger will then connect to the emulator, and you’ll be able to hit the breakpoints you put in your source code.

In the debugger you can step through your code, set watches, and explore the call stack and variable values.

If it’s not the first time you run your app and you haven’t made any changes to the native code since the last build, you don’t really need to rebuild the app – you can just run bundler, open the app in the simulator and then debug it.

In this case, create a new configuration (or modify the one you’ve already created) and uncheck the **Build and Launch Application** checkbox in it. When you debug this configuration, WebStorm will run React Native bundler and will wait for you to open an app in the simulator with the **Remote debug** enabled in the app.

There’s also now more flexibility with running React Native bundler. It’s now listed as a Before Launch task in the React Native configuration. By default, it will run `react-native start`. You can also select an npm task from your project’s package.json that will start the bundler.

Or if you have bundler already running, you can simply remove this step from the configuration (because you don’t need to run more than one bundler per app).

If you are using Expo in your app, please see this [blog post](https://blog.jetbrains.com/webstorm/2018/02/webstorm-2018-1-eap-181-3263/#debugging-expo for the steps.)

## Coding assistance

As you may know, WebStorm has support for React and JSX that will surely be helpful when building a React Native app. This includes: code completion for attributes, events and required properties for React components; navigation to the definition and completion for custom components; refactorings for component names; and lots more. Check out our blog post, [Working with React in WebStorm: coding assistance](https://blog.jetbrains.com/webstorm/2015/10/working-with-reactjs-in-webstorm-coding-assistance/).

WebStorm 2016.3 also adds code completion for React Native StyleSheet properties:

If you’re using Flow in your project, WebStorm can highlight the errors from Flow in the editor. Enable Flow as a JavaScript version in **Preferences > Languages & Frameworks > JavaScript** and specify a path to the Flow executable. Find out more about using Flow in this [blog post](https://blog.jetbrains.com/webstorm/2016/11/using-flow-in-webstorm/).

Source: [Developing mobile apps with React Native in WebStorm](https://blog.jetbrains.com/webstorm/2016/12/developing-mobile-apps-with-react-native-in-webstorm/)
