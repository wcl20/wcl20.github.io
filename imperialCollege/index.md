---
layout: default
---
## Imperial College London
<div class="download-list">
	{% for item in site.data.imperialCollege %}
		<h3>{{ item.year }}</h3>
		<ul>
			{% for subject in item.subjects %}
				<li>
					<p>{{ subject.title }}</p>
					{% if subject.link %}<a href="{{ site.url }}{{ subject.link }}" target="_blank"><i class="fa fa-download"></i></a>{% endif %}
				</li>
			{% endfor %}
		</ul>
	{% endfor %}
</div>