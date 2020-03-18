---
layout: article
title:  "Expo: Configuration with app.json"
date:   2019-02-20 17:39:12 +0700
tags: expo react react-native
---

# Configuration with app.json

`app.json` is your go-to place for configuring parts of your app that don't belong in code. It is located at the root of your project next to your `package.json`. It looks something like this:
   
```json
{
  "expo": {
    "name": "My app",
    "slug": "my-app",
    "sdkVersion": "UNVERSIONED",
    "privacy": "public"
  }
}
```

## Properties

The following is a list of properties that are available for you under the `"expo"` key in `app.json`:

### `"name"

**Required.** The name of your app as it appears both within Expo and on your home screen as a standalone app.

> **ExpoKit:** To change the name of your app, edit the "Display Name" field in Xcode and the `app_name` string in `android/app/src/main/res/values/strings.xml`.

### `"description"`

A short description of what your app is and why it is great.

### `"slug"`

**Required.** The friendly url name for publishing. eg: `my-app-name` will refer to the `expo.io/@your-username/my-app-name` project.

### `"privacy"`

Either `public` or `unlisted`. If not provided, defaults to `unlisted`. In the future `private` will be supported. `unlisted` hides the experience from search results. Valid values: `public`, `unlisted`

### `"sdkVersion"`

**Required.** The Expo sdkVersion to run the project on. This should line up with the version specified in your package.json.

### `"version"`

Your app version; use whatever versioning scheme that you like.

> **ExpoKit:** To change your app version, edit the "Version" field in Xcode and the `versionName` string in `android/app/build.gradle`.

### `"platforms"`

Platforms that your project explicitly supports. If not specified, it defaults to `["ios", "android"]`.

### `"githubUrl"`

If you would like to share the source code of your app on Github, enter the URL for the repository here and it will be linked to from your Expo project page.

### `"orientation"`

Lock your app to a specific orientation with `portrait` or `landscape`. Defaults to no lock. Valid values: '`default`', '`portrait`', '`landscape`'

### `"primaryColor"`

On Android, this will determine the color of your app in the multitasker. Currently this is not used on iOS, but it may be used for other purposes in the future.

6 character long hex color string, eg: "`#000000`"

### `"icon"`

Local path or remote url to an image to use for your app's icon. We recommend that you use a 1024x1024 png file. This icon will appear on the home screen and within the Expo app.

> **ExpoKit:** To change your app's icon, edit or replace the files in `ios/<PROJECT-NAME>/Assets.xcassets/AppIcon.appiconset` (we recommend using Xcode), and `android/app/src/main/res/mipmap-<RESOLUTION>`. Be sure to follow the guidelines for each platform ([iOS](https://developer.apple.com/design/human-interface-guidelines/ios/icons-and-images/app-icon/), [Android 7.1 and below](https://material.io/design/iconography/#icon-treatments), and [Android 8+](https://developer.android.com/guide/practices/ui_guidelines/icon_design_adaptive)) and to provide your new icon in each existing size.

### `"appKey"`

By default, Expo looks for the application registered with the AppRegistry as `main`. If you would like to change this, you can specify the name in this property.

### `"androidShowExponentNotificationInShellApp"`

Adds a notification to your standalone app with refresh button and debug info.

### `"scheme"`

Standalone Apps Only. URL scheme to link into your app. For example, if we set this to `'demo'`, then demo:// URLs would open your app when tapped. String beginning with a letter followed by any combination of letters, digits, "+", "." or "-"

> **ExpoKit:** To change your app's scheme, replace all occurrences of the old scheme in `Info.plist`, `AndroidManifest.xml`, and `android/app/src/main/java/host/exp/exponent/generated/AppConstants.java`.

### `"entryPoint"`

The relative path to your main JavaScript file.

### `"extra"`

