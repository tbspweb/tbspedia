---
layout: default
title: Wiki Index
---

# Wiki Pages Index

{% assign all_pages = site.pages | where_exp: "page", "page.title" | sort: 'title' %}
{% assign main_pages = all_pages | where_exp: "page", "page.url contains '/'" | where_exp: "page", "page.url != '/'" %}

## Quick Stats
- Total Pages: {{ all_pages.size }}
- Last Updated: {{ site.time | date: "%Y-%m-%d" }}

---

## Browse by Namespace

<details open>
<summary><strong>📄 Main Pages ({{ main_pages.size }})</strong></summary>
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

<details>
<summary><strong>📂 Categories</strong></summary>
<ul>
{% for page in all_pages %}
  {% if page.url contains '/Category/' %}
<li><a href="{{ page.url | relative_url }}">{{ page.title }}</a></li>
  {% endif %}
{% endfor %}
</ul>
</details>

<details>
<summary><strong>🔧 Templates</strong></summary>
<ul>
{% for page in all_pages %}
  {% if page.url contains '/Template/' %}
<li><a href="{{ page.url | relative_url }}">{{ page.title }}</a></li>
  {% endif %}
{% endfor %}
</ul>
</details>

<details>
<summary><strong>👤 User Pages</strong></summary>
<ul>
{% for page in all_pages %}
  {% if page.url contains '/User/' %}
<li><a href="{{ page.url | relative_url }}">{{ page.title }}</a></li>
  {% endif %}
{% endfor %}
</ul>
</details>

<details>
<summary><strong>❓ Help Pages</strong></summary>
<ul>
{% for page in all_pages %}
  {% if page.url contains '/Help/' %}
<li><a href="{{ page.url | relative_url }}">{{ page.title }}</a></li>
  {% endif %}
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

---

## Search

<input type="text" id="search" placeholder="Search pages..." style="width: 100%; padding: 10px; margin: 10px 0; font-size: 16px;">
<ul id="results"></ul>

<script>
document.getElementById('search').addEventListener('input', function(e) {
  const query = e.target.value.toLowerCase();
  const pages = [
    {% for page in all_pages %}
    { title: "{{ page.title | escape }}", url: "{{ page.url | relative_url }}" },
    {% endfor %}
  ];
  
  const results = document.getElementById('results');
  results.innerHTML = '';
  
  if (query.length < 2) return;
  
  const matches = pages.filter(p => p.title.toLowerCase().includes(query));
  matches.slice(0, 20).forEach(page => {
    const li = document.createElement('li');
    const a = document.createElement('a');
    a.href = page.url;
    a.textContent = page.title;
    li.appendChild(a);
    results.appendChild(li);
  });
  
  if (matches.length === 0) {
    results.innerHTML = '<li>No results found</li>';
  }
});
</script>
