---
layout: article
title:  "HTML: Adding the Favicon"
date:   2018-07-03 03:46:22 +0700
tags: html favicon
---

# Adding the Favicon

Place the following the `<head>` section of the HTML file.

```
<!-- For IE 9 and below. ICO should be 32x32 pixels in size -->
<!--[if IE]>
<link rel="shortcut icon" href="path/to/favicon.ico">
<![endif]-->
```

```
<!-- Touch Icons - iOS and Android 2.1+ 180x180 pixels in size. -->
<link rel="apple-touch-icon-precomposed" href="apple-touch-icon-precomposed.png">
```

```
<!-- Firefox, Chrome, Safari, IE 11+ and Opera. 196x196 pixels in size. -->
<link rel="icon" href="path/to/favicon.png">
```

# Force refresh the Favicon

To refresh your site's favicon you can force browsers to download a new version using the link tag and a querystring on your filename. This is especially helpful in production environments to make sure your users get the update.

```
<link rel="icon" href="http://www.yoursite.com/favicon.ico?v=2">
```

Source:

- [How do you add a Favicon with HTML5?](https://www.quora.com/How-do-you-add-a-Favicon-with-HTML5)
- [How do I force a favicon refresh](https://stackoverflow.com/questions/2208933/how-do-i-force-a-favicon-refresh)
