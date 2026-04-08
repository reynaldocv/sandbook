---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---


<div class="w3-row w3-grayscale">
{% for folder in folders %}      
    <div class="w3-col l4 s12">
        <div class="w3-container w3-whitesmoke">
        <img src="{{site.baseurl}}/assets/images/{{folder}}.png" style="width:100%">          
        <strong>{{ folder }}</strong>
      {% assign count = 0 %}
      {% for post in all_posts %}
        {% if post.path contains folder and count < 3 %}   
          <li>{{ post.date | date: "%m" }} - {{ post.date | date: "%d" }}  <a href="{{ site.baseurl }}{{post.url}}">{{ post.title }}</a></li>
                 {% assign count = count | plus: 1 %}
        {% endif %}
      {% endfor %}
     </div>    
       </div>
{% endfor %}
</div>