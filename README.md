# WordPress Cheat Sheet

**Here are some of the most used code snippets for WordPress.**


## Free e-book

You can read about WordPress in my free e-book: [WordPress in the Classroom](http://ipaper.ipapercms.dk/ErhvervsakademiAarhus/Forskningsrapportguides/wordpress-in-the-classroom/?page=1).


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

Often the building blocks are found in three files:

* header.php - whatever is in the head, header and so on
* footer.php - whatever comes after the loop or content has ended
* sidebar.php - asides, menus, widget areas and similar

The content of these partial files are imported like this:

~~~~
<?php get_header(); ?>
<?php get_sidebar(); ?>
<?php get_footer(); ?>
~~~~



## Add a Menu Area

You can add theme menu areas wherever you need them in your design.

### Step I) In functions.php

In function.php find the place where the menus are defined.

~~~~
function register_my_menus() {
  register_nav_menus(
    array(
      'header-menu' => __( 'Header Menu' ),
      'extra-menu' => __( 'Extra Menu' )
    )
  );
}
add_action( 'init', 'register_my_menus' );
~~~~

In a childtheme you just add a menu as you see it above. Do it in the functions.php in the childtheme folder. Not in the parent theme.

### Step II) In the file where the menu should appear

Often menu areas are places in the header, sidebar or footer. But you can place the menu anywhere in your theme files. Just add this code in a relevant spot:

~~~~
<?php wp_nav_menu( array( 'theme_location' => 'extra-menu' ) ); ?>
~~~~

### Step III) Create your menu in the Dashboard

Now the menu area should be visible in your Dashboard. Attach one of your menus to the new area.

## How to link to an Image

The first time you try to set the source to images in your `images/myImage.jpg` folder no image will show up. Here is the reason:


### Wrong: this will not work in a WordPress theme

~~~~
<img src="<?php bloginfo('stylesheet_directory'); ?>/images/yourImage.png">
~~~~

### Correct: here is how to link to images or other files

~~~~
<img src="<?php bloginfo('stylesheet_directory'); ?>/images/yourImage.png">
~~~~

or

~~~~
<img src="<?php echo get_template_directory_uri(); ?>/images/logo.png" width="" height="" alt="" />
~~~~

For more information see [this page](https://developer.wordpress.org/themes/functionality/media/images/) in the Codex.

## Link to CSS or JavaScripts

Add your script or css file along these lines  in *functions.php*:

~~~~
/**
 * Proper way to enqueue scripts and styles
 */
function wpdocs_theme_name_scripts() {
    // below a css file
    wp_enqueue_style( 'style-name', get_stylesheet_uri() );
    // below a script
    wp_enqueue_script( 'script-name', get_template_directory_uri() . '/js/example.js', array(), '1.0.0', true );
}
add_action( 'wp_enqueue_scripts', 'wpdocs_theme_name_scripts' );
~~~~

PS: In a Childtheme add the code to the functions.php in the child theme folder


## Enable jQuery in your theme

Add this line before wp_head() in header.php - or another relevant file:

~~~~
<?php wp_enqueue_script("jquery"); ?>
<?php wp_head(); ?>
~~~~

See [this sample](https://github.com/asathoor/tw17child/blob/master/header.php#L25-L29).


## Run jQuery in the protected mode

In order to avoid a conflict you should run jQuery in protected mode. Do it like this:

~~~~
<script>
/**
 * jQuery in protected mode
 */
( function( $ ) {
	// hello world variant
	$('h1').text('I\'m a poor lonesome cowboy');
	// try: animate.css
	// @url: https://github.com/daneden/animate.css
	$('h1').hover( function(){
		$(this).addClass('animated swing');
	} );
} )( jQuery ); // jquery end
</script>
~~~~

## Create a Costum Frontpage or other pages

Here you have several options.

* In the Dashboard you can select at page and use that page as your front page.
* As an alternative you can create a file from scratch. If you name your file front-page.php WordPress will present whatever is in that page as the frontpage.

Tip: often themes has a page called page.php. Copy the file and save it as front-page.php. Then modify it according to your will.

## A fairly typical page

~~~~
<?php get_header(); ?>

    <div id="text" class="yourClass">
      <?php get_template_part('loop'); // the main loop ?>
  	</div>

<!-- /page.php -->

<?php get_footer(); ?>
~~~~

WordPress use PHP in order to get pages or posts from the database. Save your loop in a separate file *loop.php* - the content of this file is:

~~~~
<?php
/**
 * File: loop.php
 */
if ( have_posts() ) {
	while ( have_posts() ) {
		the_post();
		//
		the_title('<h3 class="title">','</h3>');
		echo '<div class="content">';
			the_content();
		echo '</div>';
		//
	} // end while
} // end if
?>
~~~~

## Create a theme from scratch

Try Underscores _S - https://underscores.me/

* Give your theme a name.
* Download your theme. It's a zip file.
* Install the theme on your server.

[See the introduction to _S in this video](https://www.youtube.com/watch?v=ruSxM4yr8FA).


## Rest API

... coming soon ...
