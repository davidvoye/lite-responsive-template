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

## Wiki features

This wiki uses the [Markdown](http://daringfireball.net/projects/markdown/) syntax.

The wiki itself is actually a git repository, which means you can clone it, edit it locally/offline, add images or any other file type, and push it back to us. It will be live immediately.

Go ahead and try:

```
$ git clone https://bitbucket.org/wwuweb/lite-responsive-template.git/wiki
```

Wiki pages are normal files, with the .md extension. You can edit them locally, as well as creating new ones.

# Style Guide Draft

## Presentation-free Markup

Refrain from creating class names based on how something looks.

```
.blue-left-links { color:blue; float:left; }
// Is less helpful when you happen to change the color scheme and layout later; but the HTML structure remains the same.
.blue-left-links { color:pink; float:none; }
// blue-left-links no longer makes sense. Describe the function of this element. For example, if this class was applied to a <ul> element that was styled different according to the time of year, this would be more helpful:
$season-hue:pink;
.seasonal-navigation { color:$season-hue; }
// Note the use of a variable which can be used elsewhere with minimal upkeep next time the season changes.
```

## DRY - Don't Repeat Yourself