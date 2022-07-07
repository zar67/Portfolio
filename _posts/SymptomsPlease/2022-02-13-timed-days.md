---
layout: post
title: "Time Limited Days"
date: 2022-02-13 18:00:00 +0100
tags: project-artefact
categories: [Symptoms Please Devlog]
---

### Tasks
- Adding time limit into days

### Summary
After thinking about the gameplay and design of the game I have decided to go back to having a time limited day, this way players are encouraged to diagnose patients quickly to do better in the game. This makes sense then that using an STI kit takes more time - as players learn the STIs they will be able to diagnose them faster and be able to stop using the STI kits to help them diagnose patients. 

I've added a timer in the format of a cloak at the top of the UI which adds pressure to the player, making them aware of the time. Before the player had no sense of how far through the day they were, and therefore treating patients would become monotonous at the end of the day, now players are against the clock and so there is more time urgency. 

<p align="center">
  <img src="{{site.baseurl}}/assets/SymptomsPlease/day-clock-interface.png" alt="Clock interface on UI"/>
</p>

This week I also added in the logic to disable actions on the desk that aren't needed for any of the active afflications. This means that when the player starts the game there will be a very limited number of actions on the desk to choose from, therefore less overwhelming and easier for them to learn. 

### Next Steps
- Iterate on UI and flow of each day.