# HTML

## Table of Contents

1. [Valid HTML](#valid-html)
1. [Separation of Concerns](#separation-of-concerns)
   1. [Limit asset includes](#limit-asset-includes)
1. [Doctype](#doctype)
1. [Encoding](#encoding)
   1. [Character Entity References](#character-entity-references)
1. [Formatting](#formatting)]
   1. [New Lines](#new-lines)
   1. [Indentation](#indentation)
   1. [Attribute Quotes](#attribute-quotes)

## Valid HTML

Write valid and semantic HTML and use the [W3C HTML Validator](https://validator.w3.org/) to validate.

Use the following resources for researching the proper HTML5 element to use.
* [MDN](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)
* [HTML5Doctor](http://html5doctor.com)

Writing semantic and valid HTML goes a long way towards promoting accessibility and reusability and will reduce the number of cross browser bugs encountered.

```
<!-- Incorrect -->
<form>
  <a onclick="submitForm()">Submit</a>
</form>

<!-- Correct -->
<form>
  <input type="submit" value="Submit">
</form>
```

## Doctype

Always explicitly declare a document type and use HTML5 where possible. The doctype should be the first line in the file without any preceding whitespace.

[An XML (HTML) document without a doctype is invalid](https://www.xml.com/pub/a/2002/09/04/xslt.html) and excluding it from a page will cause browsers to render the document inconsistently.

```
<!-- Incorrect -->
_
_<!DOCTYPE html>

<!-- Correct -->
<!DOCTYPE html>
```

## Encoding

[Always specify the encoding of an HTML document](https://www.w3.org/International/questions/qa-html-encoding-declarations), prefer `UTF-8`, and place it immediately after the opening `<head>` tag as it must be within the first 1024 bytes.

### Character Entity References

Assuming teams are using the same encoding (preferably UTF-8) across editors and files, entity references such as `&rsaquo` are not necessary.

The exception to this is when considered inside a CMS. While entity references may not be necessary in code, they are usually necessary when entered into a rich text field in most CMS's.

## Separation of Concerns

Where possible, practice absolute separation of presentation (CSS), structure (HTML), and functionality (JS) layers.

Strictly separating these three layers makes maintenance easier and encourages modularity between components.

**Caveat** Most JavaScript libraries blur these lines to an unfortunate degree.

### Limit Asset Includes

Where possible, include a single JavaScript and CSS file on each page by bundling JavaScript together and compiling CSS with Sass to single files. Including multiple files requires additional network requests and increases the surface area of your linked content between structure and functionality or presentation.

## Formatting

### New Lines

Use a new line for every block level element.

```
<!-- Not Preferred -->
<article><p>Some content goes here</p></article>

<!-- Preferred -->
<article>
  <p>Some content goes here</p>
</article>

<!-- Preferred, <br> is an inline element. -->
<article>
  <p>Some content goes here, <br> New Line</p>
</article>
```

### Void Elements

Prefer to omit a closing `/` on [void elements](https://www.w3.org/TR/html/syntax.html#writing-html-documents-elements) as they [do not serve a purpose and are unnecessary](https://www.w3.org/TR/html/syntax.html#start-tags).

```
<!-- Not Preferred -->
<br />
<img src="" />

<!-- Preferred -->
<br>
<img src="">
```

### Indentation

Indent all blocks. Refer to your teams style of indentation for spaces or tabs and quantity.

```
<!-- Not Preferred -->
<header>
<img src="logo.png">
<header>

<!-- Preferred -->
<header>
  <img src="logo.png">
<header>  
```

### Attribute Quotes

Prefer double quotation marks around attribute values. If your team is using single quotes, be consistent.

```
<!-- Not Preferred -->
<header class='js-header'></header>

<!-- Preferred -->
<header class="js-header"></header>
```

[Always use quotation marks, even when it is possible to omit them.](https://www.w3.org/TR/REC-html40/intro/sgmltut.html#h-3.2.2)
