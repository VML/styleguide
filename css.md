# CSS and Sass

## Table of Contents

1. [Validity](#validity)
1. [Encoding](#encoding)
1. [Naming](#naming)
   1. [BEM](#bem)
   1. [Naming Style](#naming-style)
   1. [Prefixing](#prefixing)
      1. [Namespace](#namespacing)
      1. [JavaScript](#javascript)
      1. [Added with JavaScript](#added-with-javascript)
1. [Selectors](#selectors)
1. [Property Shorthand v. Longhand](#shorthand)
1. [Units](#units)
   1. [0](#zeroes)
1. [Formatting](#formatting)
   1. [Declaration Order](#declaration-order)
   1. [Indentation](#indentation)
   1. [Semicolons](#semicolons)
   1. [Property Names](#property-names)
   1. [Declaration Blocks](#declaration-blocks)
   1. [Selector Separation](#selector-separation)
   1. [Rule Separation](#rule-separation)
   1. [Declaration Separation](#declaration-separation)
 1. [Quotation Marks](#quotation-marks)
1. [Sass](#sass)
   1. [Sass Syntax](#sass-syntax)
   1. [Ordering](#ordering)
   1. [Nested Selectors](#nested-selectors)
   1. [Variables](#variables)
   1. [Mixins](#mixins)
   1. [Extend](#extend)
   1. [Components](#components)

## Validity

Write valid and semantic CSS and use the [W3C CSS Validator](https://jigsaw.w3.org/css-validator/) to validate.

Writing semantic and valid CSS goes a long way towards promoting accessibility and reusability and will reduce the number of cross browser bugs encountered.

## Encoding

[Always specify the encoding](https://www.w3.org/International/questions/qa-css-charset) type of the CSS document using the [`@charset` rule](https://developer.mozilla.org/en-US/docs/Web/CSS/@charset). Note that you will also need to *save* the document in that encoding type.

```
/* Incorrect, space in front. */
_@charset "UTF-8"

/* Correct */
@charset "UTF-8"
```

The browser will first look for an HTTP header for an encoding type, then the HTML document, and finally the CSS document.

## Naming

1. Be consistent
1. Be expressive

Naming CSS selectors is one of the hardest parts of writing quality, scalable CSS, and can vary widely from person to person.

### BEM

Separate words class names by a hyphen, double hyphen, or double underscore in accordance with the [BEM guidelines](http://getbem.com/naming/).

Do not concatenate words or abbreviations by camelCasing or another method other than hyphen, double hyphen, or double underscore in order to improve scannability.

```
/* Not Preferred */
.vmlHeader {}

/* Preferred */
.vml-header {}
```

### Naming Style

Find a balance between names that are expressive names but not overly verbose for a reduced byte count and improved scannability.

```
/* Not Preferred */
.vml-navigation {}

.vml-hdr {}

/* Preferred */
.vml-nav {}

.vml-header {}
```  

### Prefixing
#### Namespace

Prefix selectors with a project specific prefix.

In large projects as well as for code that gets embedded in other projects or on external sites use prefixes (as namespaces) for class names. Use short, unique identifiers followed by a dash.

Using namespaces helps preventing naming conflicts and can make maintenance easier, for example in search and replace operations.

```
.vml-help {}
```

#### JavaScript

Avoid binding styles and functionality to the same class name. Instead prefer to prefix any class that you target with JavaScript with a `js-` to indicate that removal or changing that class will have side effects beyond styling.

Do not style classes prefixed with `js-`. Prefer to add another descriptive class namespaced for the project that you can attach styles to.

```
.js-help {}
.js-do-this {}
```

#### Added with JavaScript

In most cases prefer to avoid adding a class with JavaScript that does not exist in markup. Doing so will avoid confusion and make it easier for developers to inspect and learn more about your project without having a deep domain knowledge.

When it is necessary to add a JavaScript class that does not exist in markup, prefix the class with `jsa-` to indicate that the class was added with JavaScript. These classes **may** have styles attached to them.

```
.jsa-help {}
.jsa-do-this {}
```

## Selectors

Avoid overqualifying selectors. This is usually solved by being expressive with BEM, but prefer a flat selector structure with reduced / no nesting.

Avoiding unnecessary ancestor selectors is useful for [performance](http://www.stevesouders.com/blog/2009/06/18/simplifying-css-selectors/) [reasons](https://csswizardry.com/2011/09/writing-efficient-css-selectors/) as well as readability and maintenance.

```
/* Not Preferred */
header.vml-header {}
div.vml-error {}

/* Preferred */
.vml-header {}
.vml-error {}
```

## Shorthand

This largely depends on comfort level. Some shorthand properties are [incredibly complex](https://developer.mozilla.org/en-US/docs/Web/CSS/grid) and prone to errors.

Some shorthand properties are [much simpler](https://developer.mozilla.org/en-US/docs/Web/CSS/padding).

## Units
### Zeroes

1. Omit units after `0` unless specifically required (flex-basis).
1. Omit leading `0`s.
1. Omit trailing `0`s.

```
/* Not Preferred */
.vml-error {
  height: 0px;
}

.vml-error {
  height: 0.8px;
}

.vml-error {
  height: .10px;
}

/* Preferred */
.vml-error {
  height: 0;
}

.vml-error {
  flex: 0px;
}

.vml-error {
  height: .8px;
}

.vml-error {
  height: .1px;
}
```

## Formatting
### Declaration Order

Currently there are three display styles:

1. Alphabetical Order
2. Declaration Type (position, display, colors ... )
3. [Concentric CSS](https://github.com/brandon-rhodes/Concentric-CSS) (starts outside, moves inward)

|      | Alphabetical                                                        | Declaration                                                        | Concentric                                           |
|------|---------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------|
| Pros | No argument about sorting of properties.                            | Declarations are grouped together.                                 | No argument about sorting of properties.             |
| Cons | Weird not seeing width & height or bottom & top next to each other. | Lots of room for interpretation, where does white-space belong to? | Requires time to adapt & recall order of properties. |

Focusing on alphabetical or concentric requires recollection or time to sort accordingly. Utilizing declaration leaves some room for interpretation. However, declarations are grouped together and just as easy to find. There’s no hard rule set on ordering, especially when most rule declarations contain on average 5–8 properties.

Here is a suggested declaration order:

- Display
- Positioning
- Colors & Typography
- View: Opacity & Visibility
- CSS3: Animations, Transforms, Transitions
- Miscellaneous: Pointers, Overflows, Scrolling …
- Z-index

This decision should be left to each team.

### Indentation

Indent all [block content](https://www.w3.org/TR/CSS21/syndata.html#block) to reflect hierarchy and improve scannability.

```
@media screen, projection {

  html {
    background: #fff;
    color: #444;
  }

}
```

### Semicolons

[Use a semicolon after each declaration](https://www.w3.org/TR/css-syntax-3/#syntax-description). Omitting the final semicolon can lead to inconsistent results across parsers.

```
/* Not preferred */
.vml-header {
  display: block;
  color: white
}

/* Preferred */
.vml-header {
  display: block;
  color: white;
}
```

### Property Names

Prefer to use a single space after a property name's colon, but no space separating the property name from the colon.

```
/* Not Preferred */
.vml-header {
  color : white;
}

/* Not Preferred */
.vml-header {
  color:white;
}

/* Preferred */
.vml-header {
  color: white;
}
```

### Rule Blocks

Prefer to use a single space between the last selector and the opening [declaration block](https://drafts.csswg.org/css-syntax-3/#declaration) `{` for readability.

```
/* Not Preferred */
.vml-header{
  color: white;
}

/* Preferred */
.vml-header {
  color: white;
}
```

## Separation

### Rule Separation

Prefer to separate rule blocks by a single blank line for readability.

```
/* Not Preferred */
.vml-header {
  color: white;
}
.vml-footer {
  color: black;
}

/* Preferred */
.vml-header {
  color: white;
}

.vml-footer {
  color: white;
}
```

### Selector Separation

Separate [selectors](https://www.w3.org/TR/css3-selectors/) by a single new line and a comma for readability.

```
/* Not Preferred */
.vml-header, .vml-footer{
  color: white;
}

/* Preferred */
.vml-header,
.vml-footer {
  color: white;
}
```

### Declaration Separation

Separate declarations by a semicolon and a new line.

```
/* Not Preferred */
.vml-header {
  background: blue; color: white;
}

/* Preferred */
.vml-header {
  background: blue;
  color: white;
}
```

## Quotation Marks

Prefer [single or double quotation marks](https://drafts.csswg.org/css-syntax-3/#consume-token), do not omit quotation marks.

## Sass
### Sass Syntax

Prefer [expressive and modular code](http://thesassway.com/editorial/sass-vs-scss-which-syntax-is-better#pros-for-scss), always use the `.scss` syntax. It is close enough to CSS to not obfuscate the language excessively but offers substantial benefits over 'vanilla' CSS.

### Ordering

Try to group external (`@include`) declarations together at either the beginning of the end of the declaration set. Grouping at the beginning of the declaration set makes them easier to override.

```
/* Not Recommended: Scattered throughout */

.vml-header {
  background: #fff;
  @include transition();
  color: #000;
  @include hover-state();
}

/* Recommended: Grouped at the beginning */

.vml-header {
  @include transition();
  @include hover-state();
  background: #fff;
  color: #000;
}
```

### Nested Selectors

Prefer to not nest selectors unless absolutely necessary. There are exceptions to this in the cases of things like pseudo-selectors. When nesting is necessary always group them at the end of the set.

If nesting is necessary, always use the `&` nesting symbol instead of simply adding a nested selector and assuming the following developer will understand.

Under no circumstance nest a named partial selector. This makes code significantly more difficult to follow and more error prone.

Always separate nested selectors by 2 line breaks above.

```
/* Not Recommended: Nested selector in the middle of the set. */

.vml-header {
	background: #fff;

	& .vml-blue {
	  color: blue;
	}

	color: #000;
}

/* Not Recommended: Nested partial named selector. */

.vml-header {
	background: #fff;
	color: #000;

	&--blue {
	  color: blue;
	}
}

/* Not Recommended: Nested selector without & */

.vml-header {
	background: #fff;
	color: #000;

	.vml-blue {
	  color: blue;
	}
}

/* Recommended: Split named selectors */

.vml-header {
	background: #fff;
	color: #000;
}

.vml-header--blue {
  color: blue;
}

/* Recommended: Nest selectors with & */

.vml-header {
	background: #fff;
	color: #000;

	& .vml-blue {
	  color: blue;
	}
}

```

### Variables

Where possible, prefer to hyphenate variable names as opposed to camel casing or underscoring.

Hyphenating variable names keeps syntax closer to the preferred BEM method and helps maintain separation of syntax between JavaScript and CSS.

```
/* Not Preferred: Camel cased and underscored variables */
$vml_blue:
$vmlBlue:

/* Preferred: Hyphenated variables */
$vml-blue:
```

### Mixins

Mixins are best used to encourage DRY code and useful abstractions. Note that excessive use of Mixins that do not accept arguments can lead to a bloated CSS file if they are included multiple times.

Where possible, prefer to use a mixin only if it accepts arguments. If a mixin does not accept arguments consider creating a utility or generic class that can be applied to an element.

### Extend

`@extend` should only be used with placeholders, never with classes.

Using `@extend` with classes should be avoided because it has unintuitive and potentially dangerous behavior, especially when used with nested selectors. Even extending top-level placeholder selectors can cause problems if the order of selectors ends up changing later (e.g. if they are in other files and the order the files are loaded shifts). Gzipping should handle most of the savings you would have gained by using @extend, and you can DRY up your stylesheets nicely with mixins.

### Components

Sass should be broken out into as many component files as makes sense for your project. Sometimes that means writing a file per atom, sometimes it means writing a file per component.

Abstracting your code into a highly modular fashion makes it easier to extend functionality and contributes to an overall atomic workflow.

#### Directory Structure

**Usually used when not in a restrictive CMS or opinionated JavaScript framework**

When building the directory structure in projects using Sass it is sometimes beneficial to group "like" types and do single a single `@import` per type into a larger composite file. This saves a lot of time tracking down individual files and ensuring that files get imported in the proper order.

For example:

```
css
-- components
-- -- componentX
-- -- -- _imports.scss
-- -- -- _componentX.scss
-- -- -- _componentXHeader.scss
-- -- _imports.scss // _imports.scss should import the _imports.scss from each of the component directories.
-- mixins
-- -- _imports.scss
-- functions
-- -- _imports.scss
-- variables
-- -- _colors.scss
-- -- _typography.scss
-- -- _imports.scss // The _imports.scss file in each directory should import all files in the given directory, such as @import _colors; @import _typography;
-- styles.scss // The styles.scss should include single line imports of variables/_imports.scss; functions/_imports.scss etc.
```
