---
layout: post
title: Web Development Basics
tags: [HTML, CSS, JS]
excerpt_separator: <!--more-->
---
[toc]

### Introduction

This is the bread and butter of the frontend.

## HTML

Stands for **H**yper**t**ext **M**arkup **L**anguage

Gives structure to the website.

### Basic Structure

HTML utilizes tags to format the content of websites. Tags are denoted by angle brackets ("< >").

Almost every website will use `<html>, <head>, <body> ...`

```html
<html>
    <head>  
        <!-- Put Metadata here -->
    	<title> My First Website </title>
    </head>

    <body>
        <p>
            <!-- Put Structural Elements here -->
            Hello, World!
        </p>
    </body>
</html>
```

**Tags:**

### Basic Webpage

```html
<html>
    <head>    
    	<title> My First Website</title>
    </head>

    <body>
    	<div>
    	<h1> Welcome </h1>
        `	<p>
            	Hello, World! <br>
        	</p>
        </div>
        <img src = "https://mbhs-devclub.github.io/assets/img/noText.png">
        <a href = "https://mbhs-devclub.github.io/"> Club Website </a>

    </body>
</html>
```

**Tags Explained:**

* `<h1>`: This is a **header** tag. Sizes range from `<h1> to <h6>`
* `<p>` **Paragraph** tag. Used for displaying text.
* `<img>` **Image** tag.
* `<a>` **Anchor** tag. Used for links to other places. Use HREF.
* `<div>` **Division** tag. Defines a block of content for organization, but does not add any semantic value.

## CSS

Shorthand for **Cascading Styles Sheets**. Used for styling webpages.

Example CSS:

```css
body {
    font-size: 14px;
    color: navy;
}
```

Whereas HTML has **tags**, CSS has **selectors**.

The word `body` refers to the selector of all HTML body tags. In CSS, the attributes are applied recursively.

The text `font-size: 14px` represents a property value pair.

Examples of properties include:

```
color: Tomato; /* Text color */
background-color: lightblue; /* Background color */
border-style: dotted; /* Creates a dotted border*/
margin-top: 50px; /* Positions the element*/
padding-top: 20px; /* Inserts padding for an element */
height: 200px; /* Defines the boundary of the element */
```

### Integration

There are three ways to integrate CSS into HTML.

**Inline Styling**

```
<p style="color: red">text</p>
```

* Convenient
* But, use sparingly

**Internal Styling**

```
<html>
    <head>    
    	<title> My First Website</title>    
        <style>
        	p {
            	color: red;
        	}
    	</style>
    </head>
    ...    
</html>
```

* Apply CSS in the same HTML file
* Convenient for development

**External Styling**

main.css

```
p {
    color: red;
}

a {
    color: blue;
}
```

index.html

```
<html>
<head>
    <title>CSS Playground!</title>
    <link rel="stylesheet" href="style.css">
...
```

* Organized and Modular
* Useful if website is large and has many parts

## JavaScript

JS is your source of proccessing. Within JavaScript, you may manage your website in the backend. The "Brain" of your website, JavaScript can modify the outside with sparkly commands and even machine learning. JavaScript is used by pretty much everyone and is super popular. It may not be an amazing piece of software that can do anything and it may be vulnerable to attacks, but JavaScript, like English, is a universal language.

There are two main types of JavaScript programming. One is the inner processing (i.e. changing variables, loops, basic programming), and the other is it's interaction with the "outside world" (i.e. getting a field name, changing css (color and stuff), changing text). First we're going to show you some basic back end, then we'll show you how to make that manipulation useful, and then we'll keep on learning both of these.

#### Where to Write Your JavaScript
There are three options for where to write your JavaScript. The first is to write it directly in your HTML formatting:
```
<button type="button" onclick="document.getElementById('demo').innerHTML = Date()">Click me to display Date.</button>
```
The second is to write it in your script
```
<script>
// Create and display a variable:
var animal = "Dog";
document.getElementById("demo").innerHTML = animal;
</script>
```
And lastly, you can reference an external JavaScript file

#### Basic Brainy Javascript

Here are the basic data types you should know for now
```
var k = 1;                               // Number
var name = "Itamar";                      // String
var x = {firstName:"Itamar", lastName:"Fiorino"};    // Object
```

Creating and modifying variables (notice the semicolons):
```
var a, b, c;    // Creating 3 variables with "null" values (could be numbers or strings for all JavaScript cares
a = 1;          // Sets a to 1
b = 2;          // Sets b to 2
z = x + y;      // After this statement, C will equal 3
```

Functions can return values (ask us if this confuses you) or can just do things to output:
```
function f(p1, p2) {
    return p1 * p2;              // The function returns the product of p1 and p2
}
console.log(f(2,3))        //will display 6 into the console
```

Some more basic commands:  

Keyword	| Description
---	|---
break	| 	Terminates a switch or a loop
continue	| 	Jumps out of a loop and starts at the top
debugger	| 	Stops the execution of JavaScript, and calls (if available) the debugging function
do ... while	| 	Executes a block of statements, and repeats the block, while a condition is true
for	| 	Marks a block of statements to be executed, as long as a condition is true
function	| 	Declares a function
if ... else	| 	Marks a block of statements to be executed, depending on a condition
return	| 	Exits a function
switch	| 	Marks a block of statements to be executed, depending on different cases
try ... catch	| 	Implements error handling to a block of statements
var	| 	Declares a variable

#### Basic Functional Javascript

JavaScript can "display" data in different ways:

' Writing into an HTML element, using innerHTML.
' Writing into the HTML output using document.write().
' Writing into an alert box, using window.alert().
' Writing into the browser console, using console.log().

Try out these code snippets:
```
var animals = ["cat", "dog", "mouse"];
document.getElementById("demo").innerHTML = fruits;

function function() {
    animals.sort();
    document.getElementById("demo").innerHTML = fruits;
}
```
To run "function" in an HTML file, just call your function "function" which will modify the text within a \<p\> with id="demo"

Try testing out different functions and get some JS exercise, then you can start learning JQuery, JSON, AJAX, Node.JS, Jekyll, and more. W3Schools is an **Excellent** source of information
