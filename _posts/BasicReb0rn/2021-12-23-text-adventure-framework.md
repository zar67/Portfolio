---
layout: post
title: Text Adventure Framework
date: 2021-12-23 18:00:00
category: [Basic Reb0rn Devlog]
---

Since making my initial C++ version of Basic Reb0rn, I wanted to improve the structure to create a framework where creating new text adventures was relatively simple. The main task in order to do this was to get events being read in and triggered correctly. 

Rooms and Items will be similar to that of the original C++ port with slight modifications. 

<h3>Rooms</h3>

```json  
    {
      "ID": 0,
      "NAME": "DARK CORNER",
      "DESCRIPTION": "A DARK SPOT COVERED IN VINES AND MOSS",
      "IS_START": false,
      "IS_END": false,
      "EXIT_NORTH": false,
      "EXIT_EAST": true,
      "EXIT_SOUTH": true,
      "EXIT_WEST": false,
      "X_INDEX": 0,
      "Y_INDEX": 0
    }
```

<h3>Items</h3>

```json  
    {
      "ID": 0,
      "NAME": "OIL PAINTING",
      "VALUE": 500,
      "METADATA": 0,
      "SHOW_METADATA": false,
      "VISIBLE_TEXT": ""
    }
```

<h3>Events</h3>

I decided to start with 5 main event triggers:

- ON_USER_INPUT
- ON_ENTER_ROOM
- ON_LEAVE_ROOM
- ON_GAME_START

When something happens that means one of these trigger types should be triggered, all events of that type will be checked to see if they can be executed based on an event condition such as: IN_ROOM(3).

<h4>Parseable Language</h4>

To be able to add commands and conditions into the JSON files I needed to create a parsable language that my code could decipher. This is done through identifying key words and characters and arranging said characters as tokens in reverse polish notation.

The key words and characters understood by the code are as follows:
>
    X -> Used to signify an item name that should be taken from the player input.
    NOT
    AND
    OR
    IN_ROOM(int room_id)
    HAS_ITEM(int item_id)
    GET_ITEM_DATA(int item_id)
    RAND(int lower, int upper)
    SAY(std::string text)
    MOVE(int room_id)
    GIVE_ITEM(int item_id)
    SET_ROOM_EXIT(int room_id, int exit_id, TRUE or FALSE)
    PICKUP_ITEM(int item_id)
    SPAWN_ITEM_INTO_ROOM(int room_id, int item_id)
    SET_FREEZE(TRUE or FALSE)
    SET_ITEM_DATA(int item_id, int metadata)
    IS_ITEM_IN_ROOM(int item_id)
    REMOVE_ITEM(int item_id)
    INCREASE_SCORE(int score)
    DECREASE_SCORE(int score)
    SET_META_VISIBLE(int item_id, TRUE or FALSE)
    END_GAME
    +
    -
    *
    /
    >
    <
    =
    ;
    (
    )

Different combinations of the above keywords can create the conditions and commands needed for an event, such as:

```json
{
    "ID": 0,
    "NAME": "PICKUP_ITEM",
    "TRIGGER_TYPE": "ON_USER_INPUT",
    "IS_ONE_USE": false,
    "TEXT_PROMPT": "PICKUP ",
    "CONDITION": "IS_ITEM_IN_ROOM(X)",
    "COMMAND": "PICKUP_ITEM(X);",
    "FAILED_DESCRIPTION": "There is no such item in the room."
}
```

With the framework multiple games can be played, new JSON files just need to be added into the GameData directory. Starting a game just requires typing in the identifier of the game, e.g. HHA for the Haunted House Adventure.

<img src="{{ site.baseurl }}/assets/BasicReb0rn/framework-main-menu.png" alt="framework main menu"/>

<img src="{{ site.baseurl }}/assets/BasicReb0rn/framework-gameplay.png" alt="framework gameplay"/>