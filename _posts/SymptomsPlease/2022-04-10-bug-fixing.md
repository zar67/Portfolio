---
layout: post
title: "Bug Fixing"
date: 2022-04-10 18:00:00 +0100
tags: project-artefact
categories: [Symptoms Please Devlog]
---

### Tasks 
- Fix bugs made clear in the user testing

### Summary
I received some bugs from the user testing which I decided to fix before completing the project. The main bug was that sometimes patients wouldn't generate. This was because of the way I was storing patients in the save system. Instead of using an ID, I simplified the system by just saving the whole patient data in the appointment event. This was fine since the patient data isn't needed to be stored anywhere else except in events. 

I also finally added in the correct questions into the training section instead of the placeholder questions I had. I added a score to answers so the player gains score which is added to their leaderboard. 

<img src="{{site.baseurl}}/assets/SymptomsPlease/training-questions.png" alt="Training Questions"/>

Also, since I never managed to get around to creating or sourcing icons for the symptoms, I updated the symptoms descriptions to be more descriptive rather than just a copy of the display name.

Finally I did a whole pass of the UI to move away from using the default unity UI sprites and make the whole UI cohesive with each other.

<img src="{{site.baseurl}}/assets/SymptomsPlease/new-ui" alt="New UI"/>

### Next Steps
- Finish writing report