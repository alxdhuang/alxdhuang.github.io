---
layout: post
title: "Notes of Python Crash Course"
categories: Programming
tags: python
---

Here are some notes of [*Python Crash Course*](https://nostarch.com/pythoncrashcourse) (2015) by Eric Matthes.

{% include toc.html %}

## Projects

### Alien Invasion

#### Plan

> In Alien Invasion, the player controls a ship that appears at the bottom center of the screen. The player can move the ship right and left using the arrow keys and shoot bullets using the spacebar. When the game begins, a fleet of aliens fills the sky and moves across and down the screen. The player shoots and destroys the aliens. If the player shoots all the aliens, a new fleet appears that moves faster than the previous fleet. If any alien hits the player’s ship or reaches the bottom of the screen, the player loses a ship. If the player loses three ships, the game ends.

A simple, maybe boring game.

#### Installing Pygame

##### Installing Pygame on OS X

First, using [homebrew](https://brew.sh/) to install some libraries the [Pygame](https://www.pygame.org/news) depends on.

```
brew install hg sdl sdl_image sdl_ttf sdl_mixer portmidi
```

- `sdl`: Low-level access to audio, keyboard, mouse, joystick and graphics.
- `sdl_image`: Image file loading library.

