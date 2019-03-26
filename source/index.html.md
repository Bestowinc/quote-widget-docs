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
<html>
  <body>
    <script src="https://embed.hellobestow.com/static/js/embedded-quote.js" />
  </body>
</html>
```

```http
https://embed.hellobestow.com/
```

The Quote widget is usable in two ways:

1. You can inject a script tag directly into your website and use customization data parameters (html). All parameters need to be prefixed with `data-`. For example, the `products` parameter should be `data-products`.
2. Alternatively, you can direct users to a link and provide customization query parameters (http).

Both experiences are provided samples. Simply click on the code sample tab that applies to your needs.

# Customization

## Sizing (html only)

> For sizing control:

```html
<html>
  <body>
    <div height="500" width="400">
      <script src="https://embed.hellobestow.com/static/js/embedded-quote.js" />
    </div>
  </body>
</html>
```

```http
<NOT APPLICABLE>
```

To determine the size of the embed, wrap the script in a container div and style the height and width.

## Form Auto-fill

To auto-fill the quote form on-load, provide their associative data parameters.

| Parameter | Format                             | Description                                                                                  |
| --------- | ---------------------------------- | -------------------------------------------------------------------------------------------- |
| gender    | m / f initial                      | Gender formatted as initial.                                                                 |
| dob       | yyyymmdd                           | Birthdate integer formatted in the order of year, month, day. No hyphens or slashes.         |
| height    | integer                            | Calculate 12 \* number of feet + number of inches (filled on the form as 2 separate values). |
| weight    | floating number, one decimal point | Weight in pounds (one decimal point allowed).                                                |
| state     | state initials                     | Initials of the state of residence.                                                          |

> To auto-fill the form fields, provide any number of the following data parameters:

```html
<html>
  <body>
    <script
      data-gender="m"
      data-dob="19850101"
      data-height="72"
      data-weight="175"
      data-state="TX"
      src="https://embed.hellobestow.com/static/js/embedded-quote.js"
    />
  </body>
</html>
```

```http
https://embed.hellobestow.com?gender=m&dob=19850101&height=72&weight=175&state=TX
```

## Skip Form

If all information in the quote form is provided (refer to Form Auto-fill section), you can also opt to skip the form entirely and show your users their indicative quote info on-load.

> To auto-fill and bypass the form, provide all form fields and the skipform parameter:

```html
<html>
  <body>
    <script
      data-gender="m"
      data-dob="19850101"
      data-height="72"
      data-weight="175"
      data-state="TX"
      data-skipform="true"
      src="https://embed.hellobestow.com/static/js/embedded-quote.js"
    />
  </body>
</html>
```

```http
https://embed.hellobestow.com?gender=m&dob=19850101&height=72&weight=175&state=TX&skipform=true
```

<!-- <aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside> -->

## Products

By default, all product terms are available to your users. But if you want to control your users' options on product term, simply provide a parameter for each product to make available.

`data-products="BT1002"` - this means you want to exclude all other products besides `BT1002`

| Product Code | Product Term |
| ------------ | ------------ |
| BT0201       | 2 Years      |
| BT1002       | 10 Years     |
| BT2002       | 20 Years     |

> To restrict user available product terms to one product:

```html
<html>
  <body>
    <script
      data-products="BT1002"
      src="https://embed.hellobestow.com/static/js/embedded-quote.js"
    />
  </body>
</html>
```

```http
https://embed.hellobestow.com?products=BT1002
```

> To restrict down to multiple product terms, just add another products parameter:

```html
<html>
  <body>
    <script
      data-products="BT1002"
      data-products="BT2002"
      src="https://embed.hellobestow.com/static/js/embedded-quote.js"
    />
  </body>
</html>
```

```http
https://embed.hellobestow.com?products=BT1002&products=BT2002
```

## Default Coverage Amount

You can specify the default coverage amount selected on the coverage slider. Provide the parameter with a dollar value as an integer. The number must be one of the available options.

> To set a default coverage amount:

```html
<html>
  <body>
    <script
      data-coverage="150000"
      src="https://embed.hellobestow.com/static/js/embedded-quote.js"
    />
  </body>
</html>
```

```http
https://embed.hellobestow.com?coverage=150000
```

## Minimum Coverage Amount

You can control user access to a minimum coverage amount selectable on the coverage slider. Provide the parameter with a dollar value as an integer. The number must be one of the available options.

> To set a minimum coverage amount:

```html
<html>
  <body>
    <script
      data-mincoverage="150000"
      src="https://embed.hellobestow.com/static/js/embedded-quote.js"
    />
  </body>
</html>
```

```http
https://embed.hellobestow.com?mincoverage=150000
```

## Theme Modification (POC, not available yet)

You can modify some of the colors in the widget

| Parameter | Format      | Description                                                             |
| --------- | ----------- | ----------------------------------------------------------------------- |
| bgcolor   | hexidecimal | Changes the color of the widget card background.                        |
| fontcolor | hexidecimal | Changes the font color of components that use the theme's primary text. |

> To modify the theme colors:

```html
<html>
  <body>
    <script
      data-fontcolor="FFF000"
      data-bgcolor="FF0000"
      src="https://embed.hellobestow.com/static/js/embedded-quote.js"
    />
  </body>
</html>
```

```http
https://embed.hellobestow.com?fontcolor=FFF000&bgcolor=FF0000
```
