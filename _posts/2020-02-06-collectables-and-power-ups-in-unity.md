---
layout: post
title:  "Collectables and Power Ups in Unity"
date:   2020-02-06 10:00:00 +0000
categories: Gameplay-Programming-Module
---

The next task set for my Gameplay Programming module is to implement two collectables (a double jump and a speed boost) into my project. Since I have already implemented a double jump into my Character Controller affecting the values on the player will be simple, but I will need to think about how to implement these collectables so that more can be implemented in the future. The aims and objectives for this task are shown below:

<img src="{{ site.baseurl }}/assets/Blog/GPCollectables/objectives.png"/>

It is important that I setup these collectables in a way that it is easy to make more of different types. I am planning on setting up a parent Collectable script which my double jump and speed boost powerups will inherit from. All of the collision and particle effects will be handled on the parent script while the specific gameplay changes will be handled on the individual child scripts.
The examples we have been given to look at are <a href="https://www.youtube.com/watch?v=h9dY6gv1hzA" target="_blank">Jak and Dexter</a> as well as <a href="https://www.youtube.com/watch?v=L2DDpMLijC0" target="_blank">Spyro</a>, these are the collectable effects we should be looking to implement.

<h3>Base Collectable</h3>

The base collectable will handle collision, the duration of the effect, any particles and re-spawning. There will also be virtual Pickup() and Disable() functions that will be overridden on the double jump and speed boost scripts.

Below is my implemented update function. If the powerup has been collected, then it will update the timer until the power up should be disabled. The object will also rotate while active to add to the look and feel of the collectable. Finally, if the object isn't active, and it is a collectable that can re-spawn, then the re-spawn timer will be updated until the timer ends and the object appears again.

<img src="{{ site.baseurl }}/assets/Blog/GPCollectables/base_collectable.png" />

On collision with the object, the Pickup() function is called, which will eventually alter the gameplay, the effect duration timer is set to 0 and the object is set inactive so it cannot be collided with again.
When the timer runs out, the object is set active again and the respawn timer is reset to 0.

<h3>Double Jump</h3>

After setting up the base collectable adding the power-ups in is quite simple, I created a new script that inherits from Collectable and added the Pickup() and Disable() functions. In this script I need to populate those functions with lines of code that affect player values. So, in the double jump script I set the boolean can_double_jump to true in Pickup() and to false in Disable().

<img src="{{ site.baseurl }}/assets/Blog/GPCollectables/double_jump.png" />

<h3>Speed Boost</h3>

Implementing the speed boost was just as easy, I setup the Pickup() and Disable() functions to be the following:

<img src="{{ site.baseurl }}/assets/Blog/GPCollectables/speed_boost.png"/>

<h3>Particles</h3>

I have decided to add three different particles to each collectable: default, pickup and player. 
Default particles will add effects to the collectable, like the rotation, while it is active and not collected. Pick up particles will play when the player collides with the collectable. Player particles will be instantiated on the player on collection and move with the player to indicate the power up, these will be deleted when the powerup runs out.
I will add a simple script to the pickup particles that deletes them when they stop playing. The default particles will be disabled when the collectable is, and the player particles will be deleted when the powerup timer ends. 
When the player collides with the particle the Collect() function is called:

<img src="{{ site.baseurl }}/assets/Blog/GPCollectables/particles.png"/>

<h3>UI</h3>

Implementing the UI timers for the collectables was tricky, since I needed a way to reset the timers if a new power up of the same type was collected. I found that if I added a DoubleJump and SpeedBoost variable to the player controller, this allowed me to keep track of what power ups were active on the player. 

This also made it a lot simpler for me to integrate my speed boost with my strafing, just by checking if SpeedBoost was null or not and setting the speed accordingly. 

I used images for my timers and set them to have an image type of "filled" meaning I could set the fill amount and they would count down like a timer clockwise (as seen in the video below).

I also wanted to update the position of the timers so that they always occurred in the bottom left and if one timer ran out the next would move over. I set this up by always having the double jump first, and if there is a double jump active on the player, move the speed boost timer over by an offset.

I did all this on a new UICollectables script, the update function on that looks like this:

<img src="{{ site.baseurl }}/assets/Blog/GPCollectables/ui.png"/>

After implementing all this, I have an expandable collectable system which I can quite quickly add new and different power ups to, with working visuals to indicate to the player what power ups they have.

<div class="iframe-container">
<iframe src="https://www.youtube.com/embed/jAmGZBbe97A" frameborder="0" allowfullscreen></iframe>
</div>

<h3>Improvements</h3>

The main improvement I could make would be to add models into the collectables, so that they aren't just floating squares. I think this would help to identify which powerup is which. I could also change the sprites of the timers. 