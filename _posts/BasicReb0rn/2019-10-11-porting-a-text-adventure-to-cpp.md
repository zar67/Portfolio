---
layout: post
title: Porting A Text Adventure To C++
date: 2019-10-11 10:00:00
category: [Basic Reb0rn Devlog]
---

<h3>Planning</h3>

My first step in developing the C++ port of Basic Reb0rn was to get my documentation started. I setup a basic GDD and TDD with information from the book and my plans for the game. By reading through the book, I learned alot more about the design of the game that I did by simply copying the BASIC code. 

I outlined the structure and game flow in my documentation, these will likely change as the development of this project continues. My initial plan for the objects of the game is shown in the class diagram below.

<img src="{{ site.baseurl }}/assets/BasicReb0rn/c++-port-class_diagram.jpg" alt="class diagram for the C++ port"/>

In my GDD I outlined what I wanted to improve about various features as they were documented. Such as:
* Using the arrow keys for movement
* The addition of a menu and game over screen
* Changing the bats and ghosts so that the player can leave the room the way they came in, but that is the only action they can do until they defeat the bats and ghosts.
* Improvement of the boat and marsh system

<h3>Map Design</h3>

In my documentation I also laid out the words, map and objects that will be in the C++ version of the game. The map of the house can be seen below.

<img src="{{ site.baseurl }}/assets/BasicReb0rn/house-map.jpg" alt="haunted house map"/>

<h3>JSON Troubles</h3>

I will also be loading in the rooms, words and objects through JSON files since they are easily editable and easy to read. There is a JSON library included in the boilerplate code which allows me to retrieve information from JSON files.

In order to get the data for the rooms, objects and actions (words) into the game, I decided to use JSON. You can see below the structure for the three json objects I will need. I will use 3 files, one for actions, one for objects and one for rooms.

<h4>Actions</h4>
```json
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

<h4>Object</h4>
```json
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

<h4>Room</h4>
```json  
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