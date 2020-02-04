---
layout: article
title:  "Gatsby.js Adding Offline Support"
date:   2019-11-16 16:31 +0700
tags: node gatsby
---
To make the site more resilient to network connectivity issue, gatsby js provides an awesome plugin that cache pix and js of the site.

It is just two simple steps:

```
$ npm install --save gatsby-plugin-offline
```

Add this to the `gatsby-config.js`:

```
plugins: [`gatsby-plugin-offline`]
```

Source: [gatsbyjs adding offline support to your site](https://mitzen.blogspot.com/2018/12/gatsbyjs-adding-offline-support-to-your.html)
