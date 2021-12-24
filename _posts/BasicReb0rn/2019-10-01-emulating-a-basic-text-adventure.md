---
layout: post
title: Emulating a BASIC Text Adventure
date: 2019-10-01 16:00:00
category: [Basic Reb0rn Devlog]
---

<img src="{{ site.baseurl }}/assets/BasicReb0rn/book_cover.jpg" alt="book cover"/>

For my Low Level Programming module at UWE we were tasked with emulating and porting the game in [Write Your Own Adventure: Programs for You Microcomputer](https://www.amazon.co.uk/Write-Your-Own-Adventure-Microcomputer/dp/0686878329). 

The first task was to emulate the game in the book using an Applesoft BASIC emulator like [Calormen](https://www.calormen.com/jsbasic/). It took a good couple hours to copy all the lines of code and fix the errors to get the code running correctly. The code was also very tedious and difficult to copy due to all the one letter variables.

My biggest mistake was not reading the little information bubbles to the side of the code that helpfully give information on changing the code for the type of emulator you're using and explain how the code works.

My second mistake was just my typing ability; there were many mis-spelled variables. Specifically, when I ran the game, I encountered an error where I could go East when there wasn't an exit East. I found out that I had just simply typed in the wrong letters where the room exits were defined, so East and West were muddled up.

After a bunch of small fixes, and some reformatting of print statements for my own benefit (and sanity), the text adventure worked.

<video controls>
  <source src="{{ site.baseurl }}/assets/BasicReb0rn/basic-Gameplay.mp4" type="video/mp4">
</video>