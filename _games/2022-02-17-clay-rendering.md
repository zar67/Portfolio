---
layout: game
title: "Clay Rendering"
icon: "ClayRendering/icon.png"
date: 2022-02-17 12:00:00 +0000
publish: true
project-type: student
software-used: "Visual Studio"
game-engine-used: "Unity"
languages-used: ShaderLab
code-repository: <a href="https://github.com/zar67/AT-clay-rendering" target="_blank">GitHub</a>
tags: [AT, Coursework, Unity, ShaderLab]
---

As part of my third year of university I was tasked with creating a realistic clay shader, the task was suggested by Aardman Animations to develop a way to create a realistic clay material for use in digital claymation. 

This task greatly challenged me as I was not familiar with shaders or graphics programming before this, except for the <a href="https://zar67.github.io/Portfolio/games/2021-11-18-firectx-fps.html">DirectX FPS</a> task we had been previously assigned. 

Through this task I now know much more about PBR materials and how they work, I found <a href="https://learnopengl.com/PBR/Theory" target="_blank">LearnOpenGL</a> very useful for learning about physically based rendering. The shader uses the layered BRDF proposed by Weidlich and Wilkie and uses the Torrance-Sparrow BRDF for each layer.

<img src="{{ site.baseurl }}/assets/ClayRendering/unity-screenshot.png"/>

More information in how I developed the game can be found in the video logs <a href="https://youtube.com/playlist?list=PLFrr5q99QVCgQ9nvAoHRC83NKl4EfjXSu" target="_blank">here</a>.

The final report of the project can be found <a href="{{site.baseurl}}/assets/ClayRendering/ClayRendering-Report.pdf" target="_blank">here</a>.

<img src="{{ site.baseurl }}/assets/ClayRendering/torus-material.png"/>