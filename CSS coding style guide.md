# CSS/LESS coding style guide

**Version:** 1.0.0
**Date**: March 31, 2014

This document extensively borrows from [Wordpress style guide], [GitHub style guide] and [Idiomatic CSS].

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[GitHub style guide]: https://github.com/styleguide/css
[Wordpress style guide]: http://make.wordpress.org/core/handbook/coding-standards/css/
[Idiomatic CSS]: https://github.com/necolas/idiomatic-css

## 1. Basics

- Files MUST use only UTF-8 without BOM and the Unix LF (linefeed) line ending.

- All project styles MUST be in one main file.

- Reusable dependancies (resets, mixins) SHOULD be in separate files.

- Code MUST use tabs for indenting, not spaces.

- There MUST NOT be a hard limit on line length; the soft limit MUST be 120 characters; lines SHOULD be 80 characters or less.

- Names of elements and classes, and IDs MUST be declared in lower case with dash separators.

- Opening braces MUST go on the same line, and closing braces MUST go on the next line after the body of the ruleset.

- Media queries MUST be grouped with the rulesets they modify.

- Properties MUST be logically grouped and SHOULD be consistently ordered.

- Properties MUST be followed by a colon and a space.

- Values MUST be wrapped in double quotes, but only if they need to.

- Attribute selectors MUST always use double quotes around values.


## 2. File structure

Here is the recommended top level section structure of the main file:

1. **Dependancies**: All reusable code elements, such as reset styles, mixin declarations and `@import` statements, MUST be placed at the top of the main file.
2. **Variables**: All variables MUST go here and SHOULD be further grouped by type, e.g. colours, sizes, delays and durations, etc.
3. **Typography**: All font family variables, scale definition, google font `@import` statements MUST go here. Default font size, font family and line height MUST be declared as styles of the `html` element here as well.
4. **Primitives**: All default styling for block and inline HTML elements MUST go here and SHOULD be further grouped by element type, e.g. anchors, headings, lists, tables, forms, etc.
5. **Layout**: This section MUST contain layout styles for landmark page elements, e.g. header, footer, sidebar, etc.
6. **Components**: Each component’s styles MUST be put here.
7. **Miscellaneous**: All debug styles MUST go here.

See Comments section for more.

## 3. Naming conventions

All names MUST use american spelling (i.e. “color”, not “colour”) to be consistent with the CSS/LESS naming.

All names MUST be declared in lowercase with dash separators.

### 3.1. Variables

Variable names MUST be prefixed with the type of value the variable contains.

Variable name MUST reflect where the variable is used, rather than what it contains, i.e. `@color-background`, not `@color-red`.

Here are some example of well-named variables:

```less
@color-text: #fff;
@color-body: #333;

@duration-loading: 1s;
@delay-loading: 100ms;

@size-sidebar: 60px;

@viewport-desktop: 1280px;
```


### 3.2. Classes and IDs

Class and ID names MUST describe the nature, logical state or behaviour, and MUST NOT contain presentational terms, i.e. colour, alignment or position.

## 4. Ruleset declarations

As a rule of thumb, rulesets SHOULD NOT be nested further than 3 levels deep.

Extend statements MUST be placed at the top of the ruleset.

Mixin calls MUST be logically grouped and SHOULD be placed at the top of the ruleset, right after any extend statements.

Rulesets MAY be separated by one blank line to reinforce logical grouping.

Opening curly brace MUST be on same line as the last selector preceded by a space.

Closing curly brace MUST be on its own line at the same indentation level as the selector.

An example:

```less
.selector-1,
.selector-2,
.selector-3[type="text"] {
    .box-sizing(border-box);
    display: block;

    background: #fff;
    background: linear-gradient(#fff, rgba(0, 0, 0, 0.8));
    color: #333;

    font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
}

.selector-a,
.selector-b {
    padding: 10px;
}
```

### 4.1. Selectors

Elements that occur exactly once inside a page SHOULD use IDs, otherwise, they MUST use classes.

Selectors MUST NOT contain more than one ID, e.g. `#header .search #quick-search` is considered harmful.


### 4.2. Properties

There SHOULD generally be no more than one property/value declaration per line.

Property declaration MUST contain a space character after the colon and before the value.

Each property declaration MUST end with a semicolon.

Each property MUST be indented once.

Properties MAY be separated by one blank line for grouping purposes.

Properties MUST be logically grouped and SHOULD be consistently ordered as described below:

```css
el {
    float: ;
    clear: ;

    position: ;
    top: ;
    right: ;
    bottom: ;
    left: ;
    z-index: ;

    display: ;
    visibility: ;
    overflow: ;
    clip: ;
    direction: ;
    unicode-bidi: ;

    box-sizing: ;
    width: ;
    min-width: ;
    max-width: ;
    height: ;
    min-height: ;
    max-height: ;

    margin: ;
    border: ;
    padding: ;
    outline: ;

    opacity: ;
    background: ;
    color: ;

    font: ;
    font-family: ;
    font-size: ;
    font-style: ;
    font-variant: ;
    font-weight: ;
    letter-spacing: ;
    line-height: ;
    text-align: ;
    text-decoration: ;
    text-indent: ;
    text-transform: ;
    vertical-align: ;
    white-space: ;
    word-spacing: ;

    list-style: ;

    table-layout: ;
    caption-side: ;
    border-collapse: ;
    border-spacing: ;
    empty-cells: ;

    quotes: ;
    counter-reset: ;
    counter-increment: ;
    content: ;
}
```

Zero values SHOULD NOT have units unless necessary, such as with `transition-duration`.

Line height SHOULD be unit-less, unless necessary to be defined as a specific pixel or rem value.

Colour values MUST be declared in lower-case hex values


### 4.3. Media queries

Media queries MUST be grouped with the statements they modify.

Rulesets inside the media query MUST be indented one level in.

Stylesheet with media queries MUST degrade nicely, i.e. the page should render fine in IE8.

### 4.4. Exceptions and slight deviations

Large blocks of single declarations can use a slightly different, single-line format. In this case, a space should be included after the opening brace and before the closing brace.

```css
.selector-1 { width: 10%; }
.selector-2 { width: 20%; }
.selector-3 { width: 30%; }
```

Long, comma-separated property values — such as collections of gradients or shadows — can be arranged across multiple lines in an effort to improve readability and produce more useful diffs. There are various formats that could be used; one example is shown below.

```css
.selector {
    background-image:
        linear-gradient(#fff, #ccc),
        linear-gradient(#f3c, #4ec);
    box-shadow:
        1px 1px 1px #000,
        2px 2px 1px 1px #ccc inset;
}
```


## 5. Comments

LESS code MUST be use `//` comment blocks exclusively, instead of `/* */`.

Comments MUST be placed on a new line above their subject.

Code SHOULD be broken into discrete sections and subsections.

Section title in LESS:

```less
// =================
// = Section title =
// =================
```

Section title in CSS:

```css
/* ================= */
/* = Section title = */
/* ================= */
```

Subsection title in LESS:

```less
// 
// Subsection title
// 
```

Subsection title in CSS:

```css
/*
    Subsection title
*/
```
