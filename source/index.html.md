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
  <script src="https://embed.hellobestow.com/static/js/embedded-quote-iframe.js"></script>
</body>
```

```http
https://partners.hellobestow.com/enroll/
```

> When the above script executes, the resulting DOM will look something like this:

```html
<body>
  <script src="https://embed.hellobestow.com/static/js/embedded-quote-iframe.js"></script>
  <div style="height: auto">
    <iframe
      src="https://embed.hellobestow.com/?widget=basic1&isIframe=true"
      name="bestowQuote"
    >
      ...
    </iframe>
  </div>
</body>
```

```http
<NOT APPLICABLE>
```

**Both experiences below are provided samples. Simply click on the code sample tab that applies to your needs.**

**FOR SCRIPT USAGE (HTML):** All that is required to display Bestow's Quote Widget on your website is adding a script to your HTML. The script will bootstrap an `<iframe>` at the same level in the DOM tree. Therefore the script tag MUST be placed in the `<body>` in order to avoid semantically incorrect HTML and possible errors.

The embed widget supports initialization/auto-fill of form fields via HTML5 data attributes. All parameters need to be prefixed with `data-`. For example, the `products` parameter should be `data-products`).

**FOR QUERY PARAMETER USAGE (HTTP):** Provide a link in your application with the appropriate URL. The documentation will refer to `https://partners.hellobestow.com/enroll/` as the base URL. If you have been provided a different `Partner` landing page, please use that instead.

To access the API, you must include query parameters in the URL of your link (see `http` tab for examples).

# API

## Initialization Parameters

The widget can be _initialized_ with a combination of parameters if you so choose. It is important to note that the widget will ignore parameters that are appended without refreshing the page. The following parameters are supported as query params or data attributes:
One thing to note is that the default experience will use a 5 digit zip input to determine residence, but if the state param is provided it will use the state dropdown instead.

| Parameter                                            | Format                                                          | Description                                                                                                                       |
| ---------------------------------------------------- | --------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| gender                                               | m / f initial                                                   | Gender formatted as initial.                                                                                                      |
| date_of_birth, date_of_birth&#124;yyyymmdd, birthday | "dd/mm/yyyy", "yyyy-mm-dd", "yyyymmdd", "yyyymmdd 00:00:00 UTC" | Birthdate in any one of three supported parameter names and any one of four supported formats.                                    |
| height                                               | integer                                                         | Height in inches (displayed on the form as 2 separate values, feet and inches).                                                   |
| weight                                               | floating number, one decimal point                              | Weight in pounds (one decimal point allowed).                                                                                     |
| zip                                                  | 5-digit integer                                                 | 5 digit zipcode                                                                                                                   |
| state                                                | state initials (TX, MI, CA)                                     | Abbreviation of the state of residence. *Note* if this is provided, the quote will use the state dropdown instead of the zip input|
| coverage                                             | integer                                                         | The initial amount of coverage, in increments of 50,000 only.                                                                     |
| mincoverage                                          | integer                                                         | The minimum amount of coverage the user can possibly select, in increments of 50,000 only. (See caveat in coverage section).      |
| products                                             | product code                                                    | See "Products" section for details.                                                                                               |
| skipform                                             | boolean                                                         | Initializes to quote screen, bypassing the form. Only valid value is true, all others ignored. (See caveat in Skip Form section). |

> To auto-fill the form fields, provide any number of the following data parameters:

```html
<script
  data-gender="m"
  data-date_of_birth="01/01/1991"
  data-height="72"
  data-weight="175"
  data-state="TX"
  src="https://embed.hellobestow.com/static/js/embedded-quote-iframe.js"
/></script>
```

```http
https://partners.hellobestow.com/enroll/?gender=m&date_of_birth=19850101&height=72&weight=175&state=TX
```

## Campaign Parameters

You can provide `utm_` parameters for proper affiliate tracking. All parameters below are supported.

| Paremeter   |
| ----------- |
| utm_source  |
| utm_name    |
| utm_medium  |
| utm_content |
| utm_term    |

