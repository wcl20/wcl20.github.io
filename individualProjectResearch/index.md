---
layout: default
---
## Individual Project Research
<div class="list-navigation">
	<ul>
		{% for item in site.data.individualProjectResearch %}
			<li><a href="{{ item.link }}">{{ item.title }}</a></li>
		{% endfor %}
	</ul>
</div>