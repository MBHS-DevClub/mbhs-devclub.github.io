# Web Development

### Introduction

This is the bread and butter of websites.

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

### Integration

There are three ways to integrate CSS into HTML. 

**Inline Styling**

```HTML
<p style="color: red">text</p>
```

* Convenient
* But, use sparingly

**Internal Styling**

```HTML
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

```CSS
p {
    color: red;
}

a {
    color: blue;
}
```

index.html

```HTML
<html>
<head>
    <title>CSS Playground!</title>
    <link rel="stylesheet" href="style.css">
...
```

* Organized and Modular
* Useful if website is large and has many parts

## JS

Give your webpage some sparkle!

