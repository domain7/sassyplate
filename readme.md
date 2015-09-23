# SASS/Compass Boilerplate

For documentation and more information on SASS and Compass, refer to the official documentation:

* SASS: [http://sass-lang.com](http://sass-lang.com)
* Compass: [http://compass-style.org](http://compass-style.org)

## Setup

Clone this repo into your project to be, or elsewhere and bring all the files in. Since this is a boilerplate and not an updatable framework you'll want to remove the `.git` directory. You'll likely want to remove `.gitignore` and use your project's `.gitignore` as this one excludes compiled css files.

The minimal `.editorconfig` file is in place for the development of the boilerplate and you may prefer a more specific one from your project too.

## Location of directory to watch

The watched directory should be the theme directory, with your stylesheet directory being a child of that.

## File structure

### screen.scss

This file is your main compiled stylesheet, and screen.css should be included by your document.

This file acts as an asset manager and loads the following:

* Compass files
* Libraries
* Variables (fonts, colours, etc)
* Mixins (reusable styles)
* Modules (larger, self-contained, reusable units)
* Partials (parts of styling broken off for maintainability)
* A top-down stylesheet

Note that files are included in order of necessity. For example, Compass CSS stuff can be used in variables which can be used in mixins, modules, site styles, etc.

#### What about media queries?
Note that since SASS allows you to nest @media declarations, separate stylesheets containing media queries are unnecessary. Nesting @media declarations also reinforces a modular approach.

### Libraries, variables, and mixins
An example of a SASS library is http://github.com/nathanshubert/Unicode-Shapes-Preprocessor-Library.
They should be prefixed with an underscore, stored in the includes directory,
and are included like such:

	@import "includes/library-name";

### Variables/maps
Common values should be stored in variables/maps. To enable looping and level 2 ninja moves, many common variables have been moved to maps with accompanying functions. The previous variable names are still available for now for compatibility.

For example, `$color-base` is now accessible using `color(base)`. For more background, read https://viget.com/extend/sass-with-maps

#### Map getter functions
* `color()`
* `font()`
* `weight()`
* `breakpoint()`


### Font Awesome
Font Awesome is included in the boilerplate by default. The font and icon variables are in `includes/fontawesome`, with the font files being located at `fonts/fontawesome`. When included variables are created for every icon, named matching the Font Awesome documentation ([fortawesome.github.io/Font-Awesome/icons](http://fortawesome.github.io/Font-Awesome/icons/)) For example, the Facebook icon would be

	$icon-facebook

Other UI modules may rely upon these icon variables. If you want to replace them with say something from [Icomoon](https://icomoon.io/app), you'll need to provide these variables when excluding Font Awesome. Don't worry though, the Compass compiler will let you know if you forgot 😜


## Images and sprites

Our boilerplate's images directory has the following structure:

		images/
					/sprites/
									/common-1x
									/common-2x
									/common-compatibility

All of our sites really should be supporting high pixel density displays (eg, retina). Fortunately Compass's
spriting ability makes this really easy for us. We can also use spriting to help with compatibility images
such as alpha screens.

Note that all sprite images need to be saved as png's.

Included in the template is includes/_sprites.scss. _sprites.scss contains two items:

	- A sprite-background mixin for sprites with a high pixel density counterpart
	- A template to use vanilla compass sprites for compatibility


To use the sprite-background mixin, you'll need two images of the same name, one in the
images/sprites/common-1x and one in the images/sprites/common-2x directories. The mixin will automatically
use the right one.

		@include sprite-background(logo);

The template for vanilla compass sprites for compatibility is intended to be used for
older broser support. Think rounded corners and such things. Compatibility sprite images
should be saved in images/compatibility


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

### modules/_default-styles.scss

This module adds default styles to wysiwyg areas (maybe add a `.wysiwyg` for this?), most useful when using the Meyer reset. This isn't for generic site styles, which go in `_base.scss`.

## _base.scss

Any global styling needed goes here. This shouldn't become an everything bucket ala the old school `screen.css` file.

## ie.scss

We no longer include a separate ie.css stylesheet. A separate IE stylesheet is reduced in importance by SASS allowing nested selectors like the following:

	.thinger {
			.lt-ie8 & {
						display: none;
			}
	}

This compiles as follows:

		.lt-ie8 .thinger { display: none; }

Using these kinds of selects also allows code to be more maintainable my keeping all pieces of related code together. For instance, if you have styles for buttons, your buttons css can include the bass, fallbacks using Modernizr, media queries, and fallbacks for IE, all in the same declaration block.

If you need a more extensive IE stylesheet, ad one as needed.
