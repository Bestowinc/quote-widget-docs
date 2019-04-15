---
title: Quote Widget API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - html
  - http

# toc_footers:
#   - <a href='#'>Sign Up for a Developer Key</a>
#   - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

# includes:
#   - errors

search: true
---

# Introduction

Welcome to the Quote Widget documentation!

# Get Started

> For the most basic usage:

```html
<body>
  <script src="https://embed.hellobestow.com/static/js/embedded-quote.js"></script>
</body>
```

```http
<NOT APPLICABLE>
```

> When the above script executes, the resulting DOM will look something like this:

```html
<body>
  <script src="https://embed.hellobestow.com/static/js/embedded-quote.js"></script>
  <script src="https://embed.hellobestow.com/static/js/runtime~main.fdfcfda2.js"></script>
  <div id="tooltip-root"></div>
  <div id="bestow-root-el">...</div>
  <script src="https://embed.hellobestow.com/static/js/2.092fa89c.chunk.js"></script>
  <script src="https://embed.hellobestow.com/static/js/main.405cb6fb.chunk.js"></script>
</body>
```

```http
<NOT APPLICABLE>
```

All that is required to display Bestow's Quote Widget on your website, is adding a script to your HTML!

**IMPORTANT:** The script will bootstrap the other scripts required to render the widget and then append the widget's root `<div>` at the same level in the DOM tree. Therefore the script tag MUST be placed in the `<body>` in order to avoid semantically incorrect HTML and possible errors.

## Sizing (html only)

> For sizing control:

```html
<div height="500" width="400">
  <script src="https://embed.hellobestow.com/static/js/embedded-quote.js"></script>
</div>
```

```http
<NOT APPLICABLE>
```

The default behavior is to expand to the width of whatever parent element the `<script>` is placed inside. To limit the size of the embedded widget, wrap the script in a container div and style the height and width.

## Initialization

The widget supports initialization/auto-fill of form fields via one of two methods:

1. You can inject a script tag directly into your website and use HTML5 data attributes to initialize it. Any parameter that is valid as a query param will also work as a data attribute. (All parameters need to be prefixed with `data-`. For example, the `products` parameter should be `data-products`).

2. Alternatively, you can use query parameters in the URL of the page in which the script is appended (see http tab for examples). **IMPORTANT NOTE:** URL query parameters take precedence over data attributes. If you have your script located at `http://your-domain.com/?height=72` and your script tag reads `<script src="https://embed.hellobestow.com/static/js/embedded-quote.js" data-weight="160"></script>`, the `data-weight` attribute will be ignored in favor of the query parameters and only `height` will be initialized.

Both experiences are provided samples. Simply click on the code sample tab that applies to your needs.

# API

## Initialization Parameters

The widget can be _initialized_ with a combination of parameters if you so choose. It is important to note that the widget will ignore parameters that are appended without refreshing the page. The following parameters are supported as query params or data attributes:

| Parameter                                  | Format                             | Description                                                                                                                       |
| ------------------------------------------ | ---------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| gender                                     | m / f initial                      | Gender formatted as initial.                                                                                                      |
| date_of_birth, date_of_birth&#124;yyyymmdd | dd/mm/yyyy, yyyy-mm-dd, yyyymmdd   | Birthdate in any one of three supported formats.                                                                                  |
| height                                     | integer                            | Height in inches (displayed on the form as 2 separate values, feet and inches).                                                   |
| weight                                     | floating number, one decimal point | Weight in pounds (one decimal point allowed).                                                                                     |
| state                                      | state initials (TX, MI, CA)        | Abbreviation of the state of residence.                                                                                           |
| coverage                                   | integer                            | The initial amount of coverage, in increments of 50,000 only.                                                                     |
| mincoverage                                | integer                            | The minimum amount of coverage the user can possibly select, in increments of 50,000 only. (See caveat in coverage section).      |
| products                                   | product code                       | See "Products" section for details.                                                                                               |
| skipform                                   | boolean                            | Initializes to quote screen, bypassing the form. Only valid value is true, all others ignored. (See caveat in Skip Form section). |

> To auto-fill the form fields, provide any number of the following data parameters:

