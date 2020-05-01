---
layout: default
title: Build a snake game in Python Day-2
date: 2020-04-30 23:30:00 -0400
published: 2020-04-30 23:30:00 -0400
comments: true
tags: [Python, pygame, curses]
github: "https://github.com/cao-weiwei/"
noimage: true
---

## Introduction

After knowing the building blocks of `curses`, let's jump onto our first version of the snake game🧐. 

<!--more-->

Maybe you will think that it seems too abstract for you to take actions to build such a game using the previous knowledge, and the scenarios might be familar with you, if someone told you how to draw a panda in 4 steps 🤨

<img src="/assets/images/posts/Build_a_Snake_Game_in_Python_Day_02/01_how_to_drawa_panda_in_4_steps.png" alt="01_how_to_drawa_panda_in_4_steps" style="zoom:60%;" />

## Analysis the snake game

Exactly right, even we know all the ways how to use tools we cannot build a house without enough preparations ahead. Let's recall the last time you played the snake game, if you have no ideas about the game, just googling it😏.  Here are the major factors in this game:

1. There should be three main actors in the game:

- First is the main board or screen, which contains a snake and a piece of food. 
- Then is the snake, it will travel on the board and searching for food. 
- The last thing is a piece of food that can be eaten by the snake. That's all visible objects on the screen.

2. Except for the above objects, we should know how the ways that users interacting with the game. In this terminal game, we assume that the user can only use four arrow keys to control the moving directions of the snake. 

3. Snake is controlled by users and the main purpose of the game is to eat as much as possible food, so every time a piece of food is eaten by the snake it will show on the board randomly and the snake will get lengthened due to eating the food. 
4. If the snake crashed into the boundary of the board or itself, then the game will over.

As long as we have the ideas of the game, we could get started on the code, doing the coolest things😎. However, before we dive into the code, it's best to take a bird's-eye view and see everything all right:

- firstly, we should initialize a screen for using as the board of the game, and I hope you have ideas about how to set a screen in `curses`;
- then,  objects, a snake and a piece of food, are drawn on the screen;
- the last and the most complex step is the main process of the game, controlling snake to move and to eat food.

## Coding time

### 1. To initialize a screen

First and the formost is to initialize a screen, otherwise nothing will be shown😂.

```python
import curses, random

# 0. initialize a main screen of the game
main_scr = curses.initscr()  
curses.curs_set(0)  # 0.1 setting the visibility of cursor, 0-invisible, 1-normal, 2-strong
# 1. based on the main screen to create a gaming board
height, width = main_scr.getmaxyx()  # 1.1 get the height and width of the main screen
board = curses.newwin(height, width, 0, 0)  # 1.2 create a board for gaming
board.keypad(1)  # 1.3 using keyboard for receiving commands
board.timeout(100)  # 1.4 setting for inerval, every 100 ms the board will get a char from user
```

When we have the canvas, we can paint snake and food on it right now.

### 2. To paint snake and food

Everything displayed on screen is tracked by using a pair of coordinate, let's say `(y, x)`. Y-asixs represents the height of the object and x-asixs represents the width of the object. If we draw a box on a screen and its coordinate is `(y, x)`, it can be explained using below figure.   

<img src="/assets/images/posts/Build_a_Snake_Game_in_Python_Day_02/02_coordinate.png" alt="02_coordinate" style="zoom:40%;" />

```python
# 2. draw a snake on the board
snake_y = int(height / 4)  		# 2.1 initial head coordinates of a snake
snake_x = int(width / 2)
snake = [  										# 2.2 draw a snake with coordinates on the board
    [snake_y, snake_x],  			# 2.3 the coordinates of head
    [snake_y, snake_x - 1],  	# 2.4 the coordinates of body
    [snake_y, snake_x - 2],
    [snake_y, snake_x - 3],
    [snake_y, snake_x - 4]
]
board.addch(snake[0][0], snake[0][1], '+')	# 2.5 paint chars on the screen and update screen
main_scr.refresh()

# 3. put the first food spot on the board
food_y = int(height / 2)		# 3.1 initial position of food
food_x = int(width / 2)
food_pos = [food_y, food_x]
board.addch(food_pos[0], food_pos[1], '$')  # 3.2 paint the first position of food
main_scr.refresh()
```

