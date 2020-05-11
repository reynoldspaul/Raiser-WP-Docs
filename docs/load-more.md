---
id: load-more
title: Load More
sidebar_label: Load More
---

Raiser WP Premium offers AJAX based 'load more' functionality.

To use, first add the Raiser_Load_More_Trait to your custom post type.

You can also define a template file for the post card.

```
class Projects_CPT extends Raiser_CPT_Base {

	use Raiser_Load_More_Trait;

	public $load_more_card_template = 'parts/card-post';

}
```

## Load More Button

Inside your template, add the below function to render the load more button

```
// optional arguments
$args = [
	'class'				=> 'wrapper-class',
	'button_text' 		=> '<span>Load More</span>',
	'wp_query'			=> $wp_query,
	'queried_object'	=> 'projects',
	'template_slug'		=> 'parts/post',
	'template_name'		=> 'gallery',
	'template_callback'	=> 'callback_to_your_template_render_function'
];

Raiser_Load_More::load_more_button( $args );
```

### Load More Results

To render the AJAX results of a load more button click, place the following div inside your page template

```
<div id="raiser-load-more-results"></div>
```

### Load More Spinner

To show a spinner during the AJAX request, add the class 'raiser-load-more-spinner' to your spinner

```
// spinner example
<i class="fa fa-spinner fa-spin raiser-load-more-spinner"></i>
```

## Example

Here is a full example of a load more button on an archive page
```
<section id="main" role="main">

    <div class="container">

		<div class="row">

			<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
				<?php get_template_part( 'parts/card', 'post' ); ?>
			<?php endwhile; endif; ?>

			<div id="raiser-load-more-results"></div>

		</div>

		<div class="row">
			<div class="col-12">
				<i class="fa fa-spinner fa-spin raiser-load-more-spinner"></i>
			</div>
		</div>

		<div class="row">
			<div class="col-12 ">
				<?php Raiser_Load_More::load_more_button([
					'button_text' => '<span>See More</span>',
				]); ?>
			</div>
		</div>

    </div>

</section>
```