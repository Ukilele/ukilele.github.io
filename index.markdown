---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
background: '/assets/titleimage.jpg'
---

<ul style="list-style-type: none;">
  {% for post in site.posts %}
    <li>
      <h2><a href="{{ post.url }}">{{ post.title }}</a></h2>
      {{ post.excerpt.split("</h1>")[1] }}
    </li>
  {% endfor %}
</ul>
