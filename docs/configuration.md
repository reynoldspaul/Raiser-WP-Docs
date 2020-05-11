---
id: configuration
title: Configuration
sidebar_label: Configuration
---

Raiser WP uses array based configuration files, located within your-theme-folder/config. No more large sections of script just to define some basic aspects to your theme.

Init the config files within your theme by running the following command from inside the Raiser-WP plugin directory.

```
$ php raiser init:config
```

## Config Helper

You can access config values within your theme code via the following helper function
```
// access the dashboard setting within the admin.php config file
rw_config('admin.dashboard');
```

## Custom Config Files

> You can set up a new config file inside the /config folder. You can access values via the helper function
```
rw_config('your_file_name.config_key');
```

## admin.php Settings

Config Key | Value | Details
------------ | ----------- | -----------------
show_admin_bar | true/false | Show/hide the WordPress admin bar on the front end
dashboard.show_welcome_panel | true/false | Show/hide the welcome panel in the dashboard
dashboard.show_meta_boxes | Array eg:<br>dashboard_plugins<br>dashboard_recent_comments<br>dashboard_site_health<br>dashboard_activity | Set which dashboard meta boxes to show - use the metabox id
gutenberg_editor | true/false | Use the Gutenberg editor in posts
theme_support | Array eg:<br>menus<br>post-thumbnails | Set theme support - [WP docs](https://developer.wordpress.org/reference/functions/add_theme_support/)

## theme.php Settings

Config Key | Value | Details
------------ | ----------- | -----------------
theme_name | String | Define your theme name
wp_head | Array of true/false<br>remove_wp_emoji<br>remove_rest_api_header<br>remove_weblog_link<br>remove_wp_generator<br> | Clean up the html header - Remove code that you probably don't need
permalink_structure | String | Permalink Structure - [WP docs](https://wordpress.org/support/article/settings-permalinks-screen/)
stylesheets | Array | Include stylesheets - [WP docs](https://developer.wordpress.org/reference/functions/wp_enqueue_style/)
scripts | Array | Include scripts - [WP docs](https://developer.wordpress.org/reference/functions/wp_enqueue_script/).<br>Use '[name]-async-defer' to async and defer the script<br>Set 'localize' to localize js vars
menus | Array | Register Theme Menus
custom_login_image | Array<br>src<br>background-color<br>size | Login Screen Custom Logo
editor_custom_colors | Array | Custom Editor Colours
image_sizes | Array | WordPress Custom Image Sizes
widgets | Array | Register Widget Areas - [Wp docs](https://developer.wordpress.org/reference/functions/register_sidebar/)

## gutenberg.php Settings

Config Key | Value | Details
------------ | ----------- | -----------------
theme_support | Array<br>align-wide | Add theme support for Gutenberg
editor_styles | String | Enqueue a stylesheet for admin
block_categories | Array | Set custom block categories
blocks | Array eg:<br>Block_name::class | Register your custom Gutenberg blocks
