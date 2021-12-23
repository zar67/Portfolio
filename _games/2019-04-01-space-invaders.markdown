---
layout: game
title:  "Space Invaders"
icon: "SpaceInvaders/space-invaders.jpg"
date:   2019-04-01 10:00:00 +0000
status: "Finished"
publish: false
software-used: "CLion, GitKraken, GitHub"
languages-used: C++
textures: <a href="https://www.kenney.nl/" target="_blank">Kenney</a>
code-repository: <a href="https://github.com/zar67/ESD-invaders-of-the-earth" target="_blank">GitHub</a>
download-location: <a href="https://zoerowbotham.itch.io/spaceinvaders" target="_blank">zoerowbotham.itch.io</a>
tags: [Student Project, ESD, Space Invaders, C++]
---

In order to help me learn C++ in my first year of university, I recreated the popular game Space Invaders. In the game, alien ships move downwards towards the player. In order to win the game, the player has to shoot all of the ships. However, if the ships get too close or the player gets shot, it's game over and Earth is taken over by aliens...

<video controls>
  <source src="{{ site.baseurl }}/assets/SpaceInvaders/space-invaders-normal.mp4" type="video/mp4">
</video>

<img src="{{ site.baseurl }}/assets/SpaceInvaders/space-invaders-normal.jpg"/>
<img src="{{ site.baseurl }}/assets/SpaceInvaders/space-invaders-lost.jpg"/>

As part of this project, I experimented with different trajectories of the aliens. The main ones were the curved (quadratic) trajectory and the sin curve. These can be seen below.

<video controls>
  <source src="{{ site.baseurl }}/assets/SpaceInvaders/space-invaders-quadratic-movement.mp4" type="video/mp4">
</video>

<video controls>
  <source src="{{ site.baseurl }}/assets/SpaceInvaders/space-invaders-sine-movement.mp4" type="video/mp4">
</video>