# Pico Pages List Resume

A nested pages list with resume plugin for the stupidly simple & blazing fast, flat file CMS [Pico](http://pico.dev7studios.com).
This plugin is derivated from [Pico Page List Plugin](https://github.com/nliautaud/pico-pages-list)

## Installation

Copy `pico_pages_listresume.php` to the `plugins` directory of your Pico Project.

## Usage

Add a generated nested pages list in your *theme* by using the following Twig variable :

	{{ pages_listresume }}

You'll automatically get something like :

* [A cool page]()
  A small resume of the page 
* [Sub-page is coming]()
    A small resume of the page 
	* [The choosen one]()
	  A small resume of the page 
	* category
		* [A page]()
		  A small resume of the page 
* [untitled]()
  A small resume of the page 

Under the hood :

```html
<ul>
	<li class="titled">
		<a href="http://mysite.com/titled">A cool page</a>
	</li>
	<li class="foo-page is-parent">
		<a href="http://mysite.com/foo-page">Sub-page is coming</a>
		<small>A small resume of the page</small>
		<ul>
			<li class="child is-current">
				<a href="http://mysite.com/foo-page/child">The choosen one</a>
				<small>A small resume of the page</small>
			</li>
			<li class="category">
				category
				<small>A small resume of the page</small>
				<ul>
					<li class="bar">
						<a href="http://mysite.com/category/bar">A page</a>
						<small>A small resume of the page</small>
					</li>
				</ul>
			</li>
		</ul>
	</li>
	<li class="untitled">
		<a href="http://mysite.com/untitled">untitled</a>
		<small>A small resume of the page</small>
	</li>
</ul>
```

## Features

The plugin generate a clean nested html list, using links only if the page exists. The page title is used if possible.

The lists items are defined by css classes allowing per-page or general manipulations :

```css
#nav .foo-page a {
	/* access to a specific page link */
}
#nav .foo-page .child a {
	/* access to a specific foo-page/child link */
}
#nav .is-current {
	/* access to the current page item */
}
#nav .is-parent {
	/* access to every parent item of the current one */
}
```

To exclude pages from the generated list, add to Pico config the setting `hide_pages`, and separate paths with commas. Childs of a path will be excluded with their parent :

```php
$config['listresume_hide_pages'] = 'this/page,all/in/here/';
```

To not generate link for folder :

```php
$config['listresume_create_folder_link] = false;
```