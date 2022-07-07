---
layout: post
title: "Adding an Online Leaderboard"
date: 2022-01-16 18:00:00 +0100
tags: prototype
categories: [Symptoms Please Devlog]
---

### Tasks
- Start Work On Leaderboard
- Ensure app meets demo requirements

### Summary
This week I began by setting up an online leaderboard, I had a look at multiple options for doing this including writing a Python Flask server. I eventually decided on using Firebase. Firstly I needed to create each user using Firebase Authentication, I generated an email from the username and used a static password of 123456, since none of the users need to log in. I can always change this later to have the users enter an email and password, but since my target audience is secondary school children, having no login is probably the best option.

<p align="center">
  <img src="{{site.baseurl}}/assets/SymptomsPlease/firebase-auth.png" alt="Firebase Authentication Page"/>
</p>

Then the data of each user is stored under their unique UID in Firebase Database, the data includes their username, score and whether they have enabled online access, for privacy purposes. Users that haven't enabled online access they won't be able to see the leaderboard and their name won't come up on the leaderboard other player's see.

<p align="center">
  <img src="{{site.baseurl}}/assets/SymptomsPlease/firebase-database.png" alt="Firebase Database Page"/>
</p>

The "valid_name" field of the database contains all the unused usernames, when a new user is created one of these names is selected. When a user takes a username it's removed from the valid names list. When a user changes their name, the old name is put back into the valid names list and the new name removed, the users email is also updated to reflect the new name.

### Next Steps
- Meet with Lloyd to discuss Demo requirements
- Prepare for Demo