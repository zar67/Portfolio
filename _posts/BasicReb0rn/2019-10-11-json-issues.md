---
layout: post
title: JSON Issues
date: 2019-10-11 12:00:00
category: [Basic Reb0rn Devlog]
---

In order to get the data for the rooms, objects and actions (words) into the game, I decided to use JSON. You can see below the structure for the three json objects I will need. I will use 3 files, one for actions, one for objects and one for rooms.

<br>
<h3>Actions</h3>
```json
    ACTION
    {
        "ID": 0,
        "Verb": "HELP",
        "Object": -1,
        "Required Objects": [-1, -1, -1],
        "Required Room": -1,
        "Response": ""
    }
```
For the actions, I need the following information:
* ID - unique idenifier for the action.
* Verb - the word for the specific action.
* Required Objects - the second word that refers to an object (-1 for no object needed, 0 for any object).
* Required Objects - objects the player needs to have in their inventory for the action to be completed (-1 if no objects needed). There needs to be at least 3 items in this array because the candle needs 3 objects to be lit.
* Required Room - needed if the action can only be called from a specific room (-1 means any room).
* Response - the output that should be given if the action is completed.

<br>
<h3>Object</h3>
```json
    OBJECT
    {
        "ID": 1,
        "Name": "PAINTING",
        "Description": "A creepy painting",
        "Collectible": true,
        "Hidden": false
    } 
```
For the objects:
* ID - unique identifier.
* Name - the name of the objects, this will be typed by the player when doing anything with the object e.g. EXAMINE PAINTING.
* Description - The given output when the player examines the object.
* Collectible - Whether the object can be picked up and put into the player's inventory.
* Hidden - Whether the object is hidden (used for the key and the candle).

<br>
<h3>Room</h3>
```json  
    ROOM
    {
        "ID": 0,
        "Name": "DARK CORNER",
        "Exits": [false, true, true, false],
        "Items": [-1, -1, -1, -1, -1]
    } 
```
For the rooms:
* ID - unique identifier.
* Name - the named displayed to the player.
* Exits - Booleans determining the N, E, S, W exits of the room.
* Items - The objects currently in the room, limited to a maximum of 5 objects.

<br>
I loaded these files into the game and put the data into classes that hold the data. If the game is restarted at any point, the data is recollected from the files.

I had some issues with the JSON files being changed to include random characters whenever I edited the them, and on random occasions when I ran the game. This wasn't good because the game then created an error and wouldn't run. I tried many things to fix this, like changing the encoding of the JSON files, rewriting them and switching between .txt and .json. 
Finally, I ended up realising that I needed to pass both the first and last parameters of the parse function by using buffer.as_char() and buffer.length. So, this is what my code looks like now:

```cpp
    // Get file data
    using Buffer = ASGE::FILEIO::IOBuffer;
    Buffer buffer = file.read();
    file.close();

    // Read file data as JSON
    auto file_data = nlohmann::json::parse(buffer.as_char(), buffer.as_char() + buffer.length);
```

This fixed my issue due to buffer.length() getting the exact size of the file, excluding any hidden or encoding characters.
JSON files now load correctly each time I run the program and I can now use the data in the game.