---
layout: post
title: "Notes of Getting Started with Phaser 3"
modified_date: 2019-04-13 22:46:08 +0800
date: 2019-04-07 15:18:20 +0800
categories: Programming
tags: game phaser
---

[*Getting Started with Phaser 3*](https://phaser.io/tutorials/getting-started-phaser3) is a tutorial written by [Richard Davey](https://twitter.com/photonstorm) for completely new guys to [Phaser](https://github.com/photonstorm/phaser).

## Why Need a Local Web Server?

> Your game is going to need to load resources: images, audio files, JSON data, maybe other JavaScript files. And in order to do this it needs to run unhindered by the browser security shackles. It needs `http://` access to the game files. And for that we need a web server.

## Installing a Web Server

### Python

```shell
cd /home/somedir
python3 -m http.server
```

### Node.js

```shell
npm install http-server -g
```

```shell
http-server [path] [options]
```

`[path]` defaults to `./public` if the folder exists, and `./` otherwise.

## Hello World

Create an [`index.html`](https://github.com/alxdhuang/phaser-examples/blob/master/hello-world/index.html) in a folder, then run a web server.

```shell
http-server
```

Open the web page (for example, `http://192.168.5.78:8080`) in a browser to play the game.