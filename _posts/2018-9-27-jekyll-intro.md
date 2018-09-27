---
layout: post
title: Jekyll Intro
tags: [Jekyll, YAML]
excerpt_separator: <!--more-->
---

# Jekyll and its Mysteries

## Installing Jekyll

#### MacOS
```
xcode-select --install
ruby -v
gem install bundler jekyll
```


#### Windows
*Start by opening command prompt as admin.*

```
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1 && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"
choco install ruby -y
gem install bundler
gem install jekyll
```
If you recieve an SSL error, you will need install Ruby manually by going [here](https://rubyinstaller.org/downloads/).


## What is Jekyll?
"*Transform your plain text into static websites and blogs*."
![](https://cdn.worldvectorlogo.com/logos/jekyll.svg)
Jekyll is a static site generator. Let's headover to their [site](https://jekyllrb.com/) to discuss more. Basically makes creating any static website super simple.

## Get Started
When building your site the first thing that you want to do is to create a directory to make a project.

`jekyll new my_directory_name`

From there we can go into our directory and host our website —locally of course.
`jeykll serve`

This will be hosted at [localhost:4000](localhost:4000) as default.


## Editing Our Jekyll Site
Start of with the index.md file. This is the generic home file and will be important later. 

You will notice the format that Jekyll uses has a header and content. 
```
---
header
---
content
```
The header will have all the information relating to that specific page. This includes layout, title, date, categories, tags, and your custom variables.

#### Editing your home page.
Change the layout to `default` in order to add your own. Now in the section below you are able to add your own contention.
Try adding some text. `jekyll serve` your site and view your content.

#### Quick guide to Markdown.
*impromptu*

#### Creating Posts
*impromptu* 

#### Creating New Pages
*impromptu* 

#### Use Gem Themes
*impromptu* 

#### Download and Use Themes
Start by heading over to [jekyllthemes]()(http://jekyllthemes.org). From there choose a theme that you a partial too and download the theme you want to use. 

#### Organizing Many Pages
To organize many pages add `include: ['_pages']` to your config.yml page. 

## Jekyll Tools

Jekyll comes with several tools for organization, such as creating templates.

### Front Matter (YAML)

Stands for YAML Ain't Markup Language.

Really nice way to list out data.

```yaml
---
my_number: 5
title: Home
---
...
```

Jekyll provides a quick way to access these variables as `page.my_number` or `page.title`

### Liquid

Manipulate content, along with YAML.

**Object**

```html
<h1> {{page.title}} </h1>
```

**Tags**

```
{% if page.show_sidebar %}
```

**Filters**

```
<h1> {{"Hello, World" |}}
```
### Jekyll Layouts

Checkout the `_layouts` directory. If it is not there, create one.

Create a new file named `default.html`.

```
<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <title>{{ page.title }}</title>
  </head>
  <body>
    {{ content }}
  </body>
</html>
```

Then, edit the main file, `index.html`

```html
---
layout: default
title: Home
---
<h1>{{ "Hello World!" | downcase }}</h1>
```

Now, checkout <http://localhost:4000/about.html> 

### Example: About Page 

Create the file `about.md` in the project root.
```
---
layout: default
title: About
---
# About page

```
## Advanced Usage
Loop through posts:
```
{% for post in site.posts %}
<div class="row">
	<div class="small-12 columns">
  	
		<sub>{{ post.date | date: '%B %d, %Y' }}</sub>
		<a href="{{ post.url }}"><h3>{{ post.title }}</h3></a>

	  	{{ post.excerpt }}

		<ul class="inline-list" style="margin-top:-1em;">
			{% for category in post.categories %}
			<li><h6><a href="/#!/{{ category }}"><i class="fa fa-tag"></i> {{ category }}</a></h6></li>
			{% endfor %}
		</ul>

	</div>
</div>
{% endfor %}
```

Loop through categories:
```
{% for category in site.categories %}
   <div class="catbloc" id="{{ category | first | remove:' ' }}">
        <h2>{{ category | first }}</h2>

        <ul>
           {% for posts in category %}
             {% for post in posts %}
               {% if post.url %}
                <li>
                  <a href="{{ post.url }}">
                    <time>{{ post.date | date: "%-d %B %Y" }}</time>
                    {{ post.title }}
                  </a>
                </li>
              {% endif %}
            {% endfor %}
          {% endfor %}
       </ul>
   </div>
{% endfor %}
```


## Jekyll File Structure
```
.
├── _config.yml
├── _data
|   └── members.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.md
|   └── on-simplicity-in-technology.md
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.md
|   └── 2009-04-26-barcamp-boston-4-roundup.md
├── _sass
|   ├── _base.scss
|   └── _layout.scss
├── _site
└── index.html # can also be an 'index.md' with valid front matter
```

* Config.yml : Basic Configs. Makes life easier.
* _drafts : a place to put unpublished posts.
    * Naming Convention: Just the title
* _includes : partials you could include in code
    * `{% include file.ext %}` -> `_includes/file.ext`
* _layouts : where to put the layouts specified by front matter
* _posts : where your dynamic content goes, where the webpages you write goes
* _data : well formatted data
    * `site.data.filename` references `filename.yml`
* _sass : where your sass partials goes
* _site : the site that is generated from jekyll
