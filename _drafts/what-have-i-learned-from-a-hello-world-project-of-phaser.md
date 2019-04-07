---
layout: post
title: "What Have I Learned from a Hello World Project of Phaser"
categories: Notes
tags: game phaser
---

The [Hello World](https://phaser.io/tutorials/getting-started-phaser3/part5) project is a tiny example game to introduce [Phaser](https://github.com/photonstorm/phaser).

Version: v3.16.2

{% include toc.html %}

## How to Create a New Game

```javascript
var game = new Phaser.Game(config);
```

`Phaser` is a namespace exported from the Phaser framework. We create an instance of the `Game` class by passing a configuration `config`.

## What Does the Configuration Have

For example,

```javascript
var config = {
    type: Phaser.AUTO,
    width: 800,
    height: 600,
    physics: {
        default: 'arcade',
        arcade: {
            gravity: { y: 200 }
        }
    },
    scene: {
        preload: preload,
        create: create
    }
};
```

`config.type` specifies the type of renderer. We can also set it as `Phaser.WEBGL` or `Phaser.CANVAS`.