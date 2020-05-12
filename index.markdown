---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults
background: '/assets/titleimage.jpg'
---


  {% for post in site.posts %}
    <p>
      <h2><a href="{{ post.url }}">{{ post.excerpt }}</a></h2>
    </p>
  {% endfor %}