```html
<script
  data-utm_source="Source"
  data-utm_name="Name"
  data-utm_medium="Medium"
  data-utm_content="Content"
  data-utm_term="Term"
  src="https://embed.hellobestow.com/static/js/embedded-quote-iframe.js"
></script>
```

```http
https://partners.hellobestow.com/enroll/?utm_source=Source&utm_name=Name&utm_medium=Medium&utm_content=Content&utm_term=Term
```

## Coverage Options

The widget can be initialized with a preselected coverage amount, as well as a minimum value that prevents the user from selecting a lower coverage amount.

### Default Coverage Amount

You can specify the default coverage amount selected on the coverage slider. Provide the parameter with a dollar value as an integer. The number must be an increment of 50,000.

> To set a default coverage amount:

```html
<script
  data-coverage="150000"
  src="https://embed.hellobestow.com/static/js/embedded-quote-iframe.js"
/>
```

```http
https://partners.hellobestow.com/enroll/?coverage=150000
```

### Minimum Coverage Amount

You can control user access to a minimum coverage amount selectable on the coverage slider. Provide the parameter with a dollar value as an integer. Again, the number must be an increment of 50,000.

> To set a minimum coverage amount:

```html
<script
  data-mincoverage="150000"
  src="https://embed.hellobestow.com/static/js/embedded-quote-iframe.js"
/>
```

```http
https://partners.hellobestow.com/enroll/?mincoverage=150000
```

**CAVEAT:** If a `coverage` param is set to a value lower than the `mincoverage` param, the widget will ignore `coverage`, default to `mincoverage`, and generate an error in the console.

> This will default to mincoverage:

```html
<script
  data-coverage="150000"
  data-mincoverage="300000"
  src="https://embed.hellobestow.com/static/js/embedded-quote-iframe.js"
></script>
```

```http
https://partners.hellobestow.com/enroll/?coverage=150000&mincoverage=300000
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
  src="https://embed.hellobestow.com/static/js/embedded-quote-iframe.js"
/>
```

```http
https://partners.hellobestow.com/enroll/?gender=m&date_of_birth=01/01/1991&height=72&weight=175&state=TX&skipform=true
```

> This is invalid:

```html
<script
  data-gender="m"
  data-skipform="true"
  src="https://embed.hellobestow.com/static/js/embedded-quote-iframe.js"
></script>
```

```http
https://partners.hellobestow.com/enroll/?gender=m&skipform=true
```

## Products (i.e. term choice)

By default, all product terms are available to your users. But if you want to control your users' options on product term, simply provide a parameter/value for each product to make available.

**FOR SCRIPT USAGE (HTML):**

`data-products="BT1002"` - this means you want to include ONLY `BT1002`

`data-products="BT1002,BT2002"` - this means you want to include `BT1002` and `BT2002`.

**FOR QUERY PARAM USAGE (HTTP):** If using the Query Param implementation, separate each product into its own `products` parameter. See the example for use case.

`products=BT1002` - this means you want to include ONLY `BT1002`

`products=BT1002&products=BT2002` - this means you want to include `BT1002` and `BT2002`.

| Product Code | Product Term |
| ------------ | ------------ |
| BT0201       | 2 Years      |
| BT1002       | 10 Years     |
| BT2002       | 20 Years     |

> To restrict user available product terms to one product:

```html
<script
  data-products="BT1002"
  src="https://embed.hellobestow.com/static/js/embedded-quote-iframe.js"
/>
```

```http
https://partners.hellobestow.com/enroll/?products=BT1002
```

> To restrict down to multiple product terms:

```html
<script
  data-products="BT1002,BT2002"
  src="https://embed.hellobestow.com/static/js/embedded-quote-iframe.js"
/>
```

```http
https://partners.hellobestow.com/enroll/?products=BT1002&products=BT2002
```

## Theme Modification

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
  src="https://embed.hellobestow.com/static/js/embedded-quote-iframe.js"
/>
```

```http
https://partners.hellobestow.com/enroll/?fontcolor=FFF000&bgcolor=FF0000
```
