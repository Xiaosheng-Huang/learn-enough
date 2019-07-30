## Introduction to CSS

### CSS always be changing

using a tool like [CanIUse](http://www.caniuse.com/) to figure out how well-supported the style is. 

### Sample site setup

```
$ cd                                   
$ mkdir -p repos/<username>.github.io  
$ cd repos/<username>.github.io
$ touch index.html 
```

## CSS values: color and sizing

### CSS color

#### Setting transparency via rgba()

0 is transparent, 1 is opaque.

### Percentages

### em

### rem

### vh, vw

### Pleasing fonts

## The box model

### Inline vs. block

#### display: none

#### display: block

#### display: inline

#### display: inline-block

#### display: flex

### Margins, padding, and borders

```css
box-sizing: border-box;
```

#### Margin collapsing

### Floats

#### Clearing floats

```css
.clearfix:after {
  visibility: hidden;
  display: block;
  font-size: 0;
  content: " ";
  clear: both;
  height: 0;
}
```

### overflow

`overflow`

`visible`

`scroll`

### Inline block

```css
.social-list {
  list-style: none;
  padding: 0;
}
.social-list > li {
  display: inline-block;
}
```

There are little spaces between them

### Margins for boxes

`max-width`

`min-width`

#### negative margins

### Fun with borders

#### Making circles

```css
border-radius: 50%;
font-family: helvetica, arial, sans;
vertical-align: middle;
text-decoration: none;
text-transform: uppercase;
```

To find out which common fonts are available on which operating systems, consult a resource like [CSS Font Stack](http://www.cssfontstack.com/).

#### Line height

## Laying it all out

### Jekyll

static site generator

Liquid (the template language used by Jekyll) is widely used in systems like the [Shopify](http://shopify.com/) ecommerce platform.

#### Installing and running Jekyll

Jekyll is distributed as a Ruby *gem*.

**Xcode command line tools**

```
$ xcode-select --install
```

**Homebrew**

You can think of a package manager as an App Store that runs at the command line and is filled with free open-source software.

```
$ /usr/bin/ruby -e "$(curl -fSL https://www.learnenough.com/homebrew)"
```

**Ruby Environment (rbenv)**

*rbenv* is a utility that manages different Ruby versions and makes sure that Ruby software packages (called *gems*) get placed in the right spot for Ruby to find.

```
$ brew install rbenv    # automatically installs ruby-build as well
```

```
$ rbenv init
$ echo 'eval "$(rbenv init -)"' >> ~/.bash_profile
$ source ~/.bash_profile
```

every once in a while it’s a good idea to update Homebrew itself and then upgrade the installed packages as follows:

```
  $ brew update
  $ brew upgrade
```

**New Ruby version**

```
$ rbenv install 2.6.3
```

After the Ruby installation finishes, we need to tell the system that there’s a new version of Ruby:

```
$ rbenv rehash
```

```
$ rbenv global 2.6.3
```

At this point, restart your shell program to make sure all the settings are properly updated.

For future work, you may want to use specific versions of Ruby on a per-project basis, which can be done by creating a file called `.ruby-version` in the project’s root directory and including the version of Ruby to be used. (You’ll also have to install it using `rbenv install <version number>`)

when installing Ruby software via *gems*, it’s often convenient to skip the installation of the local documentation:

```
$ echo "gem: --no-document" >> ~/.gemrc
```

the RubyGems package manager comes for free with Ruby.

```
$ gem install jekyll -v 3.5.1
```

run the Jekyll server in project directory:

```
$ jekyll serve
```

the Jekyll app should be available at the URL http://localhost:4000.

The default port number for the World Wide Web is port 80, while the default port for a secure connection is 443. Other common port numbers include 21 ([ftp](https://en.wikipedia.org/wiki/File_Transfer_Protocol)), 22 ([ssh](https://en.wikipedia.org/wiki/Secure_Shell)), and 23 ([telnet](https://en.wikipedia.org/wiki/Telnet)).

we can set a different port number as follows:

```
$ jekyll serve --port 4001
```

After starting the Jekyll server, you should find a new folder in your project called `_site`.

### The layout file

the Jekyll convention for layouts is to place these files in a directory called `_layouts`:

```
$ mkdir _layouts
```

```
$ cp index.html _layouts/default.html
```

replace the entire contents of `index.html` with the Jekyll *frontmatter*:

```html
---
layout: default
---
```

### CSS file and reset

```
$ mkdir css
$ touch css/main.css
```

A standard CSS reset

```css
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center, dl, dt, dd, ol, ul, li,
fieldset, form, label, legend, table, caption,
tbody, tfoot, thead, tr, th, td, article, aside,
canvas, details, embed, figure, figcaption, footer,
header, hgroup, menu, nav, output, ruby, section,
summary, time, mark, audio, video {
  margin: 0;
  padding: 0;
  border: 0;
  font: inherit;
  vertical-align: baseline;
}
/* HTML5 display-role reset for older browsers */
article, aside, details, figcaption, figure,
footer, header, hgroup, menu, nav, section {
  display: block;
}
body {
  line-height: 1;
}
blockquote, q {
  quotes: none;
}
blockquote:before, blockquote:after,
q:before, q:after {
  content: '';
  content: none;
}
table {
  border-collapse: collapse;
  border-spacing: 0;
}
strong, b {
  font-weight: bold;
}
em, i {
  font-style: italic;
}
a img {
  border: none;
}
/* END RESET*/
```

### Includes intro

Jekyll includes are located in a folder called `_includes`.

```
$ mkdir _includes
$ touch _includes/head.html
```

include the contents of `head.html` back into the `default.html` layout

```html
{% include head.html %}
```

**Style Note: Style HTML5 elements with classes**

When an old browser encounters new HTML tags, any styles are ignored.

### Advanced selectors

#### Pseudo-classes

links have a set of  *pseudo-classes*:

- `:hover`: (applies to any element, not just links).
- `:active`
- `:visited`

```css
.header-logo:hover,
.header-logo:active {
  opacity: 0.5;
}
```

#### first-child

#### Siblings

- the *adjacent sibling* `+`
- the *general sibling* `~`

### Positioning

`position: static`

`position: absolute`

`position: relative`

`position: fixed`

`z-index`

center an absolutely positioned object horizontally and vertically in a way that allows the object to be any size… and allows the wrapper to be any size:

```css
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
```

### Fixed header

It could look interesting to have a dark area around the whole site to frame the content.

```css
html {
  box-shadow: 0 0 0 30px #000 inset;
  padding: 0 30px;
}
```

## Page templates and frontmatter

### Template content

```html
<!DOCTYPE html>
<html>
  {% include head.html %}
  <body>
    {% include header.html %}

    {{ content }}

    {% include footer.html %}
  </body>
</html>
```

### There’s no place like home

```css
.full-hero {
  height: 100vh;
  background-color: #c7dbfc;
  background-size: cover;

}
.hero-home {
  background-image: url(/images/shark.jpg);
  background-position: center top;
}
```

### More advanced selectors

added a little downward-pointing arrow at the bottom of the hero to give people a hint they should scroll:

#### The :before/:after pseudo-element

```css
.full-hero:after {
  content: "﹀";
}
```

#### :before/:after CSS triangle

```css
.full-hero:after {
  border: 10px solid;
  border-color: #fff transparent transparent;
  content: "";
  height: 0;
  width: 0;
}
```

### Other pages, other folders

these days most modern sites have pages with nice-looking addresses like http://sitename.com/pagename, without the `.html` at the end .

## Specialty page layouts with flexbox

### Having content fill a container

the flex container is the HTML element with the CSS property `display: flex` set, and each flex item is a child element that has some value of the CSS `flex:` property set.

```css
body {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}
.content-container {
  flex-grow: 1;
}
```

The `flex-grow` property works by proportions: if all three items are set to `1`, each one takes up 1/3 of the space available.

### Vertical flex centering

![](/Users/huangxiaosheng/Documents/learn enough/images/align-center.png)

the `flex-basis` is a property that controls the original width of the element. The most common values are `0`, which sets the initial width to `0` and expands only as much as is needed to contain the content.

prevent the flex item from shrinking as the parent element gets smaller by setting the `flex-shrink` property to `0`.

### Flexbox shorthand

#### Flex container properties

flexbox supports a shorthand notation that follows this pattern:

```CSS
flex: <flex-grow> <flex-shrink> <flex-basis>
```

```css
flex: 1 1 0;
```

there is an even “shorterhand” way to write this

```css
flex: 1;
```

### A gallery stub

```
$ unzip gallery.zip -d images/
```

```css
cursor: pointer;
transition: all 0.5s ease-in-out;
```

## Adding a blog

### Adding blog posts

Jekyll blog posts are located in a directory called `_posts`, with filenames in the format `YYYY-MM-DD-post-title.md`.

#### Blog index structure

```css
order: 1;
```

after any elements that are in the same parent and have a lower number.

### Blog index content loop

```
{% for post in site.posts %}
  ...Liquid code...
{% endfor %}
```

- `{{ post.url }}`: This looks at the post’s filename and builds a URL to the post.
- `{{ post.date | date: '%B %d, %Y' }`: The date tag contains the post’s date as encoded in the filename or in the frontmatter.
- `{{ post.excerpt }}`: create an excerpt by pulling out the first paragraph.

```
{% for post in site.posts limit:5 %}
{% endfor %}
```

### A blog post page

```html
{{ page.postHero }}
```

```html
<a href="{{ site.posts.first.url }}">Newest Post</a>
```

## Mobile media queries

### Getting started with mobile designs

```css
@media (max-width: 800px) {
  
}
```

### Mobile adaptation

```css
white-space: nowrap;
```

### Mobile viewport

to install an *iOS simulator*, you need to [install Xcode](https://developer.apple.com/xcode/downloads/), start Xcode from the Applications folder, then select Xcode > Open Developer Tool > Simulator.

One alternative to using the iOS simulator is to view the site using the local Internet Protocol (IP) address.

the local IP can be found using the command-line program `ifconfig`:

```
$ ifconfig | grep 192
```

```
$ jekyll serve --host 0.0.0.0
```

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

### Mobile dropdown menu

- The `:checked` pseudo-class can be used to determine whether an `input type="checkbox"` has been checked or unchecked.
- The `for` attribute  of a `label` matches the id of a input.

| :checked   | Targets checkboxes that have been clicked by a user to add a checkmark |
| ---------- | ------------------------------------------------------------ |
| :disabled  | Targets inputs that have been set to `disabled` so that they don’t respond to user clicks |
| :enabled   | Targets inputs that are not disabled                         |
| :focus     | Targets an input that a user is actively interacting with, like when you are typing text in a text box |
| :invalid   | Targets inputs that have entries that are invalid (to draw a user’s attention to the element to fix their entry) |
| :read-only | Targets inputs that a user cannot write in, but in which they can click and select text |
| :valid     | Targets inputs that have valid data                          |

## Adding more little touches

### Custom fonts

#### Installing vector image fonts

One of the most popular sources of web fonts is called [Font Awesome](http://fontawesome.com/)

The first step is to head to the download page on the [Font Awesome site](http://fontawesome.io/get-started/). extract the ZIP file and then move it to a new `fonts` directory.

Next, open up `_includes/head.html` and include the fonts file:

```html
<link rel="stylesheet"
        href="/fonts/font-awesome-4.7.0/css/font-awesome.css">
```

```html
<i class="fa fa-facebook"></i>
```

#### Loading text fonts via CDN

head over to the [Google Fonts site](https://fonts.google.com/) and type “Raleway” in the search box. Then click the plus sign to select the font.

Next, search for “Open Sans” and then add this font. At the bottom of the screen, click on the black box that says “2 Families Selected”. Then click the “CUSTOMIZE”, and change the selected version of Raleway from the default `regular 400` to `thin 100`.

### Favicons

`.png` (for [Portable Network Graphics](https://en.wikipedia.org/wiki/Portable_Network_Graphics), pronounced “ping”).

The size on most browsers is 16px x 16px

```html
<link href="/favicon.png" rel="icon">
```

### Custom title and meta description

#### Custom title

```html
{% if page.title %}
  <title>{{ page.title }} | Test Page</title>
{% else %}
  <title>Test Page: Don't Panic</title>
{% endif %}
```

#### Custom descriptions

```html
{% if page.description %}
  <meta name="description" content="{{ page.description }}">
{% else %}
  <meta name="description" content="This is a dangerous site.">
{% endif %}
```