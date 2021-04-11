---
layout: post
title: The Master Plan
date: 2019-10-05 10:00:00
category: [Basic Reb0rn Devlog]
---

My first step in developing the C++ port of Basic Reb0rn was to get my documentation started. I setup a basic GDD and TDD with information from the book and my plans for the game.
By reading through the book, I learned alot more about the design of the game that I did by simply copying the BASIC code. 

I outlined the structure and game flow in my documentation, these will likely change as the development of this project continues. My initial plan for the objects of the game is shown in the class diagram below.

<img src="{{ site.baseurl }}/assets/Blog/BasicRebornDevlog/class_diagram.jpg" alt="class diagram for the C++ port"/>

In my GDD I outlined what I wanted to improve about various features as they were documented. Such as:
* Using the arrow keys for movement
* The addition of a menu and game over screen
* Changing the bats and ghosts so that the player can leave the room the way they came in, but that is the only action they can do until they defeat the bats and ghosts.
* Improvement of the boat and marsh system

In my documentation I also laid out the words, map and objects that will be in the C++ version of the game. The map of the house can be seen below.

<img src="{{ site.baseurl }}/assets/Blog/BasicRebornDevlog/house_map.jpg" alt="haunted house map"/>

I will also be loading in the rooms, words and objects through JSON files since they are easily editable and easy to read. There is a JSON library included in the boilerplate code which allows me to retrieve information from JSON files.