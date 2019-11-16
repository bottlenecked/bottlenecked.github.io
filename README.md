# Bottlenecked's blog
This is my personal blog. Opinions expressed herein are mine and not shared by my employer. Enjoy!

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }} ({{post.date | date: '%m/%Y'}})</a>
    </li>
  {% endfor %}
</ul>
