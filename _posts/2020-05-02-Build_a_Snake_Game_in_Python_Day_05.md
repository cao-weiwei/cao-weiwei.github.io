---
layout: default
title: Build a snake game in Python Day-5
date: 2020-05-05 23:00:00 -0400
published: 2020-05-06 23:00:00 -0400
comments: true
tags: [Python, pygame]
github: "https://github.com/cao-weiwei/"
noimage: true
---

Now we almost have developled the entire game, just a little coding. Today, I will introduce the class implementation based on previous analysis😃!

<!--more-->

## The Snake Class 

🤓As we've already analyzed, the `Snake` class should do following things:

- initialize a snake instance with attributes
- get signals from keyboard to move in different directions
- to eat the food on the screen and 
- to determine whehter the snake is alive after moving

And the implementation is here:

```python
"""
@author Weiwei Cao  2020-05-03
This is a class of Snake.
"""
import Food
import InitGame


class Snake:
    def __init__(self):
        """
        initialize a snake
        """
        self.default_length = 5
        self.head_x, self.head_y = [InitGame.WIDTH // 4, InitGame.HEIGHT // 2]
        self.snake = [[self.head_x - (i * 20), self.head_y] for i in range(self.default_length)]
        self.current_direction = "right"  # default direction of the snake

    def move(self, next_direction: str) -> None:
        """
        receive signals from keyboard and changing coordinates of the snake
        :param next_direction: next direction string
        :return: None
        """
        # 0. change the direction of next direction is not opposite with current direct
        if self.current_direction == "right" and next_direction != "left" \
                or self.current_direction == "left" and next_direction != "right" \
                or self.current_direction == "up" and next_direction != "down" \
                or self.current_direction == "down" and next_direction != "up":
            self.current_direction = next_direction

        # 0.1 get new head position
        new_head_x, new_head_y = self.head_x, self.head_y
        if self.current_direction == "up":
            new_head_x = self.head_x
            new_head_y -= 20
        elif self.current_direction == "down":
            new_head_x = self.head_x
            new_head_y += 20
        elif self.current_direction == "left":
            new_head_x -= 20
            new_head_y = self.head_y
        elif self.current_direction == "right":
            new_head_x += 20
            new_head_y = self.head_y
        # 0.2 insert new head into the 1st index and update the head position
        self.snake.insert(0, [new_head_x, new_head_y])
        self.head_x, self.head_y = new_head_x, new_head_y
        # 0.3 pop the last coordinate (x, y)
        self.snake.pop()
        print(self.snake)

    def get_position(self) -> list:
        """
        get the coordinates of the snake = head * 1
        :return: a list contains coordinates of a snake
        """
        return self.snake

    def get_length(self) -> int:
        """
        get current length of the snake
        :return: current length of the snake
        """
        return len(self.snake) - self.default_length

    def eat(self, food: Food) -> None:
        """
        After eating a piece of food, updating the coordinates of the snake
        :param food: an instance of Food
        :return: None
        """
        food_pos = food.get_position()  # get the food position
        self.snake.insert(0, [food_pos[0], food_pos[1]])  # add food into the snake
        self.head_x, self.head_y = food_pos[0], food_pos[1]  # update the head of the snale

    def is_alive(self) -> bool:
        """
        Check whether the snake is alive
        :return: True if the snake is alive, otherwise False
        """
        # if the snake head is on the border or has collision with itself, then dead, return False
        if self.head_x in [-InitGame.W_CELL, InitGame.WIDTH] or self.head_y in [-InitGame.H_CELL, InitGame.HEIGHT] \
                or [self.head_x, self.head_y] in self.snake[1:]:
            return False
        else:  # the snake is alive
            return True

```

## The Food Class

Basically, `Food` class will do such things:

-  initialize a food position
-  to determine whether current food is eaten by the food and
-  update another position for the new food

```python
"""
@author Weiwei Cao  2020-05-03
This is a class of Food.
"""

import random
import InitGame
import Snake


class Food:
    def __init__(self):
        """
        Initialize the first pair of coordinate of food
        """
        self.food_x = random.randint(5, InitGame.COLS - 5) * InitGame.W_CELL
        self.food_y = random.randint(5, InitGame.ROWS - 5) * InitGame.H_CELL
        self.food_pos = [self.food_x, self.food_y]

    def update_position(self) -> None:
        """
        Randomly generate a new pair of coordinate for putting food
        :return: None
        """
        self.food_x = random.randint(5, InitGame.COLS - 5) * InitGame.W_CELL
        self.food_y = random.randint(5, InitGame.ROWS - 5) * InitGame.H_CELL
        self.food_pos = [self.food_x, self.food_y]

    def get_position(self) -> list:
        """
        Get the food position
        :return: a list contains the food coordinate in x-axis and y-axis
        """
        return self.food_pos

    def is_eaten(self, snake: Snake) -> bool:
        """
        To check the food is whether eaten by the snake
        :param snake: an instance of Snake
        :return: True if the food is eaten by the snake else return False
        """
        if self.food_pos in snake.get_position():
            return True
        else:
            return False

```



## The Button Class

There is no `Button` class in `pygame` and we need buttons to acpture mouse status and to start or quit the game, so we add following features in this class:

- to set and get attributes of a button, such as the position, size and color, etc,.
- to check the status of a button, like does the mouse is clicked in a legal area of the button

```python
"""
@author Weiwei Cao  2020-05-03
This is a class of Button.
"""


class Button:
    def __init__(self, btn_pos: tuple, btn_size: tuple, txt_pos: tuple, txt: str):
        """
        Initialize a Button object with below attributes
        :param btn_pos: a pair of coordinate, (x, y)
        :param btn_size: a pair of size, (width, height)
        :param txt_pos: a pair of coordinate, (x, y)
        :param txt: a string that will displayed on button
        """
        self.button_pos = btn_pos
        self.button_width = btn_size[0]
        self.button_height = btn_size[1]
        self.button_text_pos = txt_pos
        self.button_txt = txt

    def get_position(self) -> tuple:
        """
        get button start coordinate
        :return: a tuple contains start coordinate (x, y)
        """
        return self.button_pos

    def get_size(self) -> tuple:
        """
        get the size of button
        :return: a tuple contains width and height of the button (width, height)
        """
        return self.button_width, self.button_height

    def get_text(self) -> tuple:
        """
        get the text information on the button
        :return: a tuple contains (text, [x, y])
        """
        return self.button_txt, self.button_text_pos

    def is_hover(self, mouse_pos: tuple) -> bool:
        """
        To check  whether the mouse is hover on the button
        :param mouse_pos: an status of mouse object
        :return: True if the mouse is hover on the button else return False
        """
        if self.button_pos[0] <= mouse_pos[0] <= (self.button_pos[0] + self.button_width) \
                and self.button_pos[1] <= mouse_pos[1] <= (self.button_pos[1] + self.button_height):
            return True
        else:
            return False

    def is_click(self, click_status: tuple) -> bool:
        """
        To check whether the button is clicked by the mouse
        :param click_status: status of mouse object
        :param mouse_pos: status of mouse click
        :return: True if the mouse is clicked on the button else return False
        """
        if click_status[0] == 1 or click_status[1] == 1 or click_status[2] == 1:
            return True
        else:
            return False

```

## The core class of the game

Next is the core of the game, and it contains some configurations of the game and implement key features. The framework of is should be as following:

```python
# a class initialize the game
class Board(object):
    def __init__(self):
        """
        Initialize all related modules and the screen
        """
        pass

    def draw_objects(self, obj: object, color: tuple) -> None:
        """
        Draw objects on the screen
        :param color: the color of objects
        :param obj: instance of an object that should be drawn on the screen
        :return: None
        """
        pass

    def end_game(self, score: int) -> None:
        """
        End the current running game it will give options to user to choose a new round or exit the game
        :param score: current game scores
        :return: None
        """
        pass

    def play_game(self) -> None:
        """
        The main part for starting a game
        :return: None
        """
        pass
      
    def intro_game(self) -> None:
        """
        An interface the before user starting the game.
        If user click start, it will call the play_game() method
        If user click quit, it will close the window
        :return: None
        """
        pass
      
```

Next, we'll dive into the detail of this class .

---

If you like my articles please give me a star or leave comments below, thanks!