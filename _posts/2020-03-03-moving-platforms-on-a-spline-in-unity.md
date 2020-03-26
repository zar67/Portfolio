---
layout: post
title:  "Moving Platforms On A Spline In Unity"
date:   2020-03-03 12:00:00 +0000
categories: [Gameplay Programming Module]
---

After creating a 2.5D player on a spline for my Gameplay Programming module, we had to also implment platforms moving along a spline. We were tasked with building a system that allows a designer to use moving platforms in many different ways throughout their project. Here are the aims and objectives:

<img src="{{ site.baseurl }}/assets/Blog/GPMovingPlatforms/platforms_objectives.png"/>

I have decided that I want my system to be encapsulated into one script, with public options in the inspector for the user to change the way the platforms move. I will be using <a href="https://assetstore.unity.com/packages/tools/utilities/b-zier-path-creator-136082" target="_blank">Sebastian Lague's Path Creator Asset Pack</a> to create the splines for the player to follow.

The example we have been given is the Gloop River and Juju cave from <a href="https://youtu.be/vlEdrwaQjs8?t=159" target="_blank">Malice</a> which shows the player being able to jump on moving barrels floating down a river, the barells tip with the player's weight and obstacles will push the player off the barrel.

<h3>Moving Along A Spline</h3>

Setting up a spline with Sebastian Lague's path creator is quite simple, you place the positions of the anchor points and then can change the controls points and normals to what you want. 

I setup a simple spline in a 'lake' for some platforms to follow along.

<img src="{{ site.baseurl }}/assets/Blog/GPMovingPlatforms/spline_setup.png"/>

The actual movement for moving a platform along a spline is two lines of code:

```c#
    distance_travelled += controller.platformMoveSpeed * Time.deltaTime;
    transform.position = controller.spline.path.GetPointAtDistance(distance_travelled, controller.endInstruction);
```

The distance_travelled variable holds how far the platform has moved along the spline and increased that variable every update, then sets the new position of the platform based on the distance. 

This setup platforms 'floating' along the river. I also setup an end condition so when the platforms reach the end of the spline, they are destroyed. 

I also made public variables for the move_speed of the platforms and how far apart they should spawn so I could calculate the time delay between spawning each platform.

<h3>Mechanical Movement</h3>

Adding mechanical movement into the platforms as an option involved setting a timer and a distance for how far the platforms should move before they stop. Platforms will move for a certain amount of time, and then stop for a certain amount of time. As soon as the platforms start moving, a new platform is instantiated at the start of the spline.

```c#
    if (mechanicalMovement)
    {
        if (mechanical_move_timer > mechanicalDelay)
        {
            bool finished = false;
            foreach (MovingPlatform platform in platforms)
            {
                if (platform.MechanicalMove())
                {
                    mechanical_move_timer = 0;
                    finished = true;
                }
            }

            if (finished)
            {
                MovingPlatform new_platform = Instantiate(platformsPrefab, 
                                                          spline.path.GetPoint(0), 
                                                          Quaternion.identity, 
                                                          platformsParent).GetComponent<MovingPlatform>();
                new_platform.StartPlatform(this);
                platforms.Add(new_platform);
            }
        }
        else
        {
            mechanical_move_timer += Time.deltaTime;
        }
    }
```

<h3>Platform Tipping</h3>

To make the platform tip under the weight of the player, I got the difference between the player's position and the centre of the platform and rotated the platform in that direction. I allowed the user to change the rate at which a platform rotates and whether or not they want the platform to rotate at all.

```c#
    if (player != null && controller.rotateWithWeight)
    {
        Vector3 point = (player.transform.position - transform.position).normalized;
        weight_rotation += new Vector3(point.x * controller.tiltMultiplier, 
                                       0, 
                                       point.z * controller.tiltMultiplier);
    }
    new_rotation += weight_rotation;
    transform.rotation = Quaternion.Euler(new_rotation);
```

<h3>Adding Options</h3>

<img src="{{ site.baseurl }}/assets/Blog/GPMovingPlatforms/inspector.png"/>

These are the public options on my player movement script.

They allow the user to set a spline, an end instruction, a parent to instantiate all the platforms under and a platform prefab (which should have a moving platforms script attached to it).

Platforms can start on running the program, or be triggered by a switch (created in a previous task), they can also run forever, or stop after a delay.

The platforms can move two different ways, normally which gives a 'floating' affect, or which a mechanical movement, and values can be changed for both of these movements. There is also the option to set what rotation the platform should have. Below shows a video of all the platforms working at once, some start immediately, some are trigger and they also have different types of movement.

<div class="iframe-container">
<iframe src="https://www.youtube.com/embed/l1JEHufU6qw?list=PLFrr5q99QVCieQRuLbGoNbUDv7vbKVGF6" frameborder="0" allowfullscreen></iframe>
</div>