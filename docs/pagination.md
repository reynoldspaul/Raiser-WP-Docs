---
id: pagination
title: Pagination
sidebar_label: Pagination
---

Raiser WP Premium offers AJAX based pagination functionality.

To use, first add the Raiser_Load_More_Trait to your custom post type.

You can also define a template file for the post card.

```
class Projects_CPT extends Raiser_CPT_Base {

	use Raiser_Load_More_Trait;

	public $load_more_card_template = 'parts/card-post';

}
```

## Pagination Display

Inside your template, add the below function to render the pagination section
```
<div class="raiser-pagination">
	<?php Raiser_Load_More::pagination($pagination_args);?>
</div>

// optional args
$pagination_args = [
	'left-arrow' 				=> file_get_contents(locate_template('svg/inline-chevron-left.svg.php')),
	'right-arrow'				=> file_get_contents(locate_template('svg/inline-chevron-right.svg.php')),
	'wp_query'					=> $wp_query,
	'queried_object'			=> 'block_posts',
	'template_slug'			 	=> 'parts/card',
	'template_name'				=> $post_type,
	'template_callback'			=> 'callback_to_your_template_render_function'	
];
```

### Pagination Results

The AJAX results will replace a div with class 'raiser-posts'

## Example

Here is a full example of the ajax pagination on an archive page

```
<section id="main" role="main">

    <div class="container">

		<div class="row">
			<div class="raiser-posts">
				<?php if ( have_posts() ) : while ( have_posts() ) : the_post(); ?>
					<?php get_template_part( 'parts/card', 'post' ); ?>
				<?php endwhile; endif; ?>
			</div>
		</div>

		<div class="row">
			<div class="raiser-pagination">
				<?php Raiser_Load_More::pagination($pagination_args);?>
			</div>
		</div>

    </div>

</section>
```