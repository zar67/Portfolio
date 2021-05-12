---
layout: post
title: River Generation
date: 2021-05-9 12:00:00
category: [Tile Tap Devlog]
---

The plan for the two weeks is to implement the random river generation, before my planning I previously completed the task of generating random rivers, but the algorithm needs to be improved, I also didn't acomplish any way of clearly showing the rivers on the game. 

This is the first evolution of the algorithm, similar to the way I generate land, rivers are generated until the "riverBudget" runs out.

```c#
private int GenerateRiver(TileData origin)
{
    int length = 0;

    TileData currentTile = origin;
    HexDirection previousDirection = HexDirection.NW;
    while (!currentTile.HasRiver && currentTile.Terrain != TerrainType.Water)
    {
        currentTile.HasRiver = true;
        length++;

        if (currentTile != origin)
        {
            currentTile.RiverDirections.Add(previousDirection);
        }

        var validDirections = new List<KeyValuePair<HexDirection, TileData>>();
        foreach (var neighbour in currentTile.Neighbours)
        {
            if (neighbour.Value == null)
            {
                continue;
            }

            if (TileData.DirectionDifference(previousDirection, neighbour.Key) > 1)
            {
                validDirections.Add(neighbour);
            }

            validDirections.Add(neighbour);
        }

        int randomIndex = Random.Range(0, validDirections.Count - 1);
        var randomNeighbour = validDirections[randomIndex];

        currentTile.RiverDirections.Add(randomNeighbour.Key);
        currentTile = randomNeighbour.Value;
        previousDirection = TileData.ReverseDirection(randomNeighbour.Key);
    }

    return length;
}
```

The state of my rivers before any further development is brown dirt chunks all accross the map:

<img src="{{ site.baseurl }}/assets/Blog/TileTap2/river-generation-brown-blobs.png" alt="river generation brown blobs" style="width: 800px;"/>

The first step in displaying the rivers on the map was making sprites for all of the potenial river tiles, the Kenney asset pack I'm using has river tiles in them, but they are only ontop of grass and don't have all the possible combinations of rivers in them, so I created very simplistic river sprites to use for the minute.

Here are the river sprites for 3 directional river tiles:

<img src="{{ site.baseurl }}/assets/Blog/TileTap2/initial-river-sprites.png" alt="initial river sprites" style="width: 800px;"/>

The next task was to tediously enter in each river sprite and it's coresponding directions into the world sprite data. I had been already implemented before into the world sprite data I just needed to enter in each of the 63 sprites and which directions the river can flow in with that sprite.

<img src="{{ site.baseurl }}/assets/Blog/TileTap2/rivers-displaying-in-game.png" alt="displaying rivers in game" style="width: 800px;"/>

Now, these aren't the final sprites and I also need to sort out the sort order of the rivers so that they don't appear above other tiles, but the rivers are looking better now. 

I need to modify the algorithm so that the rivers are smoother and are more likely to go in a straight line. I also need to make the rivers longer in order to make them look better. However, these are all modifications I can make later when balancing the game. 