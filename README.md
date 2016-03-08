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
### Slice up a menu's links for theming individually
```php
 //print the footer links individually for theming
  $menu = menu_navigation_links('menu-footer-menu');
  $menu_links = array();
  for ($i =0; $i <= 3; $i++) {
    $menu_link = array_slice($menu, $i, 1);
    $menu_links[]= theme('links__menu_menu-footer-menu', array('links' => $menu_link));
  }
  $vars['footer_menu_links'] = $menu_links;
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

### theme_menu_tree
### Add search box into menu
```php
  $search_box = drupal_render(drupal_get_form('search_form'));

  return '<ul class="menu">' . $variables['tree'] .  $search_box . '</ul>';
```
### theme_menu_link
#### Add special class to expanded items
```php
if (in_array('expanded', $element['#attributes']['class'])) {
 $wrapper_start = '<span class="menu_drop_down">';
 $wrapper_end = '</span>';
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

