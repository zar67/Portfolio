---
layout: post
title: BASIC Text Adventure
date: 2019-10-01 16:00:00
category: [Basic Reb0rn Devlog]
---

<img src="{{ site.baseurl }}/assets/Blog/BasicRebornDevlog/book_cover.jpg" alt="book cover"/>

As part of our ESD module at univeristy we were given the book [Write Your Own Adventure: Programs for You Microcomputer](https://www.amazon.co.uk/Write-Your-Own-Adventure-Microcomputer/dp/0686878329) in order to reproduce the text adventure inside using the BASIC implementation. 

Our first task was to get the code in the book up and running using an online [BASIC Emulator](https://www.calormen.com/jsbasic/). It took me about 3 hours to copy all the lines of code and get it up and running properly. The code was very terious to copy as it is full of one letter variables.

My biggest mistake was not reading the little information bubbles to the side of the code that helpfully gave you information on changing the code for the type of emulator you're using or explaining how the code works.

My second mistake was just my typing ability; there were many mis-spelled variables. Specifically, when I ran the game, I encountered an error where I could go East when there wasn't an exit East. I found out that I had just simply typed in the wrong letters where the room exits were defined, so East and West were muddled up.

After a bunch of small fixes, and some reformatting of print statements for my own benefit (and sanity), the text adventure worked.

<img src="{{ site.baseurl }}/assets/Blog/BasicRebornDevlog/gameplay.jpg" alt="start of gameplay"/>

My next task is to implement this game in C++ using Object Oriented Programming and other modern coding techniques.