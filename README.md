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
#### Utilizing another module's rendering function to create a variable to print in the template
Example here is the print module
```php
    if (function_exists('print_insert_link')){
        $vars['print_link'] = print_insert_link();
    }
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
### theme_css_alter
#### Remove a module's CSS if it conflicts with theme
for example here we are removing search's css
```php
unset($css[drupal_get_path('module','search').'/search.css']);
```

### theme_form_alter
#### Add class to search form input (classless by default in Drupal 6)
```php
    if ($form_id == 'search_form') {
        $form['basic']['keys']['#attributes']['class'][] = 'search-input-form';
    }
```

## Views
### theme_preprocess_views_view
#### Adding custom js to a particular view that shouldn't be loaded on the rest of the site
```php
    $view = &$vars['view'];

    if($view->name == 'VIEWS_MACHINE_NAME' && $vars['display_id'] == 'page'){
        drupal_add_js(drupal_get_path('theme', 'THEME_NAME') . '/js/isotope.pkgd.min.js');
        drupal_add_js(drupal_get_path('theme', 'THEME_NAME') . '/js/isotope_config.js');
    }

```

