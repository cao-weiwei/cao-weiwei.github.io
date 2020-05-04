---
layout: default
title: Build a snake game in Python Day-4
date: 2020-05-03 23:00:00 -0400
published: 2020-05-03 23:00:00 -0400
comments: true
tags: [Python, pygame, curses]
github: "https://github.com/cao-weiwei/"
noimage: true
---

Today, I'm going to introduce `pygame` in a brief way. The main idea of this post is not to explain the detials of the `pygame` but some basic ideas of gaming programming. Let's get started😃!

<!--more-->

## How objects animate 

Gaming programming may have similarity with making animations, the core is not to make objects move literally but the way how we updating objects coordinates. 

- We draw objects on the surface and updating their positions to give us a kind of illusion to think the objects is alive. 
- Another thing about to determin whether the snake is alive, to check the objects' coordinates to find whether there is overlapping, if there is intersection of different objects' coordinates, we can say they may dead since there is collision. 

I think above is the key concepts we should understand for further programming🤓.

## How to use `pygame`

Basically, there are three steps for making a game in `pygame`:

-  Initialize and quit a game
- understand the coordinates in the game
- keep game ongoing

## Initialize and quit a game

The first thing before making any actions is to  import the `pygame` package. 

```python
import pygame
```

And then we need to initialize all the `pygame` modules:

```python
pygame.init() # initialize all pygame related modules
```

After initializing all related modules, we should create a surface for showing the game. Here `pygame` providers a way to control the display window and screen. 

```python
pygame.display.set_mode() # initialize a Surface to represent your drawing
pygame.display.update() # update the screen
```

The `display.set_mode()` function creates a new Surface object that represents the actual displayed graphics. Any drawing you do to this Surface will become visible on the monitor after you call `display.update()` method which allows  the screen to be updated

Next is the game iteself. Once we terminate the game, modules have to be closed to clean up all resources that we used. It can be done very ease.

```python
pygame.quit() # uninstall all pygame modules, and call it before the game ends
```

We can simply think the whole process of a game as follow:

<img src="/Users/caoweiwei/Library/Application Support/typora-user-images/image-20200503232632767.png" alt="image-20200503232632767" style="zoom:33%;" />



## Understand the coordinates in the game

The is very similar with what we learned in `curse`, please check it [here](https://cao-weiwei.github.io/posts/Build_a_Snake_Game_in_Python_Day_02/)

## Keep game ongoing

In order to avoid quiting the game after just starting, usually we'll add a infinite loop in the game. The basic build blocks of making object moving on the screen is as same as what we knew in `curses`library.

Next, we'll dive into the detail of coding in `pygame`.

---

If you like my articles please give me a star or leave comments below, thanks!