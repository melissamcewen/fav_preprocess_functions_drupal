# fav_preprocess_functions_drupal

## Core
### theme_preprocess_html
#### Adding CSS
For example here we are adding Lato, a Google font
```php
drupal_add_css('http://fonts.googleapis.com/css?family=Lato:400,700,400italic,700italic', array('type' => 'external'));
```
### theme_preprocess_page
#### Adding a search box variable to print the search box (or search boxes)
```php
$search_box = drupal_get_form('search_form');
$vars['search_box'] = drupal_render($search_box);
```
print in page.tpl.php
```
<?php print $search_box?>
```

### theme_preprocess_block
#### Giving block titles a special block title class
```php
$vars['title_attributes_array']['class'][] = 'block-title';
```
#### N-th block in region class
```php
$vars['classes_array'][] = 'region-block-'.$vars['block_id'];
```