Any extra fields you want to pass to your experience. Values are accessible via Expo.Constants.manifest.extra ([read more](https://docs.expo.io/versions/latest/sdk/constants/#expoconstantsmanifest))

### `"rnCliPath"`

### `"packagerOpts"`

### `"ignoreNodeModulesValidation"`

### `"nodeModulesPath"`

### `"facebookAppId"`

Used for all Facebook libraries. Set up your Facebook App ID at [https://developers.facebook.com](https://developers.facebook.com/).

> **ExpoKit:** To change this field, edit `Info.plist`.

### `"facebookDisplayName"`

Used for native Facebook login.

> **ExpoKit:** To change this field, edit `Info.plist`.

### `"facebookScheme"`

Used for Facebook native login. Starts with 'fb' and followed by a string of digits, like 'fb1234567890'. You can find your scheme at [https://developers.facebook.com/docs/facebook-login/ios](https://developers.facebook.com/docs/facebook-login/ios) in the 'Configuring Your info.plist' section.

> **ExpoKit:** To change this field, edit `Info.plist`.

### `"locales"`

Provide overrides by locale for System Dialog prompts like Permissions alerts

> **ExpoKit:** To add or change language and localization information in your iOS app, you need to use Xcode.

### `"assetBundlePatterns"`

An array of file glob strings which point to assets that will be bundled within your standalone app binary. Read more in the [Offline Support guide](https://docs.expo.io/versions/latest/guides/offline-support/)

### `"androidStatusBar"`

Configuration for android statusbar.

```json
{
  "androidStatusBar": {
    /*
      Configure the statusbar icons to have light or dark color.
      Valid values: "light-content", "dark-content".
    */
    "barStyle": STRING,

    /*
      Configuration for android statusbar.
      6 character long hex color string, eg: "#000000"
    */
    "backgroundColor": STRING
  }
}
```

### `"splash"`

Configuration for loading and splash screen for standalone apps.

```json
{
  "splash": {
    /*
      Color to fill the loading screen background
      6 character long hex color string, eg: "#000000"
    */
    "backgroundColor": STRING,

    /*
      Determines how the "image" will be displayed in the splash loading screen.
      Must be one of "cover" or "contain", defaults to `contain`.
      Valid values: "cover", "contain"
    */
    "resizeMode": STRING,

    /*
      Local path or remote url to an image.
      Will fill the background of the loading/splash screen.
      Image size and aspect ratio are up to you. Must be a .png.
    */
    "image": STRING
  }
}
```

> **ExpoKit:** To change your iOS app's splash screen, use Xcode to edit `LaunchScreen.xib`. For Android, edit or replace the files in `android/app/src/main/res/drawable-<RESOLUTION>`; to change the background color, edit `android/app/src/main/res/values/colors.xml`; and to change the resizeMode, set `SHOW_LOADING_VIEW_IN_SHELL_APP` in `android/app/src/main/java/host/exp/exponent/generated/AppConstants.java` (`true` for `"cover"`, `false` for `"contain"`).

### `"notification"`

Configuration for remote (push) notifications.

```json
{
  "notification": {
    /*
      Local path or remote url to an image to use as the icon for push notifications.
      96x96 png grayscale with transparency.
    */
    "icon": STRING,

    /*
      Tint color for the push notification image when it appears in the notification tray.
      6 character long hex color string eg: "#000000"
    */
    "color": STRING,

    /*
      Show each push notification individually "default" or collapse into one "collapse".
      Valid values: "default", "collapse"
    */
    "androidMode": STRING,

    /*
      If "androidMode" is set to "collapse", this title is used for the collapsed notification message.
      eg: "#{unread_notifications} new interactions"
    */
    "androidCollapsedTitle": STRING
  }
}
```

> **ExpoKit:** To change the notification icon, edit or replace the `shell_notification_icon.png` files in `android/app/src/main/res/mipmap-<RESOLUTION>`. On iOS, notification icons are the same as the app icon. All other properties are set at runtime.

### `"hooks"`

Configuration for scripts to run to hook into the publish process

```json
{
  "hooks": {
    "postPublish": STRING
  }
}
```

### `"updates"`

Configuration for how and when the app should request OTA JavaScript updates

```json
{
  "updates": {
    /*
      If set to false, your standalone app will never download any code.
      And will only use code bundled locally on the device.
      In that case, all updates to your app must be submitted through Apple review.
      Defaults to true.

      Note that this will not work out of the box with ExpoKit projects.
    */
    "enabled": BOOLEAN,

    /*
      By default, Expo will check for updates every time the app is loaded.
      Set this to `'ON_ERROR_RECOVERY'` to disable automatic checking unless recovering from an error.

      Must be one of `ON_LOAD` or `ON_ERROR_RECOVERY`.
    */
    "checkAutomatically": STRING,

    /*
      How long (in ms) to allow for fetching OTA updates before falling back to a cached version of the app.

      Defaults to 30000 (30 sec). Must be between 0 and 300000 (5 minutes).
    */
    "fallbackToCacheTimeout": NUMBER
  }
}
```

> **ExpoKit:** To change the value of enabled, edit `ios/<PROJECT-NAME>/Supporting/EXShell.plist` and `android/app/src/main/java/host/exp/exponent/generated/AppConstants.java`. All other properties are set at runtime.

### `"ios"`

**Standalone Apps Only**. iOS standalone app specific configuration

```json
{
  "ios": {
    /*
      The bundle identifier for your iOS standalone app.
      You make it up, but it needs to be unique on the App Store.

      stackoverflow.com/questions/11347470/what-does-bundle-identifier-mean-in-the-ios-project.

      iOS bundle identifier notation unique name for your app.
      For example, host.exp.exponent, where exp.host is our domain
      and Expo is our app.

      ExpoKit: use Xcode to set this.
    */
    "bundleIdentifier": STRING,

    /*
      Build number for your iOS standalone app. Must be a string
      that matches Apple's format for CFBundleVersion.

      developer.apple.com/library/content/documentation/General/Reference/InfoPlistKeyReference/Articles/CoreFoundationKeys.html#//apple_ref/doc/uid/20001431-102364.

      ExpoKit: use Xcode to set this.
    */
    "buildNumber": STRING,

    /*
      Local path or remote URL to an image to use for your app's
      icon on iOS. If specified, this overrides the top-level "icon" key.

      Use a 1024x1024 icon which follows Apple's interface guidelines for icons, including color profile and transparency.

      Expo will generate the other required sizes.
      This icon will appear on the home screen and within the Expo app.
    */
    "icon": STRING,

    /*
      URL to your app on the Apple App Store, if you have deployed it there.
      This is used to link to your store page from your Expo project page if your app is public.
    */
    "appStoreUrl": STRING,

    /*
      Whether your standalone iOS app supports tablet screen sizes.
      Defaults to `false`.

      ExpoKit: use Xcode to set this.
    */
    "supportsTablet": BOOLEAN,

    /*
      If true, indicates that your standalone iOS app does not support handsets.
      Your app will only support tablets.

      ExpoKit: use Xcode to set this.
    */
    "isTabletOnly": BOOLEAN,

    /*
      Dictionary of arbitrary configuration to add to your standalone app's native Info.plist. Applied prior to all other Expo-specific configuration.

      No other validation is performed, so use this at your own risk of rejection from the App Store.
    */
    "infoPlist": OBJECT,

    /*
      An array that contains Associated Domains for the standalone app. See apple's docs for config: https://developer.apple.com/documentation/uikit/core_app/allowing_apps_and_websites_to_link_to_your_content/enabling_universal_links
      Entries must be prefixed with "www."

      ExpoKit: use Xcode to set this.
    */
    "associatedDomains": ARRAY,

    /*
      A boolean indicating if the app uses iCloud Storage for DocumentPicker.
      See DocumentPicker docs for details.

      ExpoKit: use Xcode to set this.
    */
    "usesIcloudStorage": BOOLEAN,

    /*
      Extra module configuration to be added to your app's native Info.plist.

      For ExpoKit apps, just add these to the Info.plist file directly.
    */
    "config": {
      /*
        Branch (https://branch.io/) key to hook up Branch linking services.
      */
      "branch": {
        /*
          Your Branch API key
        */
        "apiKey": STRING
      },

      /*
        Sets `ITSAppUsesNonExemptEncryption` in the standalone ipa's Info.plist to the given boolean value.
      */
      "usesNonExemptEncryption": BOOLEAN,

      /*
        Google Maps iOS SDK key for your standalone app.

        developers.google.com/maps/documentation/ios-sdk/start
      */
      "googleMapsApiKey": STRING,

      /*
        Google Sign-In iOS SDK keys for your standalone app.

        developers.google.com/identity/sign-in/ios/start-integrating
      */
      "googleSignIn": {
        /*
          The reserved client ID URL scheme.
          Can be found in GoogeService-Info.plist.
        */
        "reservedClientId": STRING
      }
    },

    "splash": {
      /*
        Color to fill the loading screen background 6 character long hex color string, eg: "#000000"
      */
      "backgroundColor": STRING,

      /*
        Determines how the "image" will be displayed in the splash loading screen.
        Must be one of "cover" or "contain", defaults to "contain".
        Valid values: "cover", "contain"
      */
      "resizeMode": STRING,

      /*
        Local path or remote url to an image to fill the background of the loading screen.
        Image size and aspect ratio are up to you.
        Must be a .png.
      */
      "image": STRING,

      /*
        Local path or remote url to an image to fill the background of the loading screen.
        Image size and aspect ratio are up to you.
        Must be a .png.
      */
      "tabletImage": STRING
    }
  }
}
```

### `"android"`

**Standalone Apps Only**. Android standalone app specific configuration

```json
{
  "android": {
    /*
      The package name for your Android standalone app.
      You make it up, but it needs to be unique on the Play Store.

      stackoverflow.com/questions/6273892/android-package-name-convention

      Reverse DNS notation unique name for your app.
      For example, host.exp.exponent, where exp.host is our domain and Expo is our app.
      The name may only contain lowercase and uppercase letters (a-z, A-Z),
      numbers (0-9) and underscores (_). Each component of the name should start
      with a lowercase letter.

      ExpoKit: this is set in `android/app/build.gradle` as well as your
      AndroidManifest.xml file (multiple places).
    */
    "package": STRING,

    /*
      Version number required by Google Play.
      Increment by one for each release.
      Must be an integer.
      developer.android.com/studio/publish/versioning.html

      ExpoKit: this is set in `android/app/build.gradle`.
    */
    "versionCode": NUMBER,

    /*
      Local path or remote url to an image to use for your app's icon on Android.
      If specified, this overrides the top-level "icon" key.

      We recommend that you use a 1024x1024 png file.
      Transparency is recommended for the Google Play Store.
      This icon will appear on the home screen and within the Expo app.
    */
    "icon": STRING,

    /*
      Settings for an Adaptive Launcher Icon on Android.
      https://developer.android.com/guide/practices/ui_guidelines/icon_design_adaptive

      ExpoKit: icons are saved in `android/app/src/main/res/mipmap-<RESOLUTION>-v26`
      and the "backgroundColor" is set in `android/app/src/main/res/values/colors.xml`.
    */
    "adaptiveIcon": {
      /*
        Local path or remote url to an image to use for
        the foreground of your app's icon on Android.

        We recommend that you use a 1024x1024 png file,
        leaving at least the outer 1/6 transparent on each side.
        If specified, this overrides the top-level "icon" and the "android.icon" keys.
        This icon will appear on the home screen.
      */
      "foregroundImage": STRING,

      /*
        Color to use as the background for your app's Adaptive Icon on Android.
        Defaults to white (#FFFFFF).

        Has no effect if "foregroundImage" is not specified.
      */
      "backgroundColor": STRING,

      /*
        Local path or remote url to a background image for
        the background of your app's icon on Android.

        If specified, this overrides the "backgroundColor" key.
        Must have the same dimensions as "foregroundImage", and has no effect if
        "foregroundImage" is not specified.
      */
      "backgroundImage": STRING
    },

    /*
      URL to your app on the Google Play Store, if you have deployed it there.
      This is used to link to your store page from your Expo project page if your app is public.
    */
    "playStoreUrl": STRING,

    /*
      List of additional permissions the standalone app will request upon installation,
      along with the minimum necessary for an Expo app to function.

      To use ALL permissions supported by Expo, do not specify the "permissions" key.

      To use ONLY the following minimum necessary permissions and none of the extras supported
      by Expo, set "permissions" to []. The minimum necessary permissions do not require a
      Privacy Policy when uploading to Google Play Store and are:

      • receive data from Internet
      • view network connections
      • full network access
      • change your audio settings
      • draw over other apps
      • prevent device from sleeping

      To use the minimum necessary permissions ALONG with certain additional permissions,
      specify those extras in "permissions", e.g.

      ["CAMERA", "RECORD_AUDIO"]

      ExpoKit: to change the permissions your app requests, you'll need to edit
      AndroidManifest.xml manually. To prevent your app from requesting one of the
      permissions listed below, you'll need to explicitly add it to `AndroidManifest.xml`
      along with a `tools:node="remove"` tag.
    */
    "permissions": [
      "ACCESS_COARSE_LOCATION",
      "ACCESS_FINE_LOCATION",
      "CAMERA",
      "MANAGE_DOCUMENTS",
      "READ_CONTACTS",
      "READ_CALENDAR",
      "WRITE_CALENDAR",
      "READ_EXTERNAL_STORAGE",
      "READ_PHONE_STATE",
      "RECORD_AUDIO",
      "USE_FINGERPRINT",
      "VIBRATE",
      "WAKE_LOCK",
      "WRITE_EXTERNAL_STORAGE",
      "com.anddoes.launcher.permission.UPDATE_COUNT",
      "com.android.launcher.permission.INSTALL_SHORTCUT",
      "com.google.android.c2dm.permission.RECEIVE",
      "com.google.android.gms.permission.ACTIVITY_RECOGNITION",
      "com.google.android.providers.gsf.permission.READ_GSERVICES",
      "com.htc.launcher.permission.READ_SETTINGS",
      "com.htc.launcher.permission.UPDATE_SHORTCUT",
      "com.majeur.launcher.permission.UPDATE_BADGE",
      "com.sec.android.provider.badge.permission.READ",
      "com.sec.android.provider.badge.permission.WRITE",
      "com.sonyericsson.home.permission.BROADCAST_BADGE"
    ],

    /*
      Location of the google-services.json file for configuring Firebase. Including this
      key automatically enables FCM in your standalone app.

      For ExpoKit apps, add or edit the file directly at `android/app/google-services.json`.
      To enable FCM, edit the value of `FCM_ENABLED` in
      `android/app/src/main/java/host/exp/exponent/generated/AppConstants.java`.
    */
    "googleServicesFile": STRING,

    /*
      Extra module configuration to be added to your app's native AndroidManifest.xml.

      For ExpoKit apps, just add these to the AndroidManifest.xml file directly.
    */
    "config": {
      /*
        Branch (https://branch.io/) key to hook up Branch linking services.
      */
      "branch": {
        /*
          Your Branch API key
        */
        "apiKey": STRING
      },

      /*
        Google Developers Fabric keys to hook up Crashlytics and other services.
        get.fabric.io/
      */
      "fabric": {
        /*
          Your Fabric API key
        */
        "apiKey": STRING,

        /*
          Your Fabric build secret
        */
        "buildSecret": STRING
      },

      /*
        Google Maps Android SDK key for your standalone app.
        developers.google.com/maps/documentation/android-api/signup
      */
      "googleMaps": {
        /*
          Your Google Maps Android SDK API key
        */
        "apiKey": STRING
      }

      /*
        Google Sign-In Android SDK keys for your standalone app.
        developers.google.com/identity/sign-in/android/start-integrating
      */
      "googleSignIn": {
        /*
          The Android API key.
          Can be found in the credentials section of the developer console
          or in "google-services.json"
        */
        "apiKey": STRING,

        /*
          The SHA-1 hash of the signing certificate used to build the apk without any separator `:`.
          Can be found in "google-services.json".
          developers.google.com/android/guides/client-auth
        */
        "certificateHash": STRING
      }
    },

    /*
      Configuration for loading and splash screen for standalone Android apps.
    */
    "splash": {
      /*
        Color to fill the loading screen background
        6 character long hex color string, eg: "#000000"
      */
      "backgroundColor": STRING,

      /*
        Determines how the "image" will be displayed in the splash loading screen.
        Must be one of "cover" or "contain", defaults to "contain".
        Valid values: "cover", "contain"
      */
      "resizeMode": STRING,

      /*
        Local path or remote url to an image to fill the background of the loading screen in 'cover' mode.
        Image size and aspect ratio are up to you.
        Pay extra attention to the size of each image.
        See here: https://docs.expo.io/versions/latest/guides/splash-screens.html#differences-between-environments-android
        Must be a .png
        For more information see https://developer.android.com/training/multiscreen/screendensities
      */
      "mdpi": STRING,   // natural sized image (baseline)
      "hdpi": STRING,   // scale 1.5x
      "xhdpi": STRING,  // scale 2x
      "xxhdpi": STRING, // scale 3x
      "xxxhdpi": STRING // scale 4x
    },

    /*
      Configuration for setting custom intent filters in Android manifest.
      The following example demonstrates how to set up deep links. When
      the user taps a link matching *.myapp.io, they will be shown a
      dialog asking whether the link should be handled by your app or by
      the web browser.

      The data attribute may either be an object or an array of objects.
      The object may have the following keys to specify attributes of URLs matched by the filter:

      - scheme (string): the scheme of the URL, e.g. "https"
      - host (string): the host, e.g. "myapp.io"
      - port (string): the port, e.g. "3000"
      - path (string): an exact path for URLs that should be matched by the filter, e.g. "/records"
      - pathPattern (string): a regex for paths that should be matched by the filter, e.g. ".*"
      - pathPrefix (string): a prefix for paths that should be matched by the filter, e.g. "/records/" will match "/records/123"
      - mimeType (string): a mime type for URLs that should be matched by the filter

      See Android's documentation for more details on intent filter matching:

      developer.android.com/guide/components/intents-filters

      You may also use an intent filter to set your app as the default handler
      for links (without showing the user a dialog with options). To do so, you
      must set "autoVerify": true on the filter object below, and then
      configure your server to serve a JSON file verifying that you own the
      domain. See Android's documentation for details:

      developer.android.com/training/app-links

      To add or edit intent filters in an ExpoKit project, edit AndroidManifest.xml directly.
    */
    "intentFilters": [
      {
        "action": "VIEW",
        "data": {
          "scheme": "https",
          "host": "*.myapp.io"
        },
        "category": [
          "BROWSABLE",
          "DEFAULT"
        ]
      }
    ]
  }
}
```

Source: [Configuration with app.json](https://docs.expo.io/versions/latest/workflow/configuration/)
