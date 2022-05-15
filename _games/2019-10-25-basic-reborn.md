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

As part of my Low Level Programming module at UWE we were tasked with porting a text adventure game made in BASIC to a C++ game using the [ASGE](https://github.com/HuxyUK/ASGE) game framework created by our professor, James Huxtable. The game we needed to port is the one created in <a href="https://www.amazon.co.uk/Write-Your-Own-Adventure-Microcomputer/dp/0686878329" target="_blank">Write Your Own Adventure: Programs for Your Microcomputer></a>.

After creating and submitting the game port, I went back to improve the game and created a text adventure framework where the rooms, items and all events are read in through JSON files, allowing flexibility and the creation of many different text adventures.

<centre>
  <img src="{{ site.baseurl }}/assets/BasicReb0rn/framework-main-menu.png"/>
</centre>

The Text Adventure Framework loads rooms, items and events from JSON files allow flexibility of rules such as commands the user can enter and the story of the game. 

The structure of the JSON files and how the events are managed can be found in the devlog linked above.