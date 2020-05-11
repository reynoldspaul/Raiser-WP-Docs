---
id: cpt
title: Custom Post Types
sidebar_label: Custom Post Types
---

Custom post types can be registered inside the /raiser-wp/cpts folder within your theme.

```
$ php raiser make:cpt "Custom Post Type Name"

// to create templates use the --templates flag
$ php raiser make:cpt "Custom Post Type Name" --templates
```

This command will create a file called cpt_name.php inside /raiser-wp/cpts folder, and create 2 template files for this custom post type - single-post_type.php and archive-post_type.php

Alternatively, you can create the files yourself.

## CPT Class Structure

Example structure for a Custom Post Type called "Product"
```
class Product_CPT extends Raiser_CPT_Base {

    public $post_type_name = 'product';

    public function post_type_setup(){

        $this->labels = [
            'name'                  => 'Product',
        ];

        $this->rewrite = [
            'slug'                  => 'product',
        ];

        $this->args = [
            'label'                 => 'product',
            'description'           => 'A product',
            'supports'              => array( 'title', 'editor', 'thumbnail' ),
            //'show_in_rest' 			=> true, // enable for gutenberg editor	
        ];       

    }   
}
new Product_CPT;
```

## Attach Blocks

Blocks can be added to the cpt using the $blocks variable inside the class
```
// attach meta boxes
public $blocks = [
	'your_block_key_1' => Custom_Block::class
];
```

## Eager Load Data

Block data, and taxonomy data, can be eager-loaded into the $post object inside your WordPress template files via the $with variable:
```
// eager load
public $with = [
	'terms' => ['your_tax_id'],
	'blocks' => ['your_block_key_1','your_block_key_2'],
];
```
Inside your template files, you can access this data via the post object
```
// access block data
echo $post->your_block_key_1;

// access term data
echo $post->your_tax_id_term_ids;
```
> Note, if you are doing a custom query via WP_Query, be ensure to set the suppress_filters argument to false in order to eager load data into the query result.

## Admin Options Block

For your Custom Post Type, you can define an admin options block via the $admin_block variable. This block will appear in the WordPress admin menu inside your CPT options
```
// admin option block
public $admin_block = Option_Block::class;
```

## Archive Query Filter
You can modify the standard WordPress query on the archive page template by adding the following method inside the CPT class
```
public function query_on_archive_page($query){
	// modify the query
	$query->posts_per_page = 20;
	return $query;
}
```

## Getters
To modify an existing $post attribute, you can use the following method inside your CPT class
```
public function get_YOURATTRIBUTE_attribute($value){
	return strtoupper($value);
}

// for example, to uppercase a name field inside a client block, create the following function
public function get_client_name_attribute($value){
	return strtoupper($value);
}
```

## Appends
To append new values to the $post object, use the appends array and create an append function
```
public $appends = ['new_field'];

// create an append function to set the value
public function get_new_field_attribute($post){
	if( $post->ID == 2 ){
		return 'I am the second post';
	}
	return 'I am a post';
}

```
The inside your template, you will have access to this new field
```
echo $post->new_field;
```