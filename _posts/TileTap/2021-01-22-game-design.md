---
layout: post
title: The Design
date: 2021-01-22 12:00:00
category: [Tile Tap Devlog]
---

The first step to creating the new and improved Tile Tap was to define some game design aspects, I did this by setting up a combined GDD and TDD to outline what I wanted to game to look, feel and be. 

I know the first thing I want to setup is the UI for the game, so included in my documentation I made a UI flow chart to layout the  design I want.

<img src="{{ site.baseurl }}/assets/Blog/TileTap2/ui-layout.png" alt="ui flow chart"/>

The goals of the game are: 
- Grow and Expand
- Collect
- Trade and Collaborate

<br>
The main mechanics of the game will be: build, explore, fight, trade.

<h3>Build</h3>
The player should be able to, build, demolish and move buildings. Buildings cost resources to build and will produce different resources for the player. 
Some buildings may only be placed on specific tiles, they could also be less effective on some tiles.

<h3>Explore</h3>
The player should be able to send troops to explore the land, the map will be covered with a fog of war until discovered by a unit.
The map will be randomly generated but should have biomes with different types of terrain for the player to explore and use for resources.

<h3>Fight</h3>
Enemies such as predators or barbarians may be roaming in the wild and the player will enter into combat to defeat them. There will be a simple attacking system where the player will lose or win based on the strength of their units. A more in depth turn based attacking system could be implemented, but this is a stretch goal.
 
<h3>Trade</h3>
The player should be able to add friends and trade with them for resources in a similar way to Settlers of Catan.
There should also be some AI trading so that the player can play without friends and still benefit from the trading system.

<br>
So, the next steps are to add UI into the game and get started on development.