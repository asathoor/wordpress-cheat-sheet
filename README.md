# WordPress Cheat Sheet

**Here are some of the mose usefull code snippets for WordPress.**

## Where are the Theme Files?

* Themes: ../wp_content/themes/yourThemeName
* Plugins: ../wp_content/plugins/yourPluginName

## The Loop

The loop will getx the content from the WordPress database to a webpage. Here is a relatively simple loop.
Here is a very simple loop from https://developer.wordpress.org/themes/basics/the-loop/

~~~~
<?php
if ( have_posts() ) :
    while ( have_posts() ) : the_post();
        the_title( '<h2>', '</h2>' );
        the_post_thumbnail();
        the_excerpt();
    endwhile;
else:
    _e( 'Sorry, no posts matched your criteria.', 'textdomain' );
endif;
?>
~~~~

## Import the Header, Footer and Sidebar

~~~~
<?php get_header(); ?>
<?php get_sidebar(); ?>
<?php get_footer(); ?>
~~~~

## Add a Menu Area

You can add menu areas wherever you need them in your design.

### Step I) In functions.php

### Step II) In the file where the menu should appear

### Step III) Create your menu in the Dashboard

## How to link to an Image

### A) In a Theme

~~~~
<img src="<?php bloginfo('stylesheet_directory'); ?>/images/yourImage.png">
~~~~

### B) In a Childtheme

~~~~
<img src="<?php echo get_template_directory_uri(); ?>/images/yourImage.png" />
~~~~

## Link to CSS or JavaScripts

## Enable jQuery on a webpage

## Run jQuery in the protected mode

## Create a Costum Frontpage or other pages

## Create a theme from scratch

Try Underscores _S - https://underscores.me/

## Rest API
