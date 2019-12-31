---
layout: default
---
<h1>{{ page.title }}</h1>
{{ content }}
<div class="page-navigation">
<div>{% if page.prev %}<a href="{{ page.prev-url }}">&#8249; {{ page.prev }}</a>{% endif %}</div>
<div>{% if page.next %}<a href="{{ page.next-url }}">{{ page.next }} &#8250;</a>{% endif %}</div>
</div>