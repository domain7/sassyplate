# SASS/Compass Boilerplate

For documentation and more information on SASS and Compass, refer to the official documentation:

* SASS: http://sass-lang.com
* Compass: http://compass-style.org

## screen.scss

This file is your main compiled stylesheet, and screen.css should be included by your document.

This file acts as an asset manager and loads the following:

* Compass files
* Libraries
* Variables (fonts, colours, etc)
* Mixins (reusable styles)
* Modules (larger, self-contained, reusable units)
* Partials (parts of styling broken off for maintainability)
* A top-down stylesheet

Note that files are included in order of necessity. For example, Compass CSS stuff can be used in
variables which can be used in mixins, modules, site styles, etc.
	
What about media queries?
Note that since SASS allows you to nest @media declarations, separate stylesheets containing
media queries are unnecessary. Nesting @media declarations also reinforces a modular approach.

## Libraries, variables, and mixins 

An example of a SASS library is http://github.com/nathanshubert/Unicode-Shapes-Preprocessor-Library.
They should be prefixed with an underscore, stored in the includes directory,
and are included like such:
	
	@import "includes/library-name";

## Modules 
Self contained pieces of styling that can be reused.
Modules should have the following characteristics:

* Be context independent so they can be used anywhere.
* Defined within a mixin so that they can be used easily, anywhere.
* Be applied to a class that describes what the element IS, not what it looks like.
* Contain their own variations, fallbacks, and possibly media queries

Buttons are a good example of a module.

Module files should be prefixed with an underscore, stored in the modules directory, 
and included like such:

	@import "modules/module-name";

## _style.scss

A traditional-style top-down stylesheet.

## ie.scss

A separate IE stylesheet is reduced in importance by SASS allowing nested selectors
like the following:

	.lt-ie8 & {
		
	}
	
More extensive IE compatibility styling can go in here.
