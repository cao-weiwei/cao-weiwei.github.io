---
layout: default
title: Build a snake game in Python-1
date: 2020-04-29 23:30:00 -0500
published: 2020-04-29 23:30:00 -0500
comments: true
tags: [Python, pygame, curses]
github: "https://github.com/cao-weiwei/"
noimage: true
---

## Introduction

How are you guys😀! In the next following days, I'm going to introduce an interesting and small project which implemented in `Python`, using some third part libraries to create a snake game. I know it's not a big deal to complete such a project, but it really gives me a kind of enjoyment in these self-isolation days🤓. 

<!--more-->

Acutally, this iead is inspired by a youtuber and he did a snake game using `curses` library which is native supported by `Python`. You can check it out here 👉[<u>Creating a Snake game with Python in under 5 minutes</u>](https://www.youtube.com/watch?v=rbasThWVb-c&feature=youtu.be)👈. I followed his code and made it, below is the outcome.

<img src="assets/images/posts/Build_a_Snake_Game_in_Python_Day_01/snake_01_curse.gif" alt="snake_01_curse" style="zoom:90%;" />

Honestly, I was catched by the keywords '5 minutes', it took me more than 5 minutes actually. However, I should say after completing this naive game my passion was ignited and I thought it's a time for implementing a beautiful version to make me feel happy. As a result, I've just achieved this game in first version, and it will be explained in detail at next days. Here is the glance of the game interface.

<img src="assets/images/posts/Build_a_Snake_Game_in_Python_Day_01/snake_02_1st_glance.gif" alt="snake_02_1st_glance" style="zoom:80%;" />

I intend to introduce the development in following steps:
- Day1: basic idead about `curses`
- Day2: how to use `curses` to implement the game
- Day3: let's analyze the game in deep using OOP ideas
- Day4: learn pygame to draw objects and get commands
- Day5: implement the key classes of the game
- Day6: add background music and images to make it better

Now, let's jump into the `curses` to start the journey.

## About `curses`

The `curses` is a library in for people who want to create command line applications. It's based on the termial on linux or Mac to build textual interfaces, using keyboard to interact with users. It's a built-in `Python` library and provides lots of APIs to implement powerful functionalities. In short, there are two key concepts in this module.

### 1. Initializing and closing a window

We can simply think a window is a kind of canvas which contains all the objects that will display on a termial. We can create multiple windows with different sizes and place them around your screen. If we add something on a window, we should refresh the window to display the changes and if we don't use the window anymore, we should close it properly.

```python
import curses

main_scr = curses.initscr()  # initialize a main screen, getting the window object
# do something
main_scr.refresh()	# in order to update the window
# job is done
curses.endwin()     # close the window
```

If we want to declare a window with specific size, we should using another method called `newwin()`, this method can set the window's start coordinates,  height and width.

```python
board = curses.newwin(height, width, 0, 0)  # initialize a window with the size of (height, width) on the screen (0, 0)
```

### 2. Adding and displaying characters  

As we know, characters can be represented either in strings or letters one by one. Text can be printed on a window by using following statements.

```python
board.addch(0, 0, '$')  # painting a character '$' on the screen (0, 0)
board.addstr(0, 0, "Hello, snake") # putting a sentence on the screen (0, 0)
```

The above is enough for creating a simple terminal snake game, for full APIs please check offical documents 👉[here](https://docs.python.org/3/library/curses.html)👈.  Let's dive into more at tomorrow, see ya.

---

If you like my projects please give me a star or leave comments below, thanks!