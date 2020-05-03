---
layout: default
title: Build a snake game in Python Day-3
date: 2020-05-02 23:00:00 -0400
published: 2020-05-02 23:00:00 -0400
comments: true
tags: [Python, pygame, curses]
github: "https://github.com/cao-weiwei/"
noimage: true
---

😁A snake game could contains lots of features, if we want to improve the previous work, we must have clues about how to make progress🤔. Next we will use OOP ideas to make a fancy snake game.

<!--more-->

Contrary to procedure-oriented programming where programs are designed as blocks of statements to manipulate data, object-oriented programming organizes the program to combine data and functionality and wrap it inside something called an “Object”🧐. 

## OOP analysis and design

There is a structured approach for analyzing and designing a software product using OOP concepts. The most important thing is identifying the objects of the product and figuring out the relationships between each other. I'll explain the process of making the snake game as🥳:

1. Clarifying the requirements of snake game; 
2. Drawing a diagram to show how the snake  game works;
3. Identifying the objects and defining their relationships;
4. Making a design of the game.

## Clarifying requirements

🤓I'll focus on the following set of requirements while designing the snake game:

- At the screen, there is a welcome interface for users to wait for a further signal, users can click either 'start' button to start a game or 'quit' button to close the window.
- If the user clicks the 'start' button, entering a new game:
  - Food will be randomly put on the screen
  - A snake appears on somewhere of the screen and moving from left to right by default
  - The user whether presses arrow keys or not, the snake will keep moving
  - Press arrow keys to change the next direction of snake movement
  - Each time a piece of food is eaten, the snake's body length will increase by one, the user will get one point
  - If the food is eaten by the snake, the system will put another food randomly on the screen
  - The snake touches the wall or itself, the game ends
- If the user clicks the 'quit' button, the game will be terminated immediately.  

## Drawing process diagram and making prototype

The above whole process can be drawn in a figure as:

<img src="/assets/images/posts/Build_a_Snake_Game_in_Python_Day_03/01_snake_game_flow.png" alt="01_snake_game_flow" style="zoom:60%;" />

According to the process, I made mock-up of the interface.

<img src="/assets/images/posts/Build_a_Snake_Game_in_Python_Day_03/02_snake_game_prototype.png" alt="02_snake_game_prototype" style="zoom:50%;" />

## Identifying objects and defining relationships

As we knew, the most obvious objects in the game are the snake and the food. How to identify others and develop their relationships are vital points for making this game. 

**Board**: Everything in the game must be drawn or displayed on a board, like painting on canvas. And this board will contain a snake, food, and a score counter. It will initialize a game and end the game according to the conditions.

**Snake**: A snake, in the game, actually is a list of coordinates. we have to know the start position and its length. For the snake, it can move on the screen and eat food. And sometimes, it may die due to collision with the border or itself.

**Food**: As the same as the snake, it's also represented by a pair of coordinates on the screen. For the food, we should know whether it is eaten by the snake then we can draw another on the screen.

**Button**: This is a kind of UI component to receive a start signal and a terminate signal from use.  

<img src="/assets/images/posts/Build_a_Snake_Game_in_Python_Day_03/03_class_diagram.png" alt="03_class_diagram" style="zoom:60%;" />

## Making design of the game

Finally, based on previous analysis and objects we got, I made some UI of the game.

<img src="/assets/images/posts/Build_a_Snake_Game_in_Python_Day_03/04_demo-ui.png" alt="04_demo-ui" style="zoom:60%;" />

Next, we'll jump onto the pygame, which is a most famous game development library in Python.

---

If you like my articles please give me a star or leave comments below, thanks!