---
layout: page
title: Lectures
permalink: /lectures/
feature-img: "assets/img/pexels/basic.jpg"
---
{% for post in site.posts %}
 <article>
   <h2>
     <a href="{{ post.url }}">
       {{ post.title }}
     </a>
   </h2>
   <time datetime="{{ post.date | date: "%Y-%m-%d" }}">{{ post.date | date_to_long_string }}</time>
   <!-- Tag list -->
  {% capture tag_list %}{{ page.tags | join: "|"}}{% endcapture %}
  {% include tags_list.html tags=tag_list %}
 </article>
{% endfor %}
