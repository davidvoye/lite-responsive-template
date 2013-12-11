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


* Create more flexible **site names** with jQuery and styles. Apply ".is-constrained-type-size" or a better class name when site name character count is more than ~50. Also remove "bottom:-35px;" when text wraps to a second line. Support even longer titles if necessary in custom.css. Support "hiding" (but still accessible) text and letting banner image have text.
* Replace text with **social media icons** in main navigation (at 750px+).
* Update **+/- icons for mobile nav**.
* Add **Western search** code. Currently only searches site.
* **Gallery**
* **Slideshow**
* Make **documentation multiple pages** or better organized.
* **Finish documentation**
* **Instructional documentation and Quick Start Guide** for users

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


### Where Does This Code Belong?

#### _base.scss and _mixins.scss
Non-compiling helper SCSS code. Variables, mixins, etc.

#### _user.scss
Classes created specifically for other users/clients on campus to use in Dreamweaver's GUI. The users of these "unsemantic" classes will likely be working with Dreamweaver in the Design view. They are likely unfamiliar and uncomfortable with code so the classes we create should be as meaningful as possible to us, the developers, but still user-friendly for non-tech-savvy users.

Avoid explicitly presentational class names when possible, but if they are unavoidable, prefix the class declared in _user.scss with "style-". Prefix layout-related classes (like floats and clears) with "layout-"

#### _media-queries.scss
Contains layout related classes grouped by media queries. Layout classes: "A class which fundamentally divides the page into sections."

Also contains media-query-specific styles.

> "The point here is to assign a name with abstracted meaning, so the numbers can change but the names stay the same. I'd avoid device names like "iPad" or whatever too, because that just sets up bad expectations and will date itself quickly.
> 
> Better are naming schemes that suggest relationships between the names themselves. Where one is obviously bigger or smaller than another." - [Chris Coyier on Naming Media Queries](http://css-tricks.com/naming-media-queries/)

Currently, our naming pattern follows geologic/geologic-ish terms for grain size, from smallest to largest:

> Clay, Silt, Sand, Pebble, Boulder, Mountain, Continent, Planet

#### _shame.scss

This is where all the hacky, sketchy, shameful styles live. This partial is not meant as a final solution, but a temporary place to use !important or other less-desired code until a better solution is found.

