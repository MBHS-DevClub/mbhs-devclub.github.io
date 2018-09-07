---
layout: post
title: Welcome
tags: [Markdown]
excerpt_separator: <!--more-->
---
* TOC
{:toc}

# Welcome to A Lecture

Well this is not really a lecture. More of an intro to how the lectures on the site work; they use Markdown. Well... Kramdown converts the Markdown *actually never mind*.

Markdown let's us do all this:


Jekyll supports the use of [Markdown](http://daringfireball.net/projects/markdown/syntax) with inline HTML tags which makes it easier to quickly write posts with Jekyll, without having to worry too much about text formatting. A sample of the formatting follows.

Tables have also been extended from Markdown:

First Header  | Second Header
------------- | -------------
Content Cell  | Content Cell
Content Cell  | Content Cell

Here's an example of an image, which is included using Markdown:

![Image of a glass on a book]({{ site.baseurl }}/assets/img/pexels/book-glass.jpeg)

Highlighting for code in Jekyll is done using Base16 or Rouge. This theme makes use of Rouge by default.

{% highlight js %}
// count to ten
for (var i = 1; i <= 10; i++) {
    console.log(i);
}

// count to twenty
var j = 0;
while (j < 20) {
    j++;
    console.log(j);
}
{% endhighlight %}

Type on Strap uses KaTeX to display maths. Equations such as $$S_n = a \times \frac{1-r^n}{1-r}$$ can be displayed inline.

Alternatively, they can be shown on a new line:

$$ f(x) = \int \frac{2x^2+4x+6}{x-2} $$


From Michael's Rose [Minimal Mistakes](https://mmistakes.github.io/minimal-mistakes/markup-syntax-highlighting).
Syntax highlighting is a feature that displays source code, in different colors and fonts according to the category of terms. This feature facilitates writing in a structured language such as a programming language or a markup language as both structures and syntax errors are visually distinct. [Highlighting](http://en.wikipedia.org/wiki/Syntax_highlighting) does not affect the meaning of the text itself; it is intended only for human readers.


### GFM Code Blocks

GitHub Flavored Markdown [fenced code blocks](https://help.github.com/articles/creating-and-highlighting-code-blocks/) are supported.

```css
#container {
  float: left;
  margin: 0 -240px 0 0;
  width: 100%;
}
```

{% highlight scss linenos %}
.highlight {
  margin: 0;
  padding: 1em;
  font-family: $monospace;
  font-size: $type-size-7;
  line-height: 1.8;
}
{% endhighlight %}

```html
{% raw %}<nav class="pagination" role="navigation">
  {% if page.previous %}
    <a href="{{ site.url }}{{ page.previous.url }}" class="btn" title="{{ page.previous.title }}">Previous article</a>
  {% endif %}
  {% if page.next %}
    <a href="{{ site.url }}{{ page.next.url }}" class="btn" title="{{ page.next.title }}">Next article</a>
  {% endif %}
</nav><!-- /.pagination -->{% endraw %}
```

```ruby
module Jekyll
  class TagIndex < Page
    def initialize(site, base, dir, tag)
      @site = site
      @base = base
      @dir = dir
      @name = 'index.html'
      self.process(@name)
      self.read_yaml(File.join(base, '_layouts'), 'tag_index.html')
      self.data['tag'] = tag
      tag_title_prefix = site.config['tag_title_prefix'] || 'Tagged: '
      tag_title_suffix = site.config['tag_title_suffix'] || '&#8211;'
      self.data['title'] = "#{tag_title_prefix}#{tag}"
      self.data['description'] = "An archive of posts tagged #{tag}."
    end
  end
end
```

### Code Blocks in Lists

Indentation matters. Be sure the indent of the code block aligns with the first non-space character after the list item marker (e.g., `1.`). Usually this will mean indenting 3 spaces instead of 4.

1. Do step 1.
2. Now do this:

   ```ruby
   def print_hi(name)
     puts "Hi, #{name}"
   end
   print_hi('Tom')
   #=> prints 'Hi, Tom' to STDOUT.
   ```

3. Now you can do this.

### GitHub Gist Embed

An example of a Gist embed below.

<script src="https://gist.github.com/mmistakes/77c68fbb07731a456805a7b473f47841.js"></script>
