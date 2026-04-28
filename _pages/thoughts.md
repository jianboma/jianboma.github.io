---
layout: page
title: Thoughts
permalink: /thoughts/
description: Personal reflections on AI, psychology, and the nature of thinking.
nav: true
nav_order: 3
horizontal: false
---

<div class="thoughts">
{%- assign sorted_thoughts = site.thoughts | sort: "date" | reverse %}
{%- for thought in sorted_thoughts -%}
  {% include think.html %}
{%- endfor %}
</div>