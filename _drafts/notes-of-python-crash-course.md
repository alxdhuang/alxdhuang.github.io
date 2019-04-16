---
layout: post
title: "Notes of Python Crash Course"
categories: Programming
tags: python
---

[*Python Crash Course*](https://nostarch.com/pythoncrashcourse) (2015) by Eric Matthes.

{% include toc.html %}

## Projects

### Alien Invasion

#### Plan

> In Alien Invasion, the player controls a ship that appears at the bottom center of the screen. The player can move the ship right and left using the arrow keys and shoot bullets using the spacebar. When the game begins, a fleet of aliens fills the sky and moves across and down the screen. The player shoots and destroys the aliens. If the player shoots all the aliens, a new fleet appears that moves faster than the previous fleet. If any alien hits the player’s ship or reaches the bottom of the screen, the player loses a ship. If the player loses three ships, the game ends.

A simple, maybe boring game.

#### Installing Pygame

The installing steps introduced in this book seem too complicated. According to [the official wiki](https://www.pygame.org/wiki/GettingStarted), there is only one step:

```
python3 -m pip install -U pygame --user
```

The `--user` flag means to install into the home directory rather than globally.

Check it works:

```
python3 -m pygame.examples.aliens
```

#### Starting the Game

`alien_invasion.py`:

```python
import sys
import pygame

def run_game():
    pygame.init()
    pygame.display.set_mode((1200, 800))
    pygame.display.set_caption("Alien Invasion")

    # The game loop
    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                sys.exit()

        pygame.display.flip()

run_game()
```

This code fragment just creates an empty window and listens to a quit event.

[`pygame.init()`](https://www.pygame.org/docs/ref/pygame.html#pygame.init) initializes all imported pygame modules. "No exceptions will be raised if a module fails, but the total number if successful and failed inits will be returned as a tuple." We can log this information,

```python
numpass, numfail = pygame.init()
print(str(numpass) + " pass, " + str(numfail) + " fail.")
```