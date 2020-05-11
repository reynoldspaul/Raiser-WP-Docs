---
id: tax
title: Custom Taxonomies
sidebar_label: Custom Taxonomies
---

Custom Taxonomies are registered inside the /raiser-wp/tax folder within your theme.
```
$ php raiser make:tax "Tax Name"
```

## Taxonomy Class Structure

Example structure for a Taxonomy called "Project Type"
```
class Project_Type_Tax extends Raiser_Taxonomy_Base {

	public $tax_name = 'project-type';

	public function tax_setup(){

		$this->labels = [
			'name' => 'Project Type',
		];

		$this->rewrite = false;

		$this->args = [
			'hierarchical' => true,
		];			
	}


}
new Project_Type_Tax();
```

## Attach To Object

Attach the custom taxonomy to objects within your Theme by adding to the $object_types variable inside the class.
```
// attach to posts or other objects
public $object_types = ['post','projects'];
```

## Attach Blocks

Blocks can be added to the taxonomy using the $blocks variable inside the class
```
// attach meta boxes
public $blocks = [
	'your_block_key_1' => Custom_Block::class
];
```

## Eager Load Data

Block data can be eager-loaded into the $term object inside your WordPress template files via the $with variable:
```
// eager load
public $with = [
	'blocks' => ['your_block_key_1'],
];
```
Inside your template files, you can access this data via the post object
```
$term->your_block_key_1;
```