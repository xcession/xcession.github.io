---
layout: article
title:  "Bootstrap: Fixed-top Issue with Wordpress's Admin Bar"
date:   2018-07-05 15:41:33 +0700
tags: bootstrap wordpress webdev
---

# Adding an empty space if Admin bar is displayed

Using the Wordpress function to query if the toolbar is displayed, and then create an empty div below the `navbar div`:

```
<div class="navbar navbar-inverse navbar-fixed-top">
<?php 
  // Fix menu overlap
  if ( is_admin_bar_showing() ) echo '<div style="min-height: 32px;"></div>'; 
?>
<div class="navbar-inner">
```

Source: [WordPress Admin Bar Overlapping Twitter Bootstrap Navigation](https://wordpress.stackexchange.com/questions/87717/wordpress-admin-bar-overlapping-twitter-bootstrap-navigation)
