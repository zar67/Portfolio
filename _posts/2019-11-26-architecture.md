---
layout: post
title: Project Architecture
date: 2019-11-26 14:00:00
category: The-Shining-Devlog
---

This is the basic UML for our game. I tried to include as much information as I could for us all to look at, however the structure and attributes are likely to change as we develop our code. 

<img src="{{ site.baseurl }}/assets/Blog/ShiningDevlog/gameobject_uml.png" alt="project uml"/>
<img src="{{ site.baseurl }}/assets/Blog/ShiningDevlog/main_uml.png" alt="project uml"/>

I tried to think about the basics of what each class would need for the system to run, for example I know the SceneManager will need to know which screen is open, but I don't know what other variables and methods I will need just yet. I will update the UML as our project progresses we have a better understanding of what we need.

Next I will be starting to code the random room generation.