## Hello, world!

### JS in a web browser

```javascript
alert("hello, world!");
```

### JS in a REPL

Read-Eval-Print Loop, or *REPL* (pronounced “repple”).

#### Browser console

```javascript
console.log("hello, world!");
```

#### Node prompt

```
$ brew install node
```

```
$ node
>
```

### JS in a file

```javascript
console.log("hello, world!", "how's it going?");
```

## Strings

### String basics

```
> "It's not easy being green"
'It\'s not easy being green'
```

`\t`

`\n`

### Concatenation and interpolation

JavaScript also supports multiline comments enclosed in `/* ... */`

```
> let firstName = "Michael";
> let lastName  = "Hartl";
> firstName + " " + lastName;
'Michael Hartl'
```

#### The backtick syntax

```
> `${firstName} ${lastName}`;
'Michael Hartl'
```

### Properties, booleans, and control flow

```
> "badger".length === 6;
true
```

```
> let password = "foo";
> if (password.length < 6) {
    "Password is too short.";
  }
  'Password is too short.'
```

#### Combining and inverting booleans

- `&&`
- `||` 
-  `!`

#### Bang bang

every JavaScript object has a value of either `true` or `false` in a boolean context. We can force JavaScript to use such a boolean context with `!!` .

### Methods

`toLowerCase()`

`toUpperCase()`

```
> let soliloquy = "To be, or not to be, that is the question:";
> soliloquy.includes("TO BE");
false
> soliloquy.includes("To be,", 1);
false
```

### String iteration

```javascript
for (let i = 0; i < soliloquy.length; i++) {
  console.log(soliloquy[i]);
}
```

## Arrays

### Splitting

```
> "badger".split("")
[ 'b', 'a', 'd', 'g', 'e', 'r' ]
```

### Array slicing

```
> a = [42, 8, 17, 99];
> a.slice(1);
[ 8, 17, 99 ]
> a.slice(1, 3);
[ 8, 17 ]
> a.slice(-1);
[ 99 ]
```

strings also support the `slice` method.

### More array methods

As with strings, arrays respond to an `includes` method

#### Sorting and reversing

```
> a.sort();
[ 17, 42, 8, 99 ]
> a;
[ 17, 42, 8, 99 ]
> a.reverse();
[ 99, 8, 42, 17 ]
> a;
[ 99, 8, 42, 17 ]
```

#### Pushing and popping

```
> a.push(6);
5
> a.pop();
6
```

#### Undoing a split

```
> a = ["ant", "bat", "cat", 42];
> a.join();
'ant,bat,cat,42'
> a.join("");
'antbatcat42'
```

### Array iteration

## Other native objects

### Math and Number

```
> 2/3;
0.6666666666666666
```

JavaScript has only one numerical type

#### More advanced operations

```
> Math.PI
3.141592653589793
> Math.pow(2, 3);
8
> Math.sqrt(-1)
NaN
> Math.cos(2*Math.PI)
1
> Math.E;
2.718281828459045
> Math.log(10);
2.302585092994046
> Math.log10(10);
1
```

#### Math to string

```
> 100.0.toString()
'100'
> String(100.0);
'100.0'
> Number('1.24e6')
1240000
```

### Dates

```
> let now = new Date();
> now
2019-07-26T17:15:31.315Z
> let moonLanding = new Date("July 20, 1969 20:18");
> now - moonLanding;
1578373051315	// milliseconds
> now.getFullYear();
2018
> now.getMonth();
6
> now.getDay();
6
> const daysOfTheWeek = ["Sunday", "Monday", "Tuesday", "Wednesday",
                       "Thursday", "Friday", "Saturday"];
> daysOfTheWeek[now.getDay()];
'Saturday'
```

### Regular expressions

