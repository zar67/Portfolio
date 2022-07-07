---
layout: post
title: "UI Rearragement"
date: 2022-02-20 18:00:00 +0100
tags: project-artefact
categories: [Symptoms Please Devlog]
---

### Tasks
- Iterate on UI and flow of each day.

### Summary
With switching back to time-limited days, the UI needed some more thought, both to be easier to use and also allow players to access information quicker.

Before starting on UI, I made some changes to the afflictions structure; I added each symptom as it's own scriptable object so data could be held for each one, for example a description and an icon. A lot of the symptoms for the STIs overlap and so having a scriptable object means they can be reused between afflictions. I also added the ability for symptoms to not be compatible with eachother, for example a person that has an irregular or heavy period won't also have testicle pain. 

<p align="center">
  <img src="{{site.baseurl}}/assets/SymptomsPlease/symptom-scriptable-object.png" alt="Symptom Scriptable Object Inspector"/>
</p>

I added in all the symptoms back into the afflictions and updated the code to use the sriptable objects instead of strings. This means in the future I can add icons and descriptions to each symptom and display them pretty easily.

Then I moved on to some bug fixing, the modifications weren't clearing properly one they had been displayed which turned out to be a simple fix.

Finally I got onto working on the UI; I started by splitting up the tablet into two popups, one to display the current patients information and one to display the information for all the active STIs. Since the day is now timed, having a list of patients for the day didn't seem right, as there is the possibility for an unlimited number of patients; in addition to this, it took 2-3 taps for the player to get to the information for the current patient, so having a separate patient popup has sped that process up and also made it simpler.

<p align="center">
  <img src="{{site.baseurl}}/assets/SymptomsPlease/new-tablet-popup-layout.png" alt="New Tablet Popup Layout Screenshot"/>
</p>

I also moved the feedback popups for when the player takes an action and the sti results popup to the top of the desk, as I didn't want them to block the player actions when they are shown.

<p align="center">
  <img src="{{site.baseurl}}/assets/SymptomsPlease/new-results-and-feedback-position.png" alt="New Test Results and Feedback Position Screenshot"/>
</p>

I changed the feedback popup to include more information about the action the player took, including the affliction the patient suffers from if they are cured. The feedback also includes a grade based on the effectiveness and the score gained from the action. In the future I want to improve the appearance of this dropdown more to look like a doctors note.

<p align="center">
  <img src="{{site.baseurl}}/assets/SymptomsPlease/feedback-improvements.png" alt="Feedback Improvements"/>
</p>

### Next Steps
- Focus on art design and look of project
- Design tutorial