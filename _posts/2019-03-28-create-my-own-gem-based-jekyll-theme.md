---
title: Create My Own Gem-based Jekyll Theme
date: 2019-03-28 12:26:28 +0800
modified_date: 2019-04-13 22:45:17 +0800
categories: [IT, Notes]
tags: [jekyll, blog, ruby]
---

I want to customize the [Minima](https://github.com/jekyll/minima) theme. Why don't I just clone the repository and integrate it into my project? Because that way is not easy to maintain. I would very difficult to keep track of the new progress of Minima project. A better way is forking the Minima project and modify it, then use the new theme in my blog site.

## Publishing

I have forked the minima, and renamed it to [minima-rock](https://github.com/alxdhuang/minima-rock). After a little modification, I can finally publish it. First, I need a [RubyGems](https://rubygems.org) account, then follow commands below.

```
gem build minima-rock.gemspec
gem push minima-rock-VERSION.gem
```

## Using

1. Add `gem 'jekyll-remote-theme'` in the `Gemfile`.
2. Specify below in the `_config.yml`.

    ```yml
    plugins:
      - jekyll-remote-theme
    
    remote_theme: alxdhuang/minima-rock
    ```