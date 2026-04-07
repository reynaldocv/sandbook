---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---
This is the index.md

<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>


{% assign posts_by_folder = site.posts | group_by: "categories" %}

{% for folder in posts_by_folder %}
  <h3>Folder: {{ folder[0]}}</h3>
  <ul>
    {% for post in folder.items %}
      <li>{{ post.title }}</li>
    {% endfor %}
  </ul>
{% endfor %}

{% assign folder_list = "" | split: "," %}
{% for post in site.posts %}
  {% comment %} Get path relative to _posts {% endcomment %}
  {% assign path_parts = post.path | split: "/" %}
  {% if path_parts[0] == "_posts" and path_parts.size > 2 %}
    {% assign subfolder = path_parts[1] %}
    {% unless folder_list contains subfolder %}
      {% assign folder_list = folder_list | push: subfolder %}
    {% endunless %}
  {% endif %}
{% endfor %}

<ul>
  {% for folder in folder_list %}
    <li>{{ folder }}</li>
  {% endfor %}
</ul>


{% comment %} 1. Gather unique subfolder names from _posts {% endcomment %}
{% assign folders = "" | split: "" %}
{% for post in site.posts %}
  {% if post.path contains '_posts/' %}
    {% assign path_parts = post.path | split: '_posts/' | last | split: '/' %}
    {% if path_parts.size > 1 %}
      {% assign folder_name = path_parts.first %}
      {% unless folders contains folder_name %}
        {% assign folders = folders | push: folder_name %}
      {% endunless %}
    {% endif %}
  {% endif %}
{% endfor %}

{% comment %} 2. Sort folders based on the second word in the name {% endcomment %}
{% assign sorted_folders = folders | sort %} 
{% comment %} Note: Liquid sort is alphabetical. For complex second-word sorting,
you may need to create a custom sort key via a jekyll plugin or 
re-structure folder names to include the sort key first. {% endcomment %}

<ul>
{% for folder in sorted_folders | sort by name_parts %}
  {% assign name_parts = folder | split: ' ' %}
  <li>{{ folder }} (Sorted by: {{ name_parts[1] }})</li>
{% endfor %}
</ul>