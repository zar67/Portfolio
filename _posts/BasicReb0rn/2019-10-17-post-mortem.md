---
layout: post
title: Post-Mortem
date: 2019-10-22 18:00:00
category: [Basic Reb0rn Devlog]
---

Here is the comparison between the original BASIC Game (first) and my C++ port (second).

<video controls>
  <source src="{{ site.baseurl }}/assets/Blog/BasicRebornDevlog/BASIC Gameplay.mp4" type="video/mp4">
</video>

<video controls>
  <source src="{{ site.baseurl }}/assets/Blog/BasicRebornDevlog/C++ Port Gameplay.mp4" type="video/mp4">
</video>

I'm pretty happy with the port I managed to create. I made some changes in order to slightly improve gameplay but kept to the main design and feel of the game.

My use of classes for the different game data aspects (room, actions and objects) was effective, however my main Game files became crowded pretty quickly. I improved this by adding a Map class to hold information about the rooms and objects, but I could've improved this more with a Player class to clean up my code more.

However, the game runs smoothly and I have fixed the known bugs with the game.

The main changes I made were:
* Changed "CARRYING?" to "INVENTORY"
* Changed "CLIMB ROPE" to "CLIMB TREE" since that's what people naturally assumed the command was.
* Allowed the player to chop down the tree using "SWING AXE", meaning that they could no longer climb it.
* Stopped the player from being able to relight the candle if it was burnt out. In the original game it would seem like you had relit the candle, but performs actions like the candle isn't lit.
* Stopped the player from moving back into the marsh when the boat gets stuck.
* Allows the player to get into the house from the front door, stopping the player from getting compeltely stuck when using the boat, this was game ending in the original version.
* When in the room with the bats and the ghosts, the player can leave the room and vanquish the enemies only. In the original game, these rooms were game ending if you didn't have the correct objects. Now the bats and ghosts simply block the player from progressing until they are removed.
* In order to complete the game, you have to collect all of the treasures instead of all the items. This makes more sense and doesn't change the gameplay since the player has to collect most of the objects in order to get all the treasures.

<h3>Structure Improvments</h3>
In order to improve the code, adding the action commands to the JSON file and parsing them when loading the data would make the code much simplier; it would also allow me to create a range of text adventure games using JSON files of the same struture.