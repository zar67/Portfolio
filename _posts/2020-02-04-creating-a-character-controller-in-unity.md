---
layout: post
title:  "Creating a Character Controller in Unity"
date:   2020-02-04 10:00:00 +0000
categories: Gameplay-Programming-Module
---

​As part of my Gameplay Programming module I have been tasked with creating a character controller in Unity. We have been told to use the <a target= "_blank" href="https://assetstore.unity.com/packages/3d/animations/rpg-character-mecanim-animation-pack-free-65284">RPG Character Mechanim Animation Pack</a> (the free version) to implement our character, which will give us a character model as well as a collection of animations to use. The pack also has a character controller included to give us an example of what we should implement.
The main requirements I need to implement are standing, walking, jumping and attacking. The specification brief is below:

<center><img src="{{ site.baseurl }}/assets/Blog/GPAvatar/objectives.png" style="height: 300px;" /></center>

As stated, this character controller will form the foundations of my work for the module, therefore I will need to make sure that my avatar is flexible and can adapt easily as I add more features to the project.

<h3>Basic Movement</h3>

Adding basic movement for a character in Unity is something that is well documented on the internet and can be implemented several different ways, each with their own benefits and draw backs. I have decided to use Rigidbody physics to move my character, mainly because most of the needed collision checks are already done by the physics and Rigidbody.

My first step is to study and try and figure out the character controller included with the pack. The following video is the result of that character controller and is what I will be aiming towards:

<iframe width="100%" height="500" src="https://www.youtube.com/embed/3uCGkeJHhJY" frameborder="0" allowfullscreen></iframe>

So, starting with the basic movement of moving around the space, I created a blank script to work from. I added some basic movement variables to keep use like movement speed and rotation speed and then got to work on the inputs. The "horizontal" and "vertical" axis are already setup in Unity to work for both controller and keyboard, so I decided to use those for my movement. This was quite simple to set up, I changed the velocity of my character based on the horizontal and vertical input given.

<center><img src="{{ site.baseurl }}/assets/Blog/GPAvatar/movement.png" style="height: 100px;" /></center>

This got my character moving around the screen, but obviously this didn't implement any animations. So, I added an animator and a couple variables that I update within my script.

<center><img src="{{ site.baseurl }}/assets/Blog/GPAvatar/animator.png" style="height: 250px;" /></center>

I also added in a "strafe" animation, where if the left trigger is pressed, the player strafes in the direction they're moving in (essentially moves slower). I did this simply by adding the animation and setting a boolean value called "strafe" depending on whether the trigger is pressed or not.

<h3>Camera</h3>

The next thing I need to implement in order to properly test my character controller is a basic camera that follows the player, I will need to also change the movement of the player so that it is relative to the point of view of the camera. For example, when the analog stick is moved down, the player should always move towards the camera. This is possible with LookRotation() and Slerp().

<center><img src="{{ site.baseurl }}/assets/Blog/GPAvatar/camera_rotation.png" style="height: 300px;" /></center>

<h3>Jumping</h3>

Jumping is more complicated to implement than movement; there is the jump, the falling and the landing. I also want to implement a double jump, which can only happen if you're already jumping and can only happen once per jump.

FixedUpdate() is used in Unity to handle physics, however input actions like GetButtonDown() can be unreliable in FixedUpdate(). Therefore I need to detect input and set boolean values in Update() and then apply the changes I want in FixedUpdate() if the booleans are true. My code so far looks like this:

<center><img src="{{ site.baseurl }}/assets/Blog/GPAvatar/jump_update.png" style="height: 350px;" /></center>
<center><img src="{{ site.baseurl }}/assets/Blog/GPAvatar/jump_fixed_update_1.png" style="height: 500px;" /></center>
<center><img src="{{ site.baseurl }}/assets/Blog/GPAvatar/jump_fixed_update_2.png" style="height: 350px;" /></center>

My jumping definitely isn't perfect, there are still bugs and tweaks that could be made to make it smoother, however, I'm currently happy with my implementation and I'm limited on time, so I'm going to move on to the attacking.

<h3>Attacking and Weapon Arming / Disarming</h3>

The attacking system on the example character controller is quite complicated, with many different weapons for the player to use. In the free version the only weapon included is the two-handed sword, and so I will only need to implement this into my character controller. However, I will try to set it up so that more weapons can easily be added in future. 
I started by adding a simple punch when the X button is pressed on the controller, I did this on a separate animation layer with an avatar mask so that the punch animation would be played and the player could still move and jump at the same time. 
After implementing a basic attack, I decided I wanted to try and implement an arming / disarming system like the one in the example. Since the only weapon available in the free pack is the two-handed sword, I had the player automatically carrying the sword on their back. When the player presses wield (Y), the sword on the back is disabled and there is a sword on the player's hand which is enabled to give the illusion of the player taking the sword from their back.
The animations for the two handed sword are similar to the unarmed animations, but I wanted to include them when the player was armed. To do this I created a new animation layer and turned on "sync" with the base layer, this meant that all the animation states and transitions were copied to the new layer and I just had to replace the animations. In order to switch between the two layers, I change the layer weight of the armed layer so it overrides the unarmed layer.
I also added another armed layer for attacking, so that when armed the player attacks with the sword. This gave me four animation layers in total: Base Layer, Armed Layer, Attack Unarmed, Attack Armed.
I decided that if the player has not attacked in a certain amount of time (5 seconds) the character will automatically put their sword away. 

<center><img src="{{ site.baseurl }}/assets/Blog/GPAvatar/arming.png" style="height: 400px;" /></center>

After this I also added in a kick to the player. I did this in a similar way to the punching, with a new animation layer, but set the avatar mask to only include the legs, so that the player could kick while doing other animations. 

<iframe width="100%" height="500" src="https://www.youtube.com/embed/-xQArwWi6Og" frameborder="0" allowfullscreen></iframe>

<h3>Remaining Bugs</h3>

There are obviously still some bugs with this character controller which I intend to improve on throughout the module.

1. Landing isn't as reliable as I'd like it to be, I'm detecting when the player lands based on a Physics.CheckSphere() which will give me if the player is colliding with anything on a certain layer mask, however this doesn't always seem to detect correctly and the player slides along the ground for a small time.
2. When the player moves down a ramp he falls, rather than walking down the ramp as would be expected, this is because when the player is moving forward and the ground goes down, the character is no longer grounded and so thinks they are falling. 
3. Since there is one capsule collider on the player, the arms and sword quite often move into walls and other objects. This could be solved with additional colliders on the arms and sword. These extra colliders couldn't be mesh colliders though, since mesh colliders and rigid bodies cannot be used together.

<h3>Improvements</h3>

There are still a few animations that I have left to include and demonstrate. I have added in a death animation, which will come in useful later in the module. The other included animations which I could implement to improve the character, as well as bug fixes, are being hit, rolling, stunned and the character being revived. 