# Welcome

This is the Documentation Wiki for the Lite Responsive Dreamweaver Template at Western.

## About

The Lite Template is meant to be the responsive rendition of the current "static" template. It is a step toward the Drupal design, but not quite as "heavy". Neither is "static" the best descriptor now that it will respond to device and window sizes. Therefore, it is the "Lite" template.

### Goals

* Start from scratch using the latest web standards and modern practices: HTML5, SASS/.scss
* Maintain support for "modern browsers" and IE 8+ **(?)**
* Keep in mind the current/previous version of the template. Maintain the same Dreamweaver template regions for relatively simple conversions.
* Provide a custom.css file for users while maintaining the rest of the CSS/SASS in wwucommons.
* All new sites will use analytics and site/Western search capabilities (in the style of Drupal).
* Be efficient with media breakpoints.
* Incorporate Zen Grids.
* Provide responsive table styles, image solutions, and accessible content.
* Provide various page examples for users, such as: contact page, FAQ, staff listing, user "bio" page.
* H1's will be the specific page's title, rather than the site's name which will reside in the <title> element and banner.
* Provide users with a "quick guide" and more indepth articles about using the template. The quick guide on the future IT/WebTech site would remind users of the following types of tasks: Replace "sharename"; update contact information; edit <titles>; don't use inline styles, etc; use custom.css; don't try to be a link directory or portal (was previously more helpful before search engines became popular/widespread); etc.

### To-Do

* Convert em font-size units to rem when there is required amount of [browser support](http://caniuse.com/rem)

### Wiki features

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
Currently, we are importing several partials into the main.scss file. If adding more, be conscious about the order you place them in. _base is above _media-queries and _user because it contains variables and mixins that _layout and _user are dependent on. _media-queries could potentially modify things main.scss has already declared, so based on the cascade, it needed to be imported at the end of main.scss.

### Non-Compiling vs. Compiling
The _base partial contains variables and mixins that pretty much every other SCSS file will use. It is imported into every SCSS file so it is a good candidate for being non-compiling. Non-compiling means it will not generate its own CSS code. See: ["Sass code that doesn’t cause Sass to actually output CSS."](http://thesassway.com/beginner/how-to-structure-a-sass-project) Variables and mixins don't have a CSS equivalent and are simply helpers for the rest of our styles.

_fonts, _reset, and _zen all contain code that will be compiled into CSS as well as containing helpers that can be used elsewhere. They are imported at the top of our main.scss file for this reason.
### What Goes Where?

#### _base.scss and _mixins.scss
Non-compiling helper SCSS code. Variables, mixins, etc.

#### _media-queries.scss
Contains layout related classes grouped by media queries. Layout classes: "A class which fundamentally divides the page into sections."

Also contains media-query-specific styles.

#### _user.scss
Classes created specifically for other users/clients on campus to use in Dreamweaver's GUI. The users of these "unsemantic" classes will likely be working with Dreamweaver in the Design view. They are likely unfamiliar and uncomfortable with code so the classes we create should be as meaningful as possible to us, the developers, but still user-friendly for non-tech-savvy users.

Avoid explicitly presentational class names when possible, but if they are unavoidable, prefix the class declared in _user.scss with "style-". Prefix layout-related classes (like floats and clears) with "layout-"


# Classes & Naming Conventions

## Presentation-free Markup

In the vein of the [Separation of Concerns](http://en.wikipedia.org/wiki/Separation_of_concerns), we try to keep presentation (CSS/SCSS), structure (HTML), and function (JS/jQuery) separate. These three concepts support the most important part: the content.

Refrain from creating class names (an HTML attribute) based on how something looks.

"Class names should communicate *useful* information to *developers*. It’s helpful to understand what a specific class name is going to do when you read a DOM snippet, especially in multi-developer teams where front-enders won’t be the only people working with HTML components." -[Nicolas Gallagher on HTML Semantics](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)

```
.blue-left-links { color:blue; float:left; }
// Is less helpful when you happen to change the color scheme and layout later; but the HTML structure remains the same.

// A few months later, you are asked to change the colors to reflect an upcoming holiday:
.blue-left-links { color:pink; float:none; }
// blue-left-links no longer makes sense. Describe the function of this element.

// For example, if this class was applied to a <ul> element that was styled
// differently according to the time of year, the following would be more helpful:
$season-hue:pink;
.seasonal-navigation { color:$season-hue; }
// Note the use of a variable which can be used elsewhere with minimal upkeep next time the season changes.
```

## [SMACSS](http://smacss.com/) Concepts

"At the very core of SMACSS is categorization. By categorizing CSS rules, we begin to see patterns and can define better practices around each of these patterns." -[SMACSS](http://smacss.com/book/categorizing)

### Class Prefixes

### .module-

Classes prefixed with 'module-' represent "reusable, modular parts of our design". Our previous static template included "blue boxes" that would fit in this category.

* Social media icons and "widgets"
* Callout boxes
* Staff/faculty listings and directories
* Contact information that is often repeated
* Slideshow
* Gallery

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
.module-accordion.is-closed { ... }
.main-nav.is-open { ... }
```

## DRY - Don't Repeat Yourself

## Stick to Classes; Don't use IDs

Great explaination from [Stubbornella in the OOCSS FAQ](https://github.com/stubbornella/oocss/wiki/faq#should-i-use-ids-to-style-my-content):
"There are two reasons for not using IDs to style content:

1. They mess up specificity because they are too strong (the most important reason)
2. They are unique identifiers, which makes components built with them something like singletons, not reusable on the same page

On the other hand, IDs are great for linking and JS hooks. Put them in the HTML, just don’t use them for styles."