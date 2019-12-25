---
layout: default
---
## Welcome to My Blog
<div class="block-navigation">
	{% assign rows = site.data.navigation.size | divided_by: 2.0 | ceil %}
	{% for i in (1..rows) %}
		{% assign offset = forloop.index0 | times: 2 %}
		<div class="row">
			{% for item in site.data.navigation limit:2 offset: offset %}
				<a href="{{ item.link }}" class="nav">
					<p>{{ item.title }}</p>
				</a>
			{% endfor %}
		</div>
	{% endfor %}
</div>