as programmer [Jamie Zawinski](https://en.wikipedia.org/wiki/Jamie_Zawinski) [famously said](https://blog.codinghorror.com/regular-expressions-now-you-have-two-problems/):

> Some people, when confronted with a problem, think “I know, I’ll use regular expressions.” Now they have two problems.

```
> let zipCode = /\d{5}/;
> let s = "Beverly Hills 90210 was a '90s TV show set in Los Angeles.";
> s += " 91125 is another ZIP code in the Los Angeles area."
> s.match(zipCode);
[ '90210',
  index: 14,
  input: 'Beverly Hills 90210 was a \'90s TV show set in Los Angeles. 91125 is another ZIP code in the Los Angeles area.' ]
> zipCode = /\d{5}/g; 
> s.match(zipCode);
[ '90210', '91125' ]
> "ant    bat\tcat\nduck".split(/\s+/);
[ 'ant', 'bat', 'cat', 'duck' ]
```

### Plain objects

```
> let user = {};
> user["firstName"] = "Michael"; 
```

#### Map

Native JavaScript objects do have their weaknesses, such as slower performance and limited support for extracting keys and values. 

```
> let uniques = new Map();
> uniques.set("loved", 0);
Map { 'loved' => 0 }
> let currentValue = uniques.get("loved");
```

## Functions

### Function definitions

```javascript
function stringMessage(string) {
    if (string) {
      return "The string is nonempty.";
    } else {
      return "It's an empty string!";
    }
  }
```

#### Sorting numerical arrays

```javascript
a.sort((a, b) => a - b);
```

#### Fat arrow

```javascript
let altStringMessage = (string) => {
  if (string) {
    return "The string is nonempty.";
  } else {
    return "It's an empty string!";
  }
}
```

### Method chaining

```
> .load palindrome.js
```

### Iteration for each

```javascript
array.forEach((element) => {
  console.log(element);
});
```

## Functional programming

### Map

```javascript
let states = ["Kansas", "Nebraska", "North Dakota", "South Dakota"];

// Returns a URL-friendly version of a string.
//   Example: "North Dakota" -> "north-dakota"
function urlify(string) {
  return string.toLowerCase().split(/\s+/).join("-");
}

// urls: Imperative version
function imperativeUrls(elements) {
  let urls = [];
  elements.forEach(function(element) {
    urls.push(urlify(element));
  });
  return urls;
}

// urls: Functional version
function functionalUrls(elements) {
  return elements.map(element => urlify(element));
}
```

### Filter

```
> [1, 2, 3, 4, 5, 6, 7, 8].filter(n => n % 2 === 0);
[ 2, 4, 6, 8 ]
```

### Reduce

```javascript
let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
numbers.reduce((total, n) => total += n);
```

```javascript
states.reduce((lengths, state) => {
  lengths[state] = state.length;
  return lengths;
}, {});
```

## Objects and prototypes

### Defining objects

```javascript
function Phrase(content) {
    this.content = content;
  }
```

### Prototypes

```javascript
TranslatedPhrase.prototype = new Phrase();
```

### Modifying native objects

each emoji is effectively represented as two separate characters

```javascript
String.prototype.reverse = () => {
  return Array.from(this).reverse().join("");
}
```

## Testing and test-driven development

### Testing setup

Mocha is a powerful testing framework 

```
$ npm install --global mocha
```

 configure `palindrome.js` as an NPM module 

```
$ cd ~/repos/
$ mkdir palindrome
$ cd palindrome
$ cp ~/repos/js_tutorial/palindrome.js index.js
```

To get us started with a new module, the `npm` program comes with a helpful command called `npm init`

```
$ npm init
package name: (xiaosheng-huang-palindrome)
version: (0.1.0)
description: Palindrome detector
entry point: (index.js)
test command: mocha
git repository: https://github.com/Xiaosheng-Huang/xiaosheng-huang-palindrome
keywords: palindrome learn-enough javascript
author: Xiaosheng Huang
license: (ISC)
```

Create a file with the required name `readme.md` 

~~~markdown
# Phrase object (with palindrome detector)

This is a sample NPM module created in [*Learn Enough JavaScript to Be Dangerous*](https://www.learnenough.com/javascript-tutorial) by Michael Hartl.

The module can be used as follows:

```
$ npm install --global xiaosheng-huang-palindrome
$ vim test.js
let Phrase = require("mhartl-palindrome");
let napoleonsLament = new Phrase("Able was I, ere I saw Elba.");
console.log(napoleonsLament.palindrome());
$ node test.js
true
```
~~~

### Initial test coverage

```
$ mkdir test/
$ touch test/test.js
```

including two NPM modules in `test.js`

```javascript
let assert = require("assert");
let Phrase = require("../index.js");

describe("Phrase", function() {

  describe("#palindrome", function() {

    it("should return false for a non-palindrome", function() {
      let nonPalindrome = new Phrase("apple");
      assert(!nonPalindrome.palindrome());
    });

    it("should return true for a plain palindrome", function() {
      let plainPalindrome = new Phrase("racecar");
      assert(plainPalindrome.palindrome());
    });
  });
});
```

```
$ npm test
```

#### Pending tests

```javascript
it("should return true for a mixed-case palindrome");
```

```javascript
describe("#letters", function() {
  it("should return only letters", function() {
    let punctuatedPalindrome = new Phrase("Madam, I'm Adam.");
    assert.strictEqual(punctuatedPalindrome.letters(), "MadamImAdam");
  });
  
  it("should return the empty string on no match", function() {
      let noLetters = new Phrase("1234.56");
      assert.strictEqual(noLetters.letters(), "");
    });
});
```

### Refactor

```javascript
module.exports = Phrase;

String.prototype.reverse = function() {
  return Array.from(this).reverse().join("");
}

// Defines a Phrase object.
function Phrase(content) {
  this.content = content;

  // Returns the letters in the content.
  // For example:
  //   new Phrase("Hello, world!").letters() === "Helloworld"
  this.letters = function letters() {
    return (this.content.match(/[a-z]/gi) || []).join("");
  }
  
  this.processedContent = function() {
    return this.letters().toLowerCase();
  }

  // Returns true if the phrase is a palindrome, false otherwise.
  this.palindrome = function() {
    let content = this.processedContent()
    return content === content.reverse();
  }
}
```

#### Publishing the NPM module

```
$ git add -A
$ git commit -m "Finish working and refactored palindrome method"
$ git push
$ npm adduser Xiaosheng Huang
Username: xiaosheng-huang
Password: 7317motorola
Email: (this IS public) Xiaosheng-Huang@outlook.com
```

NPM requires that you verify your email address before allowing you to publish

```
$ npm publish
```

For any future revisions, you can simply increment the version number in `package.json`

## Events and DOM manipulation

### A working palindrome page

```
$ npm install <username>-palindrome   
```

browsers don’t support `require`

```
$ npm install --global browserify
$ browserify main.js -o bundle.js
```

 [watchify](https://www.npmjs.com/package/watchify) package is designed to re-build the bundled version automatically.

```html
<script src="bundle.js"></script>
```

```javascript
let string = prompt("Please enter a string for palindrome testing:");
```

the Jekyll static site builder causes errors when processing Node modules

```
$ touch .nojekyll
```

### Event listeners

```html
<button id="palindromeTester">Is it a palindrome?</button>
```

```javascript
document.addEventListener("DOMContentLoaded", function() {
  let button = document.querySelector("#palindromeTester");
  button.addEventListener("click", palindromeTester);
  });
});
```

```html
<form id="palindromeTester">
  <button type="submit">Is it a palindrome?</button>
</form>
```

```javascript
document.addEventListener("DOMContentLoaded", function() {
  let form = document.querySelector("#palindromeTester");
  form.addEventListener("submit", function() {
    palindromeTester();
  });
});
```

### Dynamic HTML

```html
<h2>Result</h2>

<p id="palindromeResult"></p>
```

```javascript
let palindromeResult = document.querySelector("#palindromeResult");
if (phrase.palindrome()) {
    palindromeResult.innerHTML = `"${phrase.content}" is a palindrome!`;
  } else {
    palindromeResult.innerHTML = `"${phrase.content}" is not a palindrome.`;
  }
```

### Form handling

```html
<form id="palindromeTester">
  <textarea name="phrase" rows="10" cols="30"></textarea>
  <br>
  <button type="submit">Is it a palindrome?</button>
</form>
```

```javascript
function palindromeTester(event) {
  event.preventDefault();
  let phrase = new Phrase(event.target.phrase.value);
  .
  .
  .
}

let tester = document.querySelector("#palindromeTester");
tester.addEventListener("submit", function(event) {
	palindromeTester(event);
});
```

```
$ npm update <username>-palindrome	# or npm install <username>-palindrome
```

## Shell scripts with Node.js

### Reading from files

```
$ npm install --global fs
```

```javascript
let fs = require("fs");
let text = fs.readFileSync("phrases.txt", "utf-8");
```

### Reading from URLs

```
$ npm install --global request
```

```javascript
let request = require("request");
let Phrase = require("<username>-palindrome");
let url = 'https://cdn.learnenough.com/phrases.txt'

request(url, function(error, response, body) {
  body.split("\n").forEach(function(line) {
    phrase = new Phrase(line);
    if (phrase.palindrome()) {
      console.log("palindrome detected:", line);
    }
  });
});
```

### DOM manipulation at the command line

```
$ npm install jsdom
```

```javascript
#!/usr/local/bin/node

// Returns the paragraphs from a Wikipedia link, stripped of reference numbers.

let request = require("request");
let url = process.argv[2];

const jsdom = require("jsdom");
const { JSDOM } = jsdom;

request(url, function(error, response, body) {
  // Simulate a Document Object Model.
  let { document } = (new JSDOM(body)).window;

  // Grab all the paragraphs and references.
  let paragraphs = document.querySelectorAll("p");
  let references = document.querySelectorAll(".reference");

  // Remove any references.
  references.forEach(function(reference) {
    reference.remove();
  });

  // Print out all of the paragraphs.
  paragraphs.forEach(function(paragraph) {
    console.log(paragraph.textContent);
  });
});
```

automatically copies the results to the macOS **p**aste**b**oard (also called the “clipboard”):

```
$ ./wikp https://es.wikipedia.org/wiki/JavaScript | pbcopy
```

## Full sample app: Image gallery

to  make a personal copy of the app, you can do using the *fork* capability at GitHub

`data-foo-bar-baz` on HTML element `object` corresponds to the variable `object.dataset.fooBarBaz`

```javascript
function activateGallery() {
  let thumbnails = document.querySelectorAll("#gallery-thumbs > div > img");
  let mainImage  = document.querySelector("#gallery-photo img");
  let currentClass = "current";
  let galleryInfo = document.querySelector("#gallery-info");
  let title       = galleryInfo.querySelector(".title");
  let description = galleryInfo.querySelector(".description");

  thumbnails.forEach(function(thumbnail) {
    // Preload large images.
    let newImageSrc = thumbnail.dataset.largeVersion;
    let largeVersion = new Image();
    largeVersion.src = newImageSrc;
    nnn
    thumbnail.addEventListener("click", function() {
      mainImage.setAttribute("src", newImageSrc);
      mainImage.setAttribute("alt", thumbnail.alt);
      
      document.querySelector(".current").classList.remove(currentClass);
      thumbnail.parentNode.classList.add(currentClass);
      
      title.innerHTML       = thumbnail.dataset.title;
      description.innerHTML = thumbnail.dataset.description;
    });
  });
}
```

### Changing the image info