From [Harry Robert's article on shame.css](http://csswizardry.com/2013/04/shame-css/):
> "By putting your bodges, hacks and quick-fixes in their own file you do a few things:
> 
> * You make them stick out like a sore thumb.
> * You keep your ‘main’ codebase clean.
> * You make developers aware that their hacks are made very visible.
> * You make them easier to isolate and fix.
> * $ git blame shame.css."

Be sure to include documentation and notes inside of comments like these double forward-slashes.


# Classes & Naming Conventions

## Presentation-free Markup

In the vein of the [Separation of Concerns](http://en.wikipedia.org/wiki/Separation_of_concerns), we try to keep presentation (CSS/SCSS), structure (HTML), and function (JS/jQuery) separate. These three concepts support the most important part: the content.

Refrain from creating class names (an HTML attribute) based on how something looks.

> "Class names should communicate *useful* information to *developers*. It’s helpful to understand what a specific class name is going to do when you read a DOM snippet, especially in multi-developer teams where front-enders won’t be the only people working with HTML components." -[Nicolas Gallagher on HTML Semantics](http://nicolasgallagher.com/about-html-semantics-front-end-architecture/)

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

> "At the very core of SMACSS is categorization. By categorizing CSS rules, we begin to see patterns and can define better practices around each of these patterns." -[SMACSS](http://smacss.com/book/categorizing)

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

## Efficient Selectors

From [Mozilla Developer Network's "Writing Efficient CSS"](https://developer.mozilla.org/en-US/docs/Web/Guide/CSS/Writing_efficient_CSS):

* "Don't qualify ... rules with tag names or classes"
```
// Bad:
button#search { ... }
// Better:
.search-button { ... }
```

* "Use the most specific [selector] possible" and don't nest selectors deeper than ~3 levels
```
// Bad:
html body main article .module p.call-out { ... }
// Better:
.module .call-out { ... }
```

## DRY - Don't Repeat Yourself

Different ways to create and maintain reusable code.

```
// In this example, all three selectors have the same font color.
// Rather than declaring a specific hex color code multiple times:
.module-slide-caption { color: #003f87; }
h2 { color: #003f87; }
a:hover { color: #003f87; }

// Declare it once with a reusable variable:
$brandColor: #003f87;
.module-slide-caption { color: $brandColor; }
h2 { color: $brandColor; }
a:hover { color: $brandColor; }

// To be even more DRY, combine selectors
//(if this is the only property being declared for these selectors):
.module-slide-caption, h2, a:hover { color: $brandColor; }

// If these three selectors had other properties, this color could be @extend-ed with a placeholder selector:
%brand-voice { color: $brandColor; }
.module-slide-caption { font-size: 2em; @extend brand-voice; }
h2 { font-weight:bold; @extend brand-voice; }
a:hover { @include transition(.5s); @extend brand-voice; }

```

## Stick to Classes; Don't use IDs

Great explaination from [Stubbornella in the OOCSS FAQ](https://github.com/stubbornella/oocss/wiki/faq#should-i-use-ids-to-style-my-content):
> "There are two reasons for not using IDs to style content:
> 
> 1. They mess up specificity because they are too strong (the most important reason)
> 2. They are unique identifiers, which makes components built with them something like singletons, not reusable on the same page
> 
> On the other hand, IDs are great for linking and JS hooks. Put them in the HTML, just don’t use them for styles."


# File Structure

## Local site

* /customize
    * customize.css
    * site-banner.jpg
    * site-banner.psd
    * navigation.html
    * header.html
    * README / Instructions.txt

* /templates
    * sidebar.dwt
    * full-page.dwt
    * two-column.dwt
    * three-column.dwt

* /images
    * /gallery
    * /slideshow

* /documents

* index.shtml
* contact.shtml
* staff-faculty-listing.shtml
* faq.shtml

## wwucommons

* /js
    * western.js

* /styles
    * /css
    * /scss
        * main.scss
        * _base.scss
        * _fonts.scss
        * _media-queries.scss
        * _mixins.scss
        * _reset.scss
        * _shame.scss
        * _user.scss


# Design & Typography

## Layout

Our layout is build from [Zen Grids](http://zengrids.com/) and visually is a combination of the Static Template and WWUZEN for our Drupal sites.

### Repeatable & Reusable

#### Color Variables
We use SCSS variables of [Western's brand colors](http://news.wwu.edu/go/doc/1538/993731/Color-usage) throughout our styles.

#### Basic Unit
Variables are also used for number values. 5px and 10px were commonly used for margins and padding. Based on this pattern we created our "baseline"/basic unit of 20px. This number can be manipulated with simple math functions. See Baseline Grid below for more information.

#### Mixins

_mixins.scss contains reusable code that can be @include-ed. This provides consistency for a number of tasks we often come across, such as "hiding" text off-screen in place of a background-image or logo.
```
@mixin hide-text {
	text-indent: 100%;
	white-space: nowrap;
	overflow: hidden;
}
```

## Typography

## Type Scale & Hierarchy

### Resources
* [Golden Ratio Typography Calculator](http://www.pearsonified.com/typography/)
* [Type Scale](http://type-scale.com/)

### Our Type Scale

* Body font-size: 10px
* Body line height: 20px

* Body, paragraphs, h4, h5, h6: 13px (1.3em)
* h3: 17px (1.7em)
* h2: 21px (2.1em)
* h1: 31px (3.1em)

* It is simple to find the equivalent [em](http://css-tricks.com/css-font-size/) amount for pixels. Our base font-size is 10px, so any pixel font-size can just be moved over a decimal point to render the em value. 15px = 1.5em (based on 10px base).

### Baseline Grid

From [Fluid Baseline Grid](http://fluidbaselinegrid.com/):
> Baseline grids "establish a typographic hierarchy that improves readability and creates harmony within the text. Measure, leading, vertical rhythm, emphasis and scale are something we obsess about."

Our baseline grid is based on a 20px scale. This is represented by the variable $baseline in our SCSS (_base.scss):
```
// Baseline grid; basic unit
$baseline: 20px;
$half-base:($baseline/2); // 10px
$quarter-base:($baseline/4); // 5px
```

# Converting Static Template Sites to the Lite Responsive Template

## How To

## Differences Between the Static Template and the Lite Responsive Template

* Created separate styling classes for users and removed default underline for h2 elements. This should prevent users from only using headings (h1-h6) for styling purposes. Should encourage better use of headings for content hierarchy.

### File Structure

### Templates

### CSS

#### Old Classes and Selectors

(List equivalents for easy find and replace)

## Troubleshooting