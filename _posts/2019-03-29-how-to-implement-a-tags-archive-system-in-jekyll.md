---
title: How to Implement a Tags Archive System in Jekyll
date: 2019-03-29 11:23:25 +0800
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
            <a class="site-tag-text" href="{{ site.baseurl }}/tags/{{ tag | slugify }}.html">{{ tag | replace:'-', ' ' }}</a>
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

    At last, insert `<script type="text/javascript" src="{{ site.baseurl }}/assets/js/color.js"></script>` into the `<head>`.

## Creating Tags Archive Pages

1. Create a file `_includes/tags_archive.html` with content as below.

    ```html
    {% raw %}
    <ul>
    {% for tag in site.tags %}
    {% if tag[0] == page.tag %}
        {% assign post_list = tag[1] %}
        {%- for post in post_list -%}
        <li>
            <span>{{ post.date | date: "%Y-%m-%d" }}</span> &raquo;
            <a href="{{ post.url | relative_url }}">
            {{ post.title | escape }}
            </a>
        </li>
        {%- endfor -%}
    {%- endif -%}
    {% endfor %}
    </ul>
    {% endraw %}
    ```

2. For every tag, for example, `jekyll`, create a file (in this case, named `jekyll.md`) in the folder `tags/`. The file look like this:

    ```html
    {% raw %}
    ---
    layout: page
    title: "Tag: 'jekyll'"
    tag: jekyll
    ---

    {% include tags_archive.html %}
    {% endraw %}
    ```

    Then, every tag `TAG` has an archive page with a url `/tags/TAG.html`.

3. (*Optional*) Creating an archive page manually for every tag is so tired. So I have created a Python script [`gen_tags.py`](https://github.com/alxdhuang/minima-rock/blob/master/script/gen_tags.py) to automatically generate archive pages. You can copy it into your repository and run it before every time you publish your posts.

## Creating Tags Cloud

1. Create a template `_includes/tags_cloud.html`. It is very alike `tags_bar.html`, except that the font size of tags is determined by the number of posts that use them.

    ```html
    {% raw %}
    <p class="tag-cloud">
    {% assign tags = site.tags | sort %}
    {% for tag in tags %}
    <span class="site-tag">
    <a class="site-tag-text" href="{{ site.baseurl }}/tags/{{ tag | first | slugify }}.html" style="font-size: {{ tag | last | size | times: 4 | plus: 80 }}%;">
        {{ tag[0] | replace:'-', ' ' }}
    </a>
    </span>
    {% endfor %}
    </p>

    <script type="text/javascript">
        setInvertedColor('site-tag-text');
    </script>
    {% endraw %}
    ```

2. Create a tags cloud page `tags.md`.

    ```
    {% raw %}
    ---
    layout: page
    title: Tags
    ---

    {% include tags_cloud.html %}
    {% endraw %}
    ```