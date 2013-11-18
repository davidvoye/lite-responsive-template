# Welcome

This is the Documentation Wiki for the Lite Responsive Dreamweaver Template at Western.

## About

The Lite Template is meant to be the responsive rendition of the current "static" template. It is a step toward the Drupal design, but not quite as "heavy". Neither is "static" the best descriptor now that it will respond to device and window sizes. Therefore, it is the "Lite" template.

### Goals

* Start from scratch using the latest web standards and modern practices: HTML5, SASS/.scss
* Keep in mind the current/previous version of the template. Maintain the same Dreamweaver template regions for relatively simple conversions.
* Provide a custom.css file for users while maintaining the rest of the CSS/SASS in wwucommons.
* All new sites will use analytics and site/Western search capabilities (in the style of Drupal).
* Be efficient with media breakpoints.
* Incorporate Zen Grids.
* Provide responsive table styles, image solutions, and accessible content.
* Provide various page examples for users, such as: contact page, FAQ, staff listing, user "bio" page.
* H1's will be the specific page's title, rather than the site's name which will reside in the <title> element and banner.
* Provide users with a "quick guide" and more indepth articles about using the template. The quick guide on the future IT/WebTech site would remind users of the following types of tasks: Replace "sharename"; update contact information; edit <titles>; don't use inline styles, etc; use custom.css; do not use your site as a "portal"; etc.

### To-Do

* Convert em font-size units to rem when there is required amount of [browser support](http://caniuse.com/rem)

## Wiki features

This wiki uses the [Markdown](http://daringfireball.net/projects/markdown/) syntax.

The wiki itself is actually a git repository, which means you can clone it, edit it locally/offline, add images or any other file type, and push it back to us. It will be live immediately.

Go ahead and try:

```
$ git clone https://bitbucket.org/wwuweb/lite-responsive-template.git/wiki
```

Wiki pages are normal files, with the .md extension. You can edit them locally, as well as creating new ones.

# Style Guide Draft

## SASS/.scss Partials

### Order of Importing
Currently, we are importing several partials into the main.scss file. If adding more, be conscious about the order you place them in. _base is above _layout and _user because it contains variables and mixins that _layout and _user are dependent on. _media-queries likely modify things _layout has already declared, so based on the cascade, they needed to be imported after _layout.

### Non-Compiling vs. Compiling
The _base partial contains variables and mixins that pretty much every other SCSS file will use. It is imported into every SCSS file so it is a good candidate for being non-compiling. Non-compiling means it will not generate its own CSS code. Variables and mixins don't have a CSS equivalent and are simply helpers for the rest of our styles.

_fonts, _reset, and _zen all contain code that will be compiled into CSS as well as containing helpers that can be used elsewhere. They are imported at the top of our main.scss file for this reason. We don't want them repeated on every partial, so they are not imported in _base.

### What Goes Where?

#### _base.scss and _mixins.scss
Non-compiling helper SCSS code. Variables, mixins, etc.

#### _media-queries.scss
Contains layout related classes grouped by media queries. Layout classes: "A class which fundamentally divides the page into sections."

#### _user.scss
Classes created specifically for other users/clients on campus to use in Dreamweaver's GUI. The audience and users for these "unsemantic" classes will likely be working with Dreamweaver in the Design view. They are likely unfamiliar and uncomfortable with code so the classes we create should be as meaningful as possible to us, the developers, but still non-tech-user-friendly.

Avoid explicitly presentational class names when possible, but if they are unavoidable, prefix the class with "style-". Prefix layout-related classes (like floats and clears) with "layout-"

### _base.scss

Contains:

* Variables (for colors, math, commonly used increments)
* Framework imports (Compass, CSS3, CSS reset, Zen Grids)
* Font imports (Muli from Google Fonts)

### _mixins.scss

Contains:

* Modules created by Mixins. Mixins are a SASS feature.
* ["Sass code that doesn’t cause Sass to actually output CSS."](http://thesassway.com/beginner/how-to-structure-a-sass-project)

See .module- class prefix below for more information: "Classes prefixed with 'module-' represent 'reusable, modular parts of our design'" like boxes, image figures, or FAQ accordions.

### _layout.scss

Contains:

* Styles related to the structure and sectioning of the page.
* Will contain a lot of .layout- prefixed classes

See .layout- class prefix below for more information: "layout- describes a class which fundamentally divides the page into sections."

### _themes.scss (?)

Specific groups of variations from _layout.scss default styles. Potentially will be implemented if we allow users to select a sub-theme (based around lime green or gray instead of light blue, for example.)
Contains:

* Mostly color specific changes. Should be imported after _layout.scss

### _media-queries.scss

Contains:

* Media queries! Surprise.

## Presentation-free Markup

Refrain from creating class names based on how something looks.

```
.blue-left-links { color:blue; float:left; }
// Is less helpful when you happen to change the color scheme and layout later; but the HTML structure remains the same.

.blue-left-links { color:pink; float:none; }
// blue-left-links no longer makes sense. Describe the function of this element.

// For example, if this class was applied to a <ul> element that was styled
// differently according to the time of year, the following would be more helpful:
$season-hue:pink;
.seasonal-navigation { color:$season-hue; }
// Note the use of a variable which can be used elsewhere with minimal upkeep next time the season changes.
```

# Classes & Naming Conventions

Taking a bit from [SMACSS](http://smacss.com/).

## Class Prefixes
### .layout-

layout- describes a class which fundamentally divides the page into sections.
```
.layout-sidebar { display:block; } 
```
Most noteably, layout-s are relevant to our various Dreamweaver templates. They will typically be applied to the <body> element of a .shtml file according to their template. If a structural style from layout-x was required on layout-y, then ideally, .layout-x could be applied to a parent container. This reduces redundancy and increases specificity:
```
...
<body class="layout-y">
	...
	<article class="layout-x">
		<div>...</div>
	</article>
...
</body>
```
Prevents having to create a whole new class for this one style because we are DRY (Don't Repeat Yourself):
```
.layout-y .layout-x div { ... }
```

### .module-

Classes prefixed with 'module-' represent "reusable, modular parts of our design". Our previous static template included "blue boxes" that would fit in this category.

```
.module-box { @include box(); }

.module-box.float-left { @include box(left); }
```

### .is- (states)

Prefixing a class with .is- can be a good way to describe an action. It also visually separates them from other classes.
```
.is-open {}
.is-closed {}
.is-hidden { display:none; }
.is-active {}
.is-inactive {}
```

They can be combined with other classes in a helpful, readable way:
```
.module-faq.is-closed { @include faq(); @include closed; }
.main-nav.is-open { @include open; }
```

## DRY - Don't Repeat Yourself

## Stick to Classes; Don't use IDs

Great explaination from [Stubbornella in the OOCSS FAQ](https://github.com/stubbornella/oocss/wiki/faq#should-i-use-ids-to-style-my-content):
"There are two reasons for not using IDs to style content:

1. They mess up specificity because they are too strong (the most important reason)
2. They are unique identifiers, which makes components built with them something like singletons, not reusable on the same page

On the other hand, IDs are great for linking and JS hooks. Put them in the HTML, just don’t use them for styles."