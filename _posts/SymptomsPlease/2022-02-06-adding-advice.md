---
layout: post
title: "Adding Advice Action"
date: 2022-02-06 18:00:00 +0100
tags: project-artefact
categories: [Symptoms Please Devlog]
---

### Tasks
- Add In Advice Action for Player
- Implement the difficulty curve by adding more STIs to handle. 

### Summary
I started this week by adding in a way to activate different topics on certain days, I added in a way to do this through the modifications sciptable object I already had. I added in a description to the activation to give some more information to the player, which currently constist of puns and jokes related to each STI as they are displayed in a social media style.

<p align="center">
  <img src="{{site.baseurl}}/assets/SymptomsPlease/modification-day-activations.png" alt="Topics Activated On Certain Days"/>
</p>

<p align="center">
  <img src="{{site.baseurl}}/assets/SymptomsPlease/modifications-activation-display.png" alt="Day Start Screen With Active Modifications"/>
</p>

This gives me the beginnings of a difficulty curve as the longer the user plays, the more STIs they have to identify and treat in patients. 

Next I added in an information popup for afflictions (STIs), so they when they are activated, the player can open the popup and gain some more information about the STI they are going to encounter, this should give them a starting point to remmbering the symptoms of each STI.

<p align="center">
  <img src="{{site.baseurl}}/assets/SymptomsPlease/sti-information-popup.png" alt="STI Information Popup"/>
</p>

I also added in the advice action I wanted to add, for more complex situations or for afflictions that have a custom action that shouldn't realistically be placed on the desk. For example, the treatment for pubic lice is to buy some special shampoo from a pharmacy, a sexual health clinic may have this on hand, but it is also likely that they would direct the patient to a pharmacy instead.

<p align="center">
  <img src="{{site.baseurl}}/assets/SymptomsPlease/advice-book-popup.png" alt="Advice Book Popup"/>
</p>

### Next Steps
- Adding time limit into days