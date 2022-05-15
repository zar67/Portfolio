---
layout: game
title:  "Basic Reb0rn"
date:   2019-10-25 10:00:00 +0000
icon: "BasicReb0rn/icon.png"
publish: true
software-used: "CLion, GitKraken, GitHub"
languages-used: C++
code-repository: <a href="https://github.com/zar67/LLP-basic-reb0rn" target="_blank">GitHub</a>
devlog-title: 2019-10-01-basic-reborn
tags: [Student Project, LLP, BASIC, Coursework, C++]
---

<img src="{{ site.baseurl }}/assets/BasicReb0rn/framework-gameplay.png"/>

<h3>Summary</h3>

As part of my Low Level Programming module at UWE we were tasked with porting a text adventure game made in BASIC to a C++ game using the [ASGE](https://github.com/HuxyUK/ASGE) game framework created by our professor, James Huxtable. 

The game we needed to port is the one created in <a href="https://www.amazon.co.uk/Write-Your-Own-Adventure-Microcomputer/dp/0686878329" target="_blank">Write Your Own Adventure: Programs for Your Microcomputer></a>.

<h4>Task Requirements</h4>
- Emulate the existing BASIC game using an online emulator ([Calormen](https://www.calormen.com/jsbasic/)).
- Port the game to C++ using an Object Oriented structure.
- Stretch Goal: Improve the game and fix any bugs.

<h4>Improvements</h4>
After the submission I went back to improve the game and created a text adventure framework where the rooms, items and all events are read in through JSON files, allowing flexibility and the creation of many different text adventures.

<h4>Map</h4>

The game environment is an 8x8 map designed to be a haunted house. Each room can have items and specific events.

<img src="{{ site.baseurl }}/assets/BasicReb0rn/house-map.jpg"/>

<h3>Emulating BASIC</h3>

The goal of the BASIC game is to navigate through a haunted house and collect all the valuable items before trying to escape. The player uses text commands such as EXAMINE OBJECT and MOVE NORTH to progress through the game.

<video controls>
  <source src="{{ site.baseurl }}/assets/BasicReb0rn/basic-gameplay.mp4" type="video/mp4">
</video>

<h3>C++ Port</h3>

<video controls>
  <source src="{{ site.baseurl }}/assets/BasicReb0rn/cpp-port-gameplay.mp4" type="video/mp4">
</video>

<h3>Text Adventure Framework</h3>

The Text Adventure Framework load rooms, items and events from JSON files allow flexibility of rules such as commands the user can enter and the story of the game. 

<centre>
  <img src="{{ site.baseurl }}/assets/BasicReb0rn/framework-main-menu.png"/>
  <img src="{{ site.baseurl }}/assets/BasicReb0rn/framework-game-screen.png"/>
</centre>