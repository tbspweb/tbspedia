---
layout: default
title: Wiki Index
---

# TBSPedia Pages Index

{% assign all_pages = site.pages | where_exp: "page", "page.title" | sort: 'title' %}
{% assign main_pages = all_pages | where_exp: "page", "page.url contains '/'" | where_exp: "page", "page.url != '/'" %}

- Last Updated: {{ site.time | date: "%Y-%m-%d" }}

---

## Browse by Namespace

<details open>
<summary><strong> TBSPedia Index({{ main_pages.size }})</strong></summary>
<ul>
{% for page in main_pages %}
  {% assign parts = page.url | split: '/' | size %}
  {% unless page.url contains '/Category/' or page.url contains '/Template/' or page.url contains '/User/' or page.url contains '/Help/' or page.url contains '/Talk/' %}
    {% if parts <= 2 or page.url contains '.html' %}
<li><a href="{{ page.url | relative_url }}">{{ page.title }}</a></li>
    {% endif %}
  {% endunless %}
{% endfor %}
</ul>
</details>

---

## Alphabetical Index

{% assign letters = "A,B,C,D,E,F,G,H,I,J,K,L,M,N,O,P,Q,R,S,T,U,V,W,X,Y,Z" | split: "," %}

{% for letter in letters %}
  {% assign letter_pages = all_pages | where_exp: "page", "page.title" | sort: 'title' %}
  {% assign has_pages = false %}
  {% for page in letter_pages %}
    {% assign first_char = page.title | slice: 0 | upcase %}
    {% if first_char == letter %}
      {% assign has_pages = true %}
      {% break %}
    {% endif %}
  {% endfor %}
  
  {% if has_pages %}
### {{ letter }}
    {% for page in letter_pages %}
      {% assign first_char = page.title | slice: 0 | upcase %}
      {% if first_char == letter %}
- [{{ page.title }}]({{ page.url | relative_url }})
      {% endif %}
    {% endfor %}
  {% endif %}
{% endfor %}

