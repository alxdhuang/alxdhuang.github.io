---
title: Create My Own Gem-based Jekyll Theme
categories: [Notes]
tags: [jekyll, blog, ruby]
---

I want to customize the [Minima](https://github.com/jekyll/minima) theme. How don't I just clone the repository and integrate it into my project? Because that way is not easy to maintain. I would very difficult to keep track of the new progress of Minima project. A better way is forking the Minima project and modify it, then use the new theme in my blog site.

## Publishing

I have forked the minima, and renamed it to [minima-rock](https://github.com/alxdhuang/minima-rock). After a little modification, I can finally publish it. First, I need a [RubyGems](https://rubygems.org) account, then follow commands below.

```
gem build minima-rock.gemspec
gem push minima-rock-VERSION.gem
```