---
layout: default 
---

<div class="page-header">
    <h1>{{ page.title }} {% if page.tagline %} <small>{{ page.tagline }}</small>{% endif %}</h1>
</div>

<ul class="tag_box inline">
    {% assign tags_list = site.tags %}  

    {% if tags_list.first[0] == null %}
        {% for tag in tags_list %} 
        <li><a href="#{{ tag }}-ref">{{ tag }} <span>{{ site.tags[tag].size }}</span></a></li>
        {% endfor %}
    {% else %}
        {% for tag in tags_list %} 
        <li><a href="#{{ tag[0] }}-ref">{{ tag[0] }} <span>{{ tag[1].size }}</span></a></li>
        {% endfor %}
    {% endif %}

    {% assign tags_list = nil %}
</ul>

{% for tag in site.tags %} 
<h2 id="{{ tag[0] }}-ref">{{ tag[0] }}</h2>
<ul class="index">
    {% assign pages_list = tag[1] %}  

    {% if site.JB.pages_list.provider == "custom" %}
        {% include custom/pages_list %}
    {% else %}
        {% for node in pages_list %}
            {% if node.title != null %}
                {% if group == null or group == node.group %}
                    {% if page.url == node.url %}
                    <li class="active">
                        <a href="{{ site.baseurl }}{{ node.url }}" class="active">{{ node.title | xml_escape }}</a>
                        <span><time datetime="{{ node.date | date: "%Y-%m-%d" }}">{{ node.date | date: "%Y/%m/%d" }}</time></span>
                    </li>
                    {% else %}
                    <li>
                        <a href="{{ site.baseurl }}{{ node.url }}" class="active">{{ node.title | xml_escape }}</a>
                        <span><time datetime="{{ node.date | date: "%Y-%m-%d" }}">{{ node.date | date: "%Y/%m/%d" }}</time></span>
                    </li>
                    {% endif %}
                {% endif %}
            {% endif %}
        {% endfor %}
    {% endif %}

    {% assign pages_list = nil %}
    {% assign group = nil %}   
</ul>
{% endfor %}
