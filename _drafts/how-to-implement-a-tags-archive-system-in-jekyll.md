---
title: How to Implement a Tags Archive System in Jekyll
categories: [Notes]
tags: [jekyll, tags]
---

This post introduces how do I implement a tags archive system in [Jekyll](https://jekyllrb.com/).

## Diplaying Tags on a Post

1. Create a file `tags_bar.html` in the `_includes/` and put code blow into the file.


    ```html
    {% raw %}
    <div class="tags-bar">
        {% assign tags = page.tags | sort %}
        {% for tag in tags %}
        <span class="site-tag">
            <a class="site-tag-text" href="/tags/{{ tag | slugify }}.html">{{ tag | replace:'-', ' ' }}</a>
        </span>
        {% endfor %}
    </div>
    {% endraw %}
    ```

2. Insert the code below into the file `_layouts/post.html` at a whatever place you like.

    ```html
    {% raw %}
    {% include tags_bar.html %}
    {% endraw %}
    ```

3. Design the style of these tags. For example, a tag is placed in a rectangle with a random background color and a black or white text color.

    Copy the JavaScript file [`assets/js/color.js`](https://github.com/alxdhuang/minima-rock/blob/master/assets/js/color.js) (the code is mostly copied from [https://stackoverflow.com/a/35970186/11128302](https://stackoverflow.com/a/35970186/11128302)) into your repository, and insert the below into `_includes/tags_bar.html`.

    ```html
    {% raw %}
    <script type="text/javascript">
        setInvertedColor('site-tag-text');
    </script>
    {% endraw %}
    ```