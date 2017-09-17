# Traversing the Template Hierarchy in Designland

Today I'll be speaking about WordPress' template hierarchy and how to leverage it for our designs and how to make our builds modular, using the built in template structure.

Let's start with discussing some basics.

* What do I mean when, I use the word "Template"?
	- **A Template** in WordPress is a PHP theme file that determines how content is displayed.
* How can we leaverage templates?
	- First you'll need to understand the **The Template Hierarchy**
* What is the **The Template Hierarchy**?
	- **The Template Hierarchy** is a list of possible files that can be used in a theme and their relationship to each other.
	- There are two useful locations to get more information on **The Template Heirarchy**
		- 🔗 [WPHierarchy.com Site](https://wphierarchy.com/)
		- 🔗 [Template Hierarchy Documentation](https://developer.wordpress.org/themes/basics/template-hierarchy/)
	- Some Examples of Templates are the following
		- `page.php` - Controls how single pages are displayed
		- `single.php` - Controls how single blog posts are displayed
		- `category.php` - Controls category archive pages
		- `tag.php` - Controls tag archive pages

Learning the what template file to use is a very important skill as a WordPress Designer/Developer. This skill will truely empower you to create custom layouts without the "need" for theme builders!

![Everyone rejoice](https://media.giphy.com/media/DKnMqdm9i980E/giphy.gif)

---

Ok, now since we've covered some basics on this let's talk about how this can help you as a designer!

Templates can really help create modularity in your theme.

A great example is if you would want to make a two different pages. One with a sidebar and one without, I know that's crazy right?

Using **The Template Hierarchy** you can create a seperate template for both. We could name them `full-width.php` and `right-sidebar.php`. You can actually name them however you like, but I would suggest being specific about the functionality of what the page is supposed to be used for.

With in these templates we can break them done in a modular fashion. But before we would do that we need to set the internal references for WordPress to recognize these templates.

Let's open `full-page.php`. A default full page template for a starter theme that I sometimes use, it looks like this.

```
<?php
/*
Template Name: Full Width (No Sidebar)
*/
?>

<?php get_header(); ?>

	<div id="content">

		<div id="inner-content" class="row">

		    <main id="main" class="large-12 medium-12 columns" role="main">

				<?php if (have_posts()) : while (have_posts()) : the_post(); ?>

					<!-- Here is our loop -->
					<?php get_template_part( 'parts/loop', 'page' ); ?>

				<?php endwhile; endif; ?>

			</main> <!-- end #main -->

		</div> <!-- end #inner-content -->

	</div> <!-- end #content -->

<?php get_footer(); ?>
```

As we can see we'll need to specify a **Template Name:**, this template name can be whatever your ❤️ desires. Though again like before when naming the file, I suggest you be somewhat specific to the use of the template.

Okay, okay I know you really want to learn how does this help us create our designs into custom page templates. Well since we have this set up we can also set up a template for a side bar.

![Okay, okay](https://media.giphy.com/media/10pR6dUXHBpZSg/giphy.gif)

So we can do one of two things.
* We can build a sidebar template and use the built in WordPress widget area.
	- In going this direction we'll need to write an if statement.

**OR**
* We can use our `right-sidebar.php` template.

I'm going to show you with our current template. Let's look at what this template should look like.

```
<?php
/*
Template Name: Right Sidebar
*/
?>

<?php get_header(); ?>

	<div id="content">

		<div id="inner-content" class="row">

		    <main id="main" class="large-8 medium-8 columns" role="main">

				<?php if (have_posts()) : while (have_posts()) : the_post(); ?>

					<!-- Here is our loop -->
			    	<?php get_template_part( 'parts/loop', 'page' ); ?>

			    <?php endwhile; endif; ?>

			</main> <!-- end #main -->

			<!-- This is our sidebar, but where's the html??? -->
			<?php get_template_part( 'parts/sidebar.php' ); ?>

		</div> <!-- end #inner-content -->

	</div> <!-- end #content -->

<?php get_footer(); ?>
```

This is our sidebar call `<?php get_template_part( 'parts/sidebar.php' ); ?>`.

![Say What?](https://media.giphy.com/media/xTkcEId8z20sPCMlK8/giphy.gif)

**Wait!** This doesn't look like a full sidebar though does it? That's because we're making a call to another template piece. This is where we can break items down into modular pieces, this is especially useful when creating pieces that are reusable.