The next is the core of the game, which will contrl the snake to move on the board and eat the food. Before that we should set a defualt direction of the snake, then it will automatically move at first.

```python
# 4. set the default direction of the snake
key = curses.KEY_RIGHT 
```

###  3. Main process of the game

####  3.1 To Receive command from keyboard

In `curses`, we use the function `window.getch() ` to get the pressed key from keyboard and it will return an integer which represents a key. [Keys are referred to by integer constants with names starting with `KEY_`](https://docs.python.org/3/library/curses.html)

```python
# 6. get command from user to control the snake
next_key = board.getch()  # 6.1 waiting for getting input from keyboard
if next_key != -1:  			# 6.2 successfully received from keyboard
  if key == curses.KEY_RIGHT and next_key != curses.KEY_LEFT \
  or key == curses.KEY_LEFT and next_key != curses.KEY_RIGHT \
  or key == curses.KEY_UP and next_key != curses.KEY_DOWN \
  or key == curses.KEY_DOWN and next_key != curses.KEY_UP:
    key = next_key
```

#### 3.2 To check the snake whehter is alive

After moving the directions of the snake, we should check the status of the snake to ensure the snake is alive and the game can continue. There are two cases of ending game, one is the snake meets the boundary of the board, and the other is the snake crash itself.

```python
# 7. check whether the snake is alive
if snake[0][0] in [0, height] or snake[0][1] in [0, width] or snake[0] in snake[1:]:  # 7.1 cases for ending game
  main_scr.keypad(0)  # reset the terminal
  curses.echo()
  curses.nocbreak()
  curses.endwin()     # close the terminal
  quit()

# 8. draw a new head of the snake and concatenate it into the previous snake body
snake_y = snake[0][0]
snake_x = snake[0][1]
if key == curses.KEY_RIGHT:  		# move to right
  snake_x += 1
elif key == curses.KEY_LEFT:  	# move to left
  snake_x -= 1
elif key == curses.KEY_UP:  		# move to up
  snake_y -= 1
elif key == curses.KEY_DOWN:  	# move to down
  snake_y += 1

snake.insert(0, [snake_y, snake_x])  # put the new head of snake in the list
```

####  3.3 To check the food whether is eaten  

When the snake moved, the food might be eaten by the snake or not. If the snake eats the food, we should lengthen the snake and put another food on the screen, otherwise we don't change anything on the screen.

```python
# 9. check whether the food is eaten by the snake
if snake[0] == food_pos:    # 9.1 eat the food
  food_pos = None
  while not food_pos:     	# create new food randomly but excluding the coordinates in snake
    food_y = random.randint(1, height - 1)
    food_x = random.randint(1, width - 1)
    food_pos = [food_y, food_x]
    if food_pos not in snake:   # avoid new coordinates in snake
      board.addch(food_pos[0], food_pos[1], '$')
    else:
      food_pos = None
else:   # 9.2 not eat the food, pop the tail since we insert a new head before
  tail = snake.pop()
  board.addch(tail[0], tail[1], ' ')
```

Don't forget to paint changes on the screen and update it.

```python
# 10. draw the new head on screen
board.addch(snake[0][0], snake[0][1], '+')
main_scr.refresh()
```

#### 3.4 To animate the snake

Once we achieve the functionalities of above sections in #3.1 - #3.3, we should make the snake alived on the screen, but how?  The code is a little tricky and straightforward, we need to put the code in a infinite loop and boom all things have done😎.

```python
# 5. Main loop until the user lose or close the game.
while True:
  # code in 3.1 - 3.3
```

Finally, we achieved the first version of the game, enjoy it 🤩!

<img src="/assets/images/posts/Build_a_Snake_Game_in_Python_Day_01/snake_01_curse.gif" alt="snake_01_curse" style="zoom:90%;" />

See previous articles plece check 👉[here](https://cao-weiwei.github.io/posts/Build_a_Snake_Game_in_Python_Day_01/)👈.  Next, we'll improve our tiny game using GUI, however, before that we should go deep in analysis using object oriented programming techniques.

---

If you like my articles please give me a star or leave comments below, thanks!