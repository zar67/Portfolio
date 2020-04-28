---
layout: post
title:  "Putting It All Together"
date:   2020-04-22 12:00:00 +0000
categories: [Gameplay Programming Module]
---

As the final task in our Gameplay Programming module, we have to put all of our work together and (in a group) create a game demo showcasing the gameplay features we've implemented so far.
​This is the specification:

<img src="{{ site.baseurl }}/assets/Blog/GPGroupWork/group_objectives.png"/>

We got our group together and decided on the gameplay and areas we wanted to create. We set tasks for each person depending on their skills with each gameplay feature. ​Our brief design documentation can be found here.
I was tasked with creating the mine system using my gameplay on a spline code and contributing my arming and disarming code for the player.
We setup a github repository and got to work. I imported some simple assets to make the mine with aswell as the Spline Creator I used for my spline work. I setup a scene with corridors and caves similar to the map seen on our documentation.

<img src="{{ site.baseurl }}/assets/Blog/GPGroupWork/level_overview.png"/>

<h3>Splines</h3>

I setup the splines I needed along the corridor and setup the minecart to move along them when actived similar to my moving platforms. I also setup the player to get into and activate the minecart when they press X and are in range. The player is set to be a child of the minecart when they get in so that they rotate with the cart.

<img src="{{ site.baseurl }}/assets/Blog/GPGroupWork/minecart_on_splines.png"/>

At the end of a spline the minecart is stopped. The player can get back in the minecart and the direction of the minecart will reverse so the player can go back to the start. 

<h3>Leaning</h3>

I set the leaning simply by Lerping the position and rotation of the minecart whenever the player moves the left analog stick left or right.

``` c#
if (Input.GetAxis("Horizontal")) < -0.1f)
{
    trackController.tiltPositionOffset = Vector3.Lerp(trackController.tiltPositionOffset, maxTiltPosition, tiltSpeed * Time.deltaTime);
    trackController.tiltRotationOffset = Vector3.Lerp(trackController.tiltRotationOffset, maxTiltRotation, tiltSpeed * Time.deltaTime);
    tiltController.tiltDirection = trackController.direction;
}
if (Input.GetAxis("Horizontal")) > 0.1f)
{
    trackController.tiltPositionOffset = Vector3.Lerp(trackController.tiltPositionOffset, maxTiltPosition, tiltSpeed * Time.deltaTime);
    trackController.tiltRotationOffset = Vector3.Lerp(trackController.tiltRotationOffset, -maxTiltRotation, tiltSpeed * Time.deltaTime);
    tiltController.tiltDirection = trackController.direction;
}
else
{
    trackController.tiltPositionOffset = Vector3.Lerp(trackController.tiltPositionOffset, Vector3.zero, tiltSpeed * Time.deltaTime);
    trackController.tiltRotationOffset = Vector3.Lerp(trackController.tiltRotationOffset, Vector3.zero, tiltSpeed * Time.deltaTime);
    tiltController.tiltDirection = 0;
}
```

<h3>Junctions</h3>

I setup junctions as separate objects to the splines, which I could place where ever I needed too. I setup a clear indication of where a split in the track is for the player and setup a collider. If the minecart is in range of the collider and the player is leaning in the correct direction then the minecart will swith to the other spline and carry on.

<img src="{{ site.baseurl }}/assets/Blog/GPGroupWork/junction.png"/>

I set the junction to have public variables so I could place it in different situations and control which splines to look at and the directions required like the lean direction and the movement direction.

<h3>UI and Incentives</h3>

In order to teach the player about the splines I setup some UI and some incentives (coins) for the player to learn about the minecart systems.
The first UI setup tells the player to press X to either get in or out of the minecart:

<img src="{{ site.baseurl }}/assets/Blog/GPGroupWork/get_in_ui.png"/>

The second UI setup tells the player to use the left analog stick to lean left and right. This tutorial UI disappears when the player first leans.

<img src="{{ site.baseurl }}/assets/Blog/GPGroupWork/lean_ui.png"/>

<h3>Enemies</h3>

I decided to add a few Cave Spiders into the area I created to add interest to the level and give the player some combat to deal with while searching for the key to escape the level with.

<img src="{{ site.baseurl }}/assets/Blog/GPGroupWork/spider.png"/>

<h3>Integration</h3>

By using Github and separate scenes the intergration of all of our work together was pretty simple. Each scene just needed to open the next one when it was done. The integration between my spline system and the player character was simple, but needed some tweaks to make everything work smoothly together. By integrating everyone elses work, I also needed to manoeuvre the coins and various gameobjects to accomodate for the player character compared to the temporary blank cube I had been using previously.

<div class="iframe-container">
<iframe src="https://www.youtube.com/embed/Z9lnLGAP7jw" frameborder="0" allowfullscreen></iframe>
</div>