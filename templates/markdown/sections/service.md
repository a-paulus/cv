{% extends "section.md" %}

{% block body %}
<table class="table table-hover">
{% for item in items.main %}
<tr>
  <td style='padding-right:0;'>
  <span class='cvdate'>{{ item.year }}</span>
  {% if item.url %}
     <a href="{{ item.url }}">{{ item.details }}</a>
  {% else %}
      {{item.details }}
  {% endif %}
  {% if item.sub_details %}
  <br><p style="color:grey;font-size:1.2rem">{{ item.sub_details }}</p>
  {% endif %}
  </td>
</tr>
{% endfor %}
</table>

### Invited Talks
<table class="table table-hover">
{% for item in items.talks %}
<tr>
  <td align='right' style='padding-right:0;padding-left:0;'>{{ loop.index }}.</td>
  <td style='padding-right:0;'>
    <span class='cvdate'>{{ item.year }}</span>
    {% if item.url %}
     <a href="{{ item.url }}"><em>{{ item.title }}</em></a> &mdash;
    {% else %}
     <em>{{ item.title }}</em> &mdash;
    {% endif %}
    {% if item.location_url %}
        <a href="{{ item.location_url }}">{{ item.location }}</a>
    {% else %}
        {{ item.location }}
    {% endif %}
  </td>
</tr>
{% endfor %}
</table>

### Reviewing
<table class="table table-hover">
{% for item in items.reviewing %}
<tr>
  <td style='padding-right:0;'>{{ item }}</td>
</tr>
{% endfor %}
</table>
{% endblock body %}
