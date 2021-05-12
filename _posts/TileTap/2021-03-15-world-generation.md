---
layout: post
title: World Generation
date: 2021-03-15 12:00:00
category: [Tile Tap Devlog]
---

To generate a random world I need two main classes: TileData and WorldData. 

<h3>World Data</h3>
WorldData is a ScriptableObject and has members to modify the generation of a world with different values. The WorldData object will also have the Generate() function to make a new world and store the TileDatas that belong to that world. 

Here's the pseudocode for the world generation:
```
func Generate(int width, int height)
    set Tiles as empty list of TileData
    for int in width
        for int in height
            CreateNewTile()
            SetTileNeighbours()
            AddTileToTiles()
        end for
    end for

    set landBudget = (int)(width * (float)height * m_landPercentage);

    while landBudget > 0
        landBudget = GenerateLandChunk()
    end while
end func
```

The values that can be changed in the inspector modify how the generate function works:
<img src="{{ site.baseurl }}/assets/Blog/TileTap2/world-data-inspector.png" alt="world data inspector"/>

<h3>TileData</h3>
When the WorldData generates a new world it stores a list of tiles as TileData, the WorldData object does not handle the instantiating of the world, only generating the data for it and so holds the TileData it generates.

The core of the TileData class resides in the HexCoordinates HexMatrics structs. These handle the positioning and the size of the tile. 

<h4>HexCoordinates</h4>
On a traditionl 2D grid there are the X and Y axis which determine the coordinates of a cell, in a hexagonal grid there also needs to be a Z axis. 

In my implementation the axis are as follows:
- X is the horizontal axis, where 0 is on the left and increases to the right
- Y is the vertical axis, where 0 is on the bottom and increases up
- Z is the diagonal axis, where 0 is the bottom left and increases to the top right.

<br>
Along with the coordinates there is a HexDirections enum is used to determine neighbours and contains the values NE, E, SE, SW, W, NW.

<h4>HexMatrics</h4>
The HexMatrics class determines the size of the tile using the outer radius and calculating the inner radius.

<img src="{{ site.baseurl }}/assets/blog/TileTap2/hex-matrics.png" alt="hex matrics"/>

```c#
public HexMatrics(float outerRadius)
{
    OuterRadius = outerRadius;
    InnerRadius = outerRadius * 0.866025404f;
}
```

<h3>World Instantiater</h3>
The WorldData scriptable object holds all the information about the generated tiles, the WorldInstaniater component uses the WorldData to instantiate a tile prefab and create the world in the scene.

Here is the world instantiated into the scene, currently I make each land chunk a random terrain type this gives the illusion of biomes, however I will be implementing a more realistic biomes system.
<img src="{{ site.baseurl }}/assets/blog/TileTap2/world-map-generation.png" alt="world map generation"/>