---
layout: post
title: "How to Set The Background Image in Jekyll According to Week Days"
date: 2019-03-30 17:22:42 +0800
categories: Notes
tags: jekyll javascript css
---

I have wrote a script that could set different background images to the `<body>` element according to different week days. Just insert the code below after the `<body>` element.

```html
{% raw %}
{% if site.data.backgrounds %}
    <script>
      const imgs = [
        {%- for item in site.data.backgrounds -%}
          '{{ item.name }}',
        {%- endfor -%}
      ];
      const date = new Date();
      const index = date.getDay() % imgs.length;
      document.body.style.backgroundImage = `url('{{ site.baseurl }}${imgs[index]}')`;
    </script>
{% endif %}
{% endraw %}
```
