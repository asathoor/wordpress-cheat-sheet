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

## How to link to an Image

## Link to CSS or JavaScripts

## Enable jQuery on a webpage

## Run jQuery in the protected mode

## Create a Costum Frontpage