```html
<script
  data-gender="m"
  data-date_of_birth="01/01/1991"
  data-height="72"
  data-weight="175"
  data-state="TX"
  src="https://embed.hellobestow.com/static/js/embedded-quote.js"
/></script>
```

```http
https://embed.hellobestow.com?gender=m&date_of_birth=19850101&height=72&weight=175&state=TX
```

## Coverage Options

The widget can be initialized with a preselected coverage amount, as well as a minimum value that prevents the user from selecting a lower coverage amount.

### Default Coverage Amount

You can specify the default coverage amount selected on the coverage slider. Provide the parameter with a dollar value as an integer. The number must be an increment of 50,000.

> To set a default coverage amount:

```html
<script
  data-coverage="150000"
  src="https://embed.hellobestow.com/static/js/embedded-quote.js"
/>
```

```http
https://embed.hellobestow.com?coverage=150000
```

### Minimum Coverage Amount

You can control user access to a minimum coverage amount selectable on the coverage slider. Provide the parameter with a dollar value as an integer. Again, the number must be an increment of 50,000.

> To set a minimum coverage amount:

```html
<script
  data-mincoverage="150000"
  src="https://embed.hellobestow.com/static/js/embedded-quote.js"
/>
```

```http
https://embed.hellobestow.com?mincoverage=150000
```

**CAVEAT:** If a `coverage` param is set to a value lower than the `mincoverage` param, the widget will ignore `coverage`, default to `mincoverage`, and generate an error in the console.

> This will default to mincoverage:

```html
<script
  data-coverage="150000"
  data-mincoverage="300000"
  src="https://embed.hellobestow.com/static/js/embedded-quote.js"
></script>
```

```http
https://embed.hellobestow.com?coverage=150000&mincoverage=300000
```

## Skip Form

If all information in the quote form is provided (refer to Form Auto-fill section), you can also opt to skip the form entirely and show your users their indicative quote info on-load.

**CAVEAT:** if the form is missing one of the required values, the `skipform` parameter will not be respected. Instead, the widget will show the form and generate an error in the console.

> To auto-fill and bypass the form, provide all form fields and the skipform parameter:

```html
<script
  data-gender="m"
  data-date_of_birth="01/01/1991"
  data-height="72"
  data-weight="175"
  data-state="TX"
  data-skipform="true"
  src="https://embed.hellobestow.com/static/js/embedded-quote.js"
/>
```

```http
https://embed.hellobestow.com?gender=m&date_of_birth=01/01/1991&height=72&weight=175&state=TX&skipform=true
```

> This is invalid:

```html
<script data-skipform="true"></script>
```

```http
https://embed.hellobestow.com?skipform=true
```

<!-- <aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside> -->

## Products (i.e. term choice)

By default, all product terms are available to your users. But if you want to control your users' options on product term, simply provide a parameter for each product to make available.

`data-products="BT1002"` - this means you want to include ONLY `BT1002`

| Product Code | Product Term |
| ------------ | ------------ |
| BT0201       | 2 Years      |
| BT1002       | 10 Years     |
| BT2002       | 20 Years     |

> To restrict user available product terms to one product:

```html
<script
  data-products="BT1002"
  src="https://embed.hellobestow.com/static/js/embedded-quote.js"
/>
```

```http
https://embed.hellobestow.com?products=BT1002
```

> To restrict down to multiple product terms, just add another products parameter:

```html
<script
  data-products="BT1002"
  data-products="BT2002"
  src="https://embed.hellobestow.com/static/js/embedded-quote.js"
/>
```

```http
https://embed.hellobestow.com?products=BT1002&products=BT2002
```

## Theme Modification (POC, not available yet)

You can modify some of the colors in the widget

| Parameter | Format      | Description                                                             |
| --------- | ----------- | ----------------------------------------------------------------------- |
| bgcolor   | hexidecimal | Changes the color of the widget card background.                        |
| fontcolor | hexidecimal | Changes the font color of components that use the theme's primary text. |

> To modify the theme colors:

```html
<script
  data-fontcolor="FFF000"
  data-bgcolor="FF0000"
  src="https://embed.hellobestow.com/static/js/embedded-quote.js"
/>
```

```http
https://embed.hellobestow.com?fontcolor=FFF000&bgcolor=FF0000
```
