---
layout: post
title: "Adding FTUE and Audio"
date: 2022-03-06 18:00:00 +0100
tags: project-artefact
categories: [Symptoms Please Devlog]
---

### Tasks
- Focus on art design and look of project
- Design tutorial

### Summary
This week I mainly focused on the first time user experience of my project, how will users learn how to play the game. I started by simply adding some popups for when the user first plays the game, explaining what each secion of the UI does.

<p align="center">
  <img src="{{site.baseurl}}/assets/SymptomsPlease/ftue-symptoms.png" alt="FTUE Symptoms Popup"/>
  <img src="{{site.baseurl}}/assets/SymptomsPlease/ftue-actions.png" alt="FTUE Actions Popup"/>
  <img src="{{site.baseurl}}/assets/SymptomsPlease/ftue-advice.png" alt="FTUE Advice Popup"/>
  <img src="{{site.baseurl}}/assets/SymptomsPlease/ftue-information.png" alt="FTUE Information Popup"/>
  <img src="{{site.baseurl}}/assets/SymptomsPlease/ftue-test-kits.png" alt="FTUE Test Kits Popup"/>
</p>

These popups appear one after the other in quick succession at the very start of the game. What I realised after implementing is that this is a lot of information for the player to get in quick succession and I should give the player the information when it becomes relevant. For example I should show the symptoms popup when the symptoms show up for the first time, and show the actions popup when the player is expected to use them for the first time. 

By the end of the week I changed the FTUE to show at the relevent point rather than all at the start.

<video controls>
  <source src="{{ site.baseurl }}/assets/SymptomsPlease/ftue-video.mp4" type="video/mp4">
</video>

This week I also added started adding audio into the game by creating an audio manager and adding some simple sounds. I need to do another pass over the sounds at a later date and add in more sounds for different interactions as well, but what I've done is a good start.

Finally this week I had another meeting with Lloyd to show him the work I'd done since the demo. He liked what I showed him and gave some advice and feedback for the tutorial popups and advice I'd done. 

### Next Steps
- Add advice slip printouts
- Close popups on tap