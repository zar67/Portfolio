---
layout: post
title: Resources Setup
date: 2021-05-09 12:00:00
category: [Tile Tap Devlog]
---

My tasks for this week are related to the Resources in the game, I need to setup the base Resources data and start the setup for Tiles generating Resources as well.

The Resources I'm planning to have in the game are:
* Wood
* Stone
* Food
* Metal


In functionality, Resources will be VirtualCurrency, with the ability to add and remove from the resources.

Firstly, I setup the resources data by creating a derived class of VirtualCurrency called VirtualResource and created an object for each of the resoucres I want to have. I then realised I didn't have any of the RowbotTools currency system setup, and so I spent some time setting up that as well to have the currency loading and saving correctly.

VirtualResources have a base regeneration time to determine how long until a new resource is generated.

<h3>Resource Tiles</h3>
Tiles that generate resources need to have a designated resource and a generation time. Users also need to have a way to collect from the tiles, eventually this will be with buildings and units, currently since I have no buildings or units I will just check the resources are generating by automatically collecting them when they generate.

In order to specify tiles that have a resource, I need to link a tile sprite to a resource and an amount, and so I added into the WorldSpriteData object this information.

<img src="{{ site.baseurl }}/assets/blog/TileTap2/resources-sprite-data.png" alt="world data values" style="width: 800px;"/>

I am thinking of reworking this at some point in the future, since it is not very user friendly and it may be beneficial to create individual tile objects (potentially included into the prefab or potentially on it's own) to handle this data in a better way.

But, moving on, I could then use this information to start generating resources. I setup an IEnumerator to handle the resources:

```c#
private IEnumerator GenerateResource()
{
    while (true)
    {
        m_resourceGenerationTimePassed = 0;

        while (m_resourceGenerationTimePassed < m_tileData.Resource.RegenerationTime)
        {
            m_resourceGenerationTimePassed += Time.deltaTime;
            yield return null;
        }

        m_tileData.Resource.Add(m_tileData.ResourceGenerationAmount);
    }
}
```

This is called from the tile initialisation function, but only if the tile actually has a resource there's not much point in call it otherwise...

If you watch the numbers in the top left of this video you can see two going up, this is the Wood and Stone resource which are being generated from forest and stone tiles. They increase in value so much because I'm collecting from all the tiles on the map automatically.

<video controls>
  <source src="{{ site.baseurl }}/assets/blog/TileTap2/resource-generation-video.mp4" type="video/mp4">
</video>