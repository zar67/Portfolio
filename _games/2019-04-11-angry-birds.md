---
layout: game
title:  "Angry Birds"
icon: "AngryBirds/angry-birds.jpg"
date:   2019-04-11 10:00:00 +0000
publish: true
software-used: "CLion, GitKraken, GitHub"
languages-used: C++
code-repository: <a href="https://github.com/zar67/ESD-angry-birds" target="_blank">GitHub</a>
textures: <a href="https://www.kenney.nl/" target="_blank">Kenney</a>
download-location: <a href="https://zoerowbotham.itch.io/angry-birds" target="_blank">zoerowbotham.itch.io</a>
tags: [Student Project, ESD, Angry Birds, Coursework, C++]
---

<img src="{{ site.baseurl }}/assets/AngryBirds/angry-birds-game.jpg"/>

This Angry Birds remake was my last piece of coursework for my first year of university. The task was to make a simplified Angry Birds replica where the player could catapault objects into other objects to destroy them. I decided to expand on this by creating structures and a very simple (and somewhat buggy) physics simulation to handle the collisions and the resolutions. 

As the first time trying to implement physics into a game from scratch this task was very challenging to me, but I manages to implement a simple collision detection and response system, even if it's a bit buggy.

As you can see in the video, the physics isn't perfect...

<video controls>
  <source src="{{ site.baseurl }}/assets/AngryBirds/angry-birds-cover.mp4" type="video/mp4">
</video>

A physics component handles the velocity of the object and collisions are checked on an update. Collisions are detected through two shapes: a circle and a rectangle (an axis-aligned bounding box). Collision resolutions are handled based on the side of the shape that was hit as well as the velocity of both shapes. On reflection this could be improved by reflecting the velocity of the shapes, so the side of the collision is not required.

<img src="{{ site.baseurl }}/assets/AngryBirds/angry-birds-game-2.jpg"/>