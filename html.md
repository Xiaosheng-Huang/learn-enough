## Basic HTML

### An HTML skeleton

Use browser’s *web inspector* to inspect the source.

 **Formatting HTML**

Edit > Lines > Auto Indent

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Page Title</title>
    <meta charset="utf-8">
  </head>
  <body>
  </body>
</html>
```

 [HTML validator](https://validator.w3.org/#validate_by_input)

## Filling in the index page

### Headings and Paragraph

### Text formatting

#### Emphasized text

t’s a common typesetting convention to emphasize terms using italics.

#### Strong text

### Links

It’s sometimes convenient for external links to open in a new browser tab. To do this, add the attribute `target="_blank"` (For [technical reasons](https://developers.google.com/web/tools/lighthouse/audits/noopener), it’s important to add the rather obscure `rel="noopener"` as well.) .

### Adding images

#### Hotlinking

*Gravatar* (which stands for “globally recognized avatar”) allows you to associate standard images with particular email addresses, and is used to display profile pictures on a large variety of websites, including GitHub and WordPress.

Gravatar URLs also support *query parameters*:

```
https://gravatar.com/avatar/ffda7d145b83c4b118f982401f962ca6?s=150
```

`s` stands for “size”,

## More pages, more tags

the `code` tag is rendered by most browsers in a monospace font.

### Tables

```html
<table>
  <tr>
    <th></th>
  </tr>
  <tr>
    <td></td>
  </tr>
</table>
```

`&ndash;` is character entity reference for a dash roughly the width of the letter “n”.

“escaping out” `<` and `>` with the HTML character entities `&lt;` (“less than”) and `&gt;` (“greater than”).

### Divs and spans

`blockquote` 

`br`

### Lists

```html
<ol>
  <li></li>
</ol>
<ul>
  <li></li>
</ul>
```

## Inline styling and CSS

### Text styling

```html
<span style="font-style: normal; font-size: 24px; font-weight: bold;
color: #ff0000;">Call me Ishmael.</span>
```

These are but a few of the many style properties available, which you can learn about at sites like [w3schools](https://www.w3schools.com/cssref/).

Don’t worry about trying to visualize the color corresponding to a hex code; that’s what [color pickers](https://www.google.com/search?q=color+picker) are for.

```html
  <h1 style="text-align: center;">A Softcover Book Report</h1>
```

### Floats

### Applying a margin

```html
<img src="images/moby_dick.png" alt="Moby Dick" height="200px"
style="float: left; margin-right: 40px;">
```

### More margin tricks

```html
<img src="images/sperm_whales.jpg" style="display: block; margin: 0 auto;">
```

### A taste of CSS

One of the simplest and most useful applications of CSS ids is for creating links to arbitrary HTML elements using a convenient hash symbol (#) syntax.



