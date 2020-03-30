---
layout: default
---
## Algorithms
<div class="list-navigation">
	{% for item in site.data.algorithms %}
		<h3>{{ item.category }}</h3>
		<ul>
			{% for problem in item.problems %}
				<li><a href="{{ problem.link }}">{{ problem.title }}</a></li>
			{% endfor %}
		</ul>
	{% endfor %}
</div>
