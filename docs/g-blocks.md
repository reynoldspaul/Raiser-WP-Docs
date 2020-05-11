---
id: g-blocks
title: Guntenberg Blocks
sidebar_label: Guntenberg Blocks
---

Guntenberg Blocks can be created inside the /raiser-wp/blocks folder within your theme.

```
$ php raiser make:block "Block Name" --type=gacf
```
> To register the block in the WP editor, it needs to be added to the blocks array inside the config/gutenberg.php file
```
'blocks' => [
    G_Block::class,
],
``` 

## Guntenberg Block Class Structure

Example structure of a Guntenberg Block called "Gallery"

```
class Gallery_Block extends Raiser_ACF_G_Block {

	public $block_name = 'gallery';

	public function init(){

		$this->block_settings = [
			'title'         => 'Gallery',
		];

		$this->gutenberg_block = [
			'name'				=> 'gallery',
			'title'				=> 'Gallery',
			'description'		=> 'A custom gallery block.',
			'render_template'	=> get_template_directory().'/raiser-wp/blocks/gallery/template.php',
			'category'			=> RAISER_THEME,
			'icon'				=> 'admin-comments',
			'keywords'			=> array( 'gallery' ),
			'mode' 				=> 'preview',
		];			

		$this->fields = [
			[
				'label' => 'Photos',
				'name' => 'photos',
				'type' => 'gallery',
				'library' => 'all',
				'insert' => 'append',
			],
		];	

	}
}
```

## Template

Inside your block folder will be a template.php file. Inside this file you have access to the following variables
```
/**
 * Block Template.
 *
 * array $block 			The block settings and attributes.
 * string $content 			The block inner HTML (empty).
 * bool $is_preview 		True during AJAX preview.
 * (int|string) $post_id 	The post ID this block is saved to.
 */

```

You can modify the $block array via a callback inside the block class
```
public function render_callback($block, $content, $is_preview, $post_id){

	// add attributes to block
	$block['new_attribute'] = get_post$post_id);

	return $block;
}	
```

## Block Visibility

You can restrict blocks on certain post types or screens via setting a location array on the block_settings array inside the init() function. The location array needs to take the form of the ACF location settings.

You can also define a custom error message to appear in the block editor.
```
public function init(){

	$this->block_settings = [
		'title'         => 'Hub Horizontal',
		'location'		=> [
			[
				[
					'param' => 'post_template',
					'operator' => '==',
					'value' => 'template-custom.php',
				],
			],
		],
		'location_error_message' => 'Error: This block is only available to PAGES with the CUSTOM template',
	];

	// other variables
}
```