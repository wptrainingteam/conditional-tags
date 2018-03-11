# Conditional Tags

## Description

In this lesson you will learn how conditional tags allow you to display unique content on a page depending on the conditions the page matches. This means you can have a block of content that only shows up on the home page and not on other pages. In this lesson you'll learn how to harness the power of conditional tags and use them in your theme templates.

## Objectives

After completing this lesson, you will be able to:

*   Explain Conditional Tags.
*   Summarize the purpose of Conditional Tags and what happens when they are used.

## Prerequisite Skills

You will be better equipped to work through this lesson if you have experience in and familiarity with:

*   Basic knowledge of PHP and HTML
*   Basic knowledge of [installing and activating WordPress themes](https://make.wordpress.org/training/handbook/user-lessons/choosing-and-installing-a-theme/)
*   Understanding of the [Template Hierarchy](https://make.wordpress.org/training/handbook/theme-school/template-hierarchy/)
*   Ability to edit files with a text editor

## Assets

*   [Twenty Fourteen Theme](https://wordpress.org/themes/twentyfourteen "Twenty Fourteen Theme Download")
*   [Child Theme of Twenty Fourteen](http://codex.wordpress.org/Child_Themes "Instructions for Creating a Child Theme")

## Screening Questions

*   Do you have at least a basic knowledge of HTML/CSS?
*   Do you have at least a basic knowledge of PHP structure?
*   Do you have a basic understanding of the file structure of a WordPress theme?
*   Will you have a locally or remotely hosted sandbox WordPress site to use during class?

## Teacher Notes

*   **Time Estimate:** 45 minutes
*   Performing a live demo while teaching the steps to create a conditional statement is crucial to having the students understand how powerful these statements are and show what they can accomplish.
*   Students can perform these tasks on either a local or remote installation of WordPress. It would be best if students can already have their sites set up and ready to customize. If there are a few students that do not, you might consider setting some time aside before class to assist students with the WordPress installation process. For more information on how to install WordPress locally or remotely, please visit our Teacher Resources page.
*   The preferred answers to the screening questions is “yes.” Participants who reply “no” to all 4 questions may not be ready for this lesson.

## Hands-on Walkthrough

### Introduction: What Are Conditional Tags

Welcome to Conditional Tags! Today, you are going to learn what Conditional Tags are and how they can be best used to enhance your WordPress theme. Conditional tags allow theme designers to pose a question and if that question evaluates to either TRUE or FALSE, something will happen. These tags can be used to generate new content on a specific post, page, category, and taxonomy template. If the question you pose evaluates to TRUE, then the content you want to display will appear. If it evaluates to FALSE, nothing will appear in that area. Here are a few examples: `is_single()` When any single Post, attachment or custom Post Type page is being displayed. This will evaluate to FALSE for Pages. `is_single( '17' )` When Post 17 is being displayed as a single Post. `is_single( 'Irish Stew' )` When the Post with Title "Irish Stew" is being displayed as a single Post. A complete list of conditional tags available for use can be viewed at http://codex.wordpress.org/Conditional_Tags Some conditional tags function in parallel to a corresponding theme template file, for example, the error page template. The template file 404.php could be used, or invoking the conditional tag `is_404()`.

* * *

### The Purpose Of Conditional Tags

In WordPress, specific template files control how your website displays content. For example, page.php controls what every single 'page' on your website looks like. This saves time in developing by not having to code every single page on a website; however, if you want something different to happen on a few specific pages, you would need to use Conditional Tags to accomplish this. Examples:

*   display a specific block of text above displayed posts, but only on the home page
*   display a block of text on a post that has a specific category
*   display a block of text on a post that has one of several specific categories
*   display a content section on all posts except ones tagged with a specific tag

### Conditional Tags In Action

Say that you are building a cooking website that shows healthy recipes for families. Each post would display a new recipe. These posts could also be categorized into ingredients such as Ground Beef, Cheddar Cheese, Milk, etc. For today's example you are going to display a simple block of text at the top of any single recipe post if it happens to be in the category of “Blue Cheese”. Note: Adding or changing template files should always be done within a child theme! (See [Child Theme Lesson Plan](https://make.wordpress.org/training/handbook/theme-school/child-themes/ "Child Themes Lesson"))

#### Step 1: Determine the appropriate template file for using the conditional tag.

You are looking to insert text on blog posts only, so you need to look for the `single.php` template file.

#### Step 2: Determine where in the template file you want the text block to appear when the conditional tag is evaluated.

You want to insert text above the blog post, so open the `single.php` file: [html] <?php /**

*   The Template for displaying all single posts

*   @package WordPress
*   @subpackage Twenty_Fourteen
*   @since Twenty Fourteen 1.0

*/ get_header(); ?> <div id="primary" class="content-area"> <div id="content" class="site-content" role="main"> <?php // Start the Loop. while ( have_posts() ) : the_post(); [/html] You should insert the conditional test after the opening #content div, but before the `while (have posts() ) : the_post()` statement.

#### Step 3: Insert the Conditional Tag in the appropriate area you have chosen.

[html] // use conditional tag to check if post has category with slug ‘blue-cheese’ is_category( ‘blue-cheese’) { // display text when viewing posts in the category of Blue Cheese echo "<p>This is my about my favorite cheese!</p>"; } [/html] the `single.php` file should now appear like this: [html] <?php /**

*   The Template for displaying all single posts

*   @package WordPress
*   @subpackage Twenty_Fourteen
*   @since Twenty Fourteen 1.0

*/ get_header(); ?> <div id="primary" class="content-area"> <div id="content" class="site-content" role="main"> <?php // use conditional tag to check if post has category with slug ‘blue-cheese’ is_category( ‘blue-cheese’) { // display text when viewing posts about Blue Cheese echo "This is my about my favorite cheese!"; } // Start the Loop. while ( have_posts() ) : the_post(); [/html] When you view a post, and that post is in the category of “Blue Cheese”, the additional content appears at the very start of the #content div.

* * *

### A Deeper Look Into Conditional Tags

You can expand the power of Conditional Tags by using a simple PHP IF statement to display one set of content if the statement evaluates to TRUE and different content if it evaluates to FALSE. Let's say on your website you have a header image added to the Twenty Fourteen theme, which shows up on every page of the website. You want the header image to only show up on the front page of your website and not on any other page. To accomplish this you will need to use the Conditional Tag `is_front_page()`.

#### Step 1: Determine the appropriate template file for using the conditional tag.

Since you are changing the structure of the header on your site, you are going to look for the `header.php` template file.

#### Step 2: Determine where in the template file you need to place the conditional tag for evaluation.

You want to evaluate your condition around the div that holds the header image, so open the `header.php` file: [html] <?php /**

*   The Header for our theme

*   Displays all of the <head> section and everything up till <div id="main">

*   @package WordPress
*   @subpackage Twenty_Fourteen
*   @since Twenty Fourteen 1.0

*/ ?><!DOCTYPE html> <!--[if IE 7]> <html class="ie ie7" <?php language_attributes(); ?>> <![endif]--> <!--[if IE 8]> <html class="ie ie8" <?php language_attributes(); ?>> <![endif]--> <!--[if !(IE 7) & !(IE 8)]><!--> <html <?php language_attributes(); ?>> <!--<![endif]--> <head> <meta charset="<?php bloginfo( 'charset' ); ?>"> <meta name="viewport" content="width=device-width"> <title><?php wp_title( '|', true, 'right' ); ?></title> <link rel="profile" href="http://gmpg.org/xfn/11"> <link rel="pingback" href="<?php bloginfo( 'pingback_url' ); ?>"> <!--[if lt IE 9]> <script src="<?php echo get_template_directory_uri(); ?>/js/html5.js"></script> <![endif]--> <?php wp_head(); ?> </head> <body <?php body_class(); ?>> <div id="page" class="hfeed site"> <?php if ( get_header_image() ) : ?> <div id="site-header"> <a href="<?php echo esc_url( home_url( '/' ) ); ?>" rel="home"> <img src="<?php header_image(); ?>" width="<?php echo get_custom_header()->width; ?>" height="<?php echo get_custom_header()->height; ?>" alt=""> </a> </div> <?php endif; ?> <header id="masthead" class="site-header" role="banner"> <div class="header-main"> <h1 class="site-title"><a href="<?php echo esc_url( home_url( '/' ) ); ?>" rel="home"><?php bloginfo( 'name' ); ?></a></h1> <div class="search-toggle"> <a href="#search-container" class="screen-reader-text"><?php _e( 'Search', 'twentyfourteen' ); ?></a> </div> <nav id="primary-navigation" class="site-navigation primary-navigation" role="navigation"> <button class="menu-toggle"><?php _e( 'Primary Menu', 'twentyfourteen' ); ?></button> <a class="screen-reader-text skip-link" href="#content"><?php _e( 'Skip to content', 'twentyfourteen' ); ?></a> <?php wp_nav_menu( array( 'theme_location' => 'primary', 'menu_class' => 'nav-menu' ) ); ?> </nav> </div> <div id="search-container" class="search-box-wrapper hide"> <div class="search-box"> <?php get_search_form(); ?> </div> </div> </header><!-- #masthead --> <div id="main" class="site-main"> [/html] You want the header image to only appear on the front page of your website, so you will need to place the conditional statement under the div with the ID of "page" and the class of "hfeed" and "site" in the `header.php` template file.

#### Step 3: Insert the Conditional Tag in the appropriate area you have chosen.

[html] // use an IF statement with the conditional tag to check if this is the front page <?php if ( is_front_page() ) : ?> // place the conditional statement for the header image and the html structure of the header image here <?php if ( get_header_image() ) : ?> <div id="site-header"> <a href="<?php echo esc_url( home_url( '/' ) ); ?>" rel="home"> <img src="<?php header_image(); ?>" width="<?php echo get_custom_header()->width; ?>" height="<?php echo get_custom_header()->height; ?>" alt=""> </a> </div> <?php endif; ?> <?php endif; ?> [/html] The `header.php` file should now appear like this: [html] <?php /**

*   The Header for our theme

*   Displays all of the <head> section and everything up till <div id="main">

*   @package WordPress
*   @subpackage Twenty_Fourteen
*   @since Twenty Fourteen 1.0

*/ ?><!DOCTYPE html> <!--[if IE 7]> <html class="ie ie7" <?php language_attributes(); ?>> <![endif]--> <!--[if IE 8]> <html class="ie ie8" <?php language_attributes(); ?>> <![endif]--> <!--[if !(IE 7) & !(IE 8)]><!--> <html <?php language_attributes(); ?>> <!--<![endif]--> <head> <meta charset="<?php bloginfo( 'charset' ); ?>"> <meta name="viewport" content="width=device-width"> <title><?php wp_title( '|', true, 'right' ); ?></title> <link rel="profile" href="http://gmpg.org/xfn/11"> <link rel="pingback" href="<?php bloginfo( 'pingback_url' ); ?>"> <!--[if lt IE 9]> <script src="<?php echo get_template_directory_uri(); ?>/js/html5.js"></script> <![endif]--> <?php wp_head(); ?> </head> <body <?php body_class(); ?>> <div id="page" class="hfeed site"> // use an IF statement with the conditional tag to check if this is the front page <?php if ( is_front_page() ) : ?> // place the conditional statement for the header image and the html structure of the header image here <?php if ( get_header_image() ) : ?> <div id="site-header"> <a href="<?php echo esc_url( home_url( '/' ) ); ?>" rel="home"> <img src="<?php header_image(); ?>" width="<?php echo get_custom_header()->width; ?>" height="<?php echo get_custom_header()->height; ?>" alt=""> </a> </div> <?php endif; ?> <?php endif; ?> [/html] Now when you are on the front page of your website it will have the header image above the navigation but if you go to any other page on your site it will disappear.

* * *

### Summary

Conditional tags are a simple way to check for specific conditions, as a true or false test. Using just a few lines, you can check to see if one or more conditions match, and execute additional functions. These can be mixed and matched and used in all template files to achieve the end result desired. Conditions vary from the id or tag of a post or page to the type of content being viewed.

## Group Exercises

**Modify the single post template theme file to display a block of text after the post content but before the comments if the post has ID of 2.**

*   What is the Conditional Tag you will need to use to accomplish this? If you don't know, where can you find a list of Conditional Tags?
*   How do you tell the Conditional Tag to only display the block of text if the post has an ID of 2?

**Display a block of text if a Post has a tag of "Breakfast" attached to it.**

*   Will you use "is" or "has" in your Conditional Tag for this exercise?
*   Which template file will you need to edit to accomplish this task?

**Add a block of content to the footer and use Conditional Tags to make it display only on the front page of your site.**

*   What template file should you look for to add a block of content to your footer?
*   What Conditional Tag should be used in this instance?

## Quiz

**Which of the following examples would not be accomplished using Conditional Tags?**

1.  Display a block of text on three pages with the ID of 4, 17, and 22
2.  Display a different sidebar on the front page than on inner pages
3.  Display your posts on the front page of your site
4.  Display a different title on the "Ground Beef" category archive page

**Answer:** 3\. Display your posts on the front page of your site

* * *

**What do Conditional Tags evaluate to?**

1.  YES / NO
2.  TRUE / FALSE
3.  MET / NOT MET
4.  TRUE / NULL

**Answer:** 2\. TRUE / FALSE

* * *

**What variable(s) can you pass into the `is_single()` Conditional Tag?**

1.  The Post ID `is_single( '22' )`
2.  The Post Title `is_single( 'Fudge Brownies' )`
3.  The Post Slug `is_single( 'fudge-brownies' )`
4.  The Post Array `is_single( array( 22, 'fudge-brownies', 'Fudge Brownies' )`
5.  All of the above

**Answer:** 5\. All of the above

* * *

**What PHP statement can be used with some Conditional Tags?**

1.  Yes statement
2.  True statement
3.  Then statement
4.  If statement

**Answer:** 4\. If statement

## Additional Resources

[Conditional Tags](https://codex.wordpress.org/Conditional_Tags) @ Codex
