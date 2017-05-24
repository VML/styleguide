# WGAC Accessibility

## Table of Contents
1. [Types of Accessibility](#types-of-accessibility)
1. [WAI-ARIA](#wai-aria)
1. [Accessible Styles](#accessibile-styles)
1. [Micro Data](#micro-data)
1. [Helper Code Snippets](#helper-code-snippets)
1. [Checkers](#checkers)
1. [Resources](#resources)

## Types of Accessibility

#### Visual Impairment
- Color blindness (Monochromacy, red-green, blue-yellow)
- Partially sighted (Corrected with contact lenses or glasses)
- Low vision (Cannot be corrected. Cataracts, glaucoma, macular degeneration, etc…)
- Total blindness

#### Physical Impairment
- Rely on a keyboard, hardware, or have trouble using a mouse

#### Hearing Impairment
- Partial impairment (low hearing, or deaf in one ear)
- Total deafness

## WAI-ARIA

> WAI-ARIA, the Accessible Rich Internet Applications Suite, defines a way to make Web content and Web applications more accessible to people with disabilities. It especially helps with dynamic content and advanced user interface controls developed with Ajax, HTML, JavaScript, and related technologies. With WAI-ARIA, developers can make advanced Web applications accessible and usable to people with disabilities. - [W3C](https://www.w3.org/WAI/intro/aria)

> ARIA enables developers to describe their widgets in more detail by adding special attributes to the markup. Designed to fill the gap between standard HTML tags and the desktop-style controls found in dynamic web applications, ARIA provides roles and states that describe the behavior of most familiar UI widgets. - [MDN](https://developer.mozilla.org/en-US/docs/Web/Accessibility/An_overview_of_accessible_web_applications_and_widgets)

#### Roles
Aria Roles tell a scren reader what function the element serves. For example `<div role="tooltip">` would tell a screen reader the element is a tooltip. Roles are categorized as: [abstract](https://www.w3.org/TR/wai-aria/roles#abstract_roles), [widget](https://www.w3.org/TR/wai-aria/roles#widget_roles), [document structure](https://www.w3.org/TR/wai-aria/roles#document_structure_roles), and [landmark](https://www.w3.org/TR/wai-aria/roles#landmark_roles).

#### Properties
[ARIA Properties](https://www.w3.org/TR/wai-aria/states_and_properties) describe the properties or meaning of an element. For example `<input aria-required="true">` would tell a screen reader the input is required.

#### States
[ARIA States](https://www.w3.org/TR/wai-aria/states_and_properties) describe the current status of an element. For example `<input aria-invalid="true">` would tell a screen reader the input is invalud.

---

### Simple rules to develop by

1. Utilize a native HTML5 element or attribute before relying on an ARIA equivalent. Some screen readers are not able to recognize HTML5 landmarks. That said, for best results you should utilize both. 

| HTML5       | ARIA                  |
| ----------- | :---------------------|
| `<header>`  | `role="banner"`       |
| `<nav>`     | `role="navigation"`   |
| `<main>`    | `role="main"`         |
| `<footer>`  | `role="contentinfo"`  |
| `<aside>`   | `role="complementary"`|
| `<section>` | `role="region"`       |
| `<article>` | `role="article"`      |
| `<form>`    | `role="form"`         |

2. Do not change native semantics 
```html
// incorrect
<h2 role="tab">Tab Heading</h2>

// correct
<div role="tab"><h2>Tab Heading</h2></div>
```

3. If you create a widget that a user can click, tap, drag, drop, slide, or scroll. A user must also be able to navigate to the widget and perform an equivalent action using the keyboard.

4. Do not use `role="presentation"` or `aria-hidden="true"` on a visible focusable element. If an interactive element is hidden using `display: none`, it will also be removed from the accessibility tree, which makes the addition of `aria-hidden="true"` unnecessary.

5. All interactive elements must have an [accessible name](http://www.w3.org/TR/accname-aam-1.1/#dfn-accessible-name)

```html
<!-- incorrect -->
<label>First name:</label> <input type="text">

<!-- correct: use for and id to associate inputs -->
<label for="first-name">First name:</label> <input id="first-name" type="text">

<!-- correct: wrap input inside of label -->
<label>First name: <input id="first-name" type="text"></label>

<!-- correct: include aria-label and placeholder attribute to cover visually and hearing impaired -->
<input aria-label="First name:" placeholder="First name:" type="text">
```

## Accessible Styles

#### Multi-device responsive design
1. Make sure you are utilizing the proper `viewport` meta tag. Do not set `maxiumum-scale=1` or `user-scaleable=no` as that will prevent users from zooming in if they need to.
```html
<!-- incorrect -->
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scaleable=no">

<!-- correct -->
<meta name="viewport" content="width=device-width, initial-scale=1">
```
2. Utilize relative units like `em` and `rem`
3. On mobile devices, assure that interactive elements like buttons or links are large enough, and have enough space around them, to make them easy to press without accidentally overlapping onto other elements.

#### Focus
Never set outline to 0 or none without providing focus alternatives. Any time we focus an element, we rely on built-in browser focus rings to style the element. Without the focus ring or styles, it's impossible for a keyboard user to tell which element has the focus.

Similar to utilizing `:hover`, you can use the `:focus` pseudo-class. Additionally styling `:active` pseudo-class will indicate interaction.

```scss
// At minimum you can add focus styles that match hover styles
.class:hover,
.class:focus {
  color: blue;
}
```
#### Colors and contrast
The recommended AA contrast ratio is 4.5:1 for all text. You can use [WAVE](https://chrome.google.com/webstore/detail/wave-evaluation-tool/jbbplnpkjmmeebjpijfedlgcdilocofh?hl=en-US), [Accessibility Developer Tools](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb), or [colorable](http://jxnblk.com/colorable/demos/text/) to identify contrast ratios.


## Micro Data
*(Coming Soon)*

## Helper Code Snippets
[Borrowed from HTML5 Boilerplate](https://github.com/h5bp/html5-boilerplate/blob/master/dist/css/main.css)

1. Hidden visually, while accessible to screen readers.
```scss
.visuallyhidden {
  border: 0;
  clip: rect(0 0 0 0);
  -webkit-clip-path: inset(50%);
  clip-path: inset(50%);
  height: 1px;
  margin: -1px;
  overflow: hidden;
  padding: 0;
  position: absolute;
  width: 1px;
  white-space: nowrap;
}

// Element is focusable while navigating via the keyboard
.visuallyhidden.focusable:active,
.visuallyhidden.focusable:focus {
    clip: auto;
    -webkit-clip-path: none;
    clip-path: none;
    height: auto;
    margin: 0;
    overflow: visible;
    position: static;
    width: auto;
    white-space: inherit;
}
```

2. Hide visually and from screen readers, but maintain layout
```scss
.invisible {
  visibility: hidden;
}
```

3. Hide visually and from screen readers
```scss
.hidden {
  display: none !important;
}
```

## Checkers
##### Websites
- [W3 Validator](http://validator.w3.org/nu/)
- [WAVE Web Accessibility Evaluation Tool](http://wave.webaim.org/)

##### Tools/Extensions
- [Siteimprove](https://chrome.google.com/webstore/detail/siteimprove-accessibility/efcfolpjihicnikpmhnmphjhhpiclljc?hl=en-US)
- [WAVE](https://chrome.google.com/webstore/detail/wave-evaluation-tool/jbbplnpkjmmeebjpijfedlgcdilocofh?hl=en-US)
- [OpenDyslexic](https://chrome.google.com/webstore/detail/opendyslexic/cdnapgfjopgaggbmfgbiinmmbdcglnam?hl=en)
- [Accessibility Developer Tools](https://chrome.google.com/webstore/detail/accessibility-developer-t/fpkknkljclfencbdbgkenhalefipecmb)
- [Color Contrast Analyser for Sketch](https://github.com/getflourish/Sketch-Color-Contrast-Analyser)

## Resources
##### Information
- [W3C: Using ARIA](https://www.w3.org/TR/using-aria/)
- [W3C: ARIA States & Properties](https://www.w3.org/TR/wai-aria/states_and_properties)
- [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA)
- [The A11Y Project](http://a11yproject.com/)
- [Hiding Content for Accessibility](https://snook.ca/archives/html_and_css/hiding-content-for-accessibility)
- [Invisible Content Just for Screen Reader Users](http://webaim.org/techniques/css/invisiblecontent/)

##### Examples
- [W3C: Landmarks](https://www.w3.org/TR/wai-aria-practices/examples/landmarks/index.html)
- [Screen Reader Landmark Navigation Example](https://dequeuniversity.com/assets/html/jquery-summit/html5/slides/landmarks-example.html)
- [OAA Accessibility](http://oaa-accessibility.org/)

##### Screen Readers
- [Voiceover](https://www.apple.com/accessibility/mac/vision/) (OSX, Free
- [NVDA](https://www.nvaccess.org/) (Windows, Free)
- [JAWS](http://www.freedomscientific.com/Downloads/JAWS) (Windows, $1000)
- [ChromeVox](https://chrome.google.com/webstore/detail/chromevox/kgejglhpjiefppelpmljglcjbhoiplfn?hl=en) (Chrome, Free)
- [Screen Reader Emulator](https://addons.mozilla.org/en-US/firefox/addon/fangs-screen-reader-emulator/) (Firefox, Free)