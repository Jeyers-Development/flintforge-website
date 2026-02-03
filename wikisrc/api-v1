# Flintforge Modding API v1 Documentation

## Step 1: Workspace Setup

Replace your_mod_name with whatever you want to call your mod with no uppercase, and no spaces.

![](https://github.com/Jeyers-Development/flintforge-website/blob/main/wikisrc/setup.gif?raw=true)

## Step 2: Mod Declaration Files

The mod declaration files are the _'title', 'authors', 'permanent', _and_ 'version'_ files. Without these, your mod will not import.

1. Edit the _'permanent'_ file: this files contents will be along the lines of _'example_mod' or 'jacobs_recipe_mod' (just make it the same as the workspace dir name, that just makes things easier)_, NO SPACES, NO CAPITALS. DO NOT CHANGE THIS AFTER PUBLISHING. Saves may corrupt for players if you change _permanent_'s contents after they first install it and then update it. The file name implies that it is permanent.
2. Edit the _'version'_ file: for this API version set the contents to exactly (don't include the quotes) "InDevp_mod"
3. Edit the _'title'_ file: set the contents to whatever you want the mod's name to be when it says it is imported, (ex. _'Example Mod', 'Jacobs Recipe Mod'_)
4. Edit the _'authors'_ file: set this files contents to whoever needs credit to this project. If you set this to "John Doe, Jace Marie, and James Kanes" on import it will say "Mod Imported: Example Mod (example_mod) - By John Doe, Jace Marie, and James Kanes"

## Step 3: Add content

As of now you can add ***items*** and ***recipes***. The rest of this document will be dedicated to that.

### Adding Items:

1. Under the ***'data'*** directory from earlier create another folder called ***'item'.***
2. For each item create a <item_name>.json file, replacing <item_name> with your items name with no uppercase, and no spaces.
3. Edit the item file. (heres an example from the Insane Multitool Mod) REMOVE ALL COMMENTS FROM THIS IF YOU COPY IT AND CHANGE NAMES!

```json
{
    "modItemId": 0, //MAKE EACH ITEM HAVE A UNIQUE modItemID, MAKE IT INCREMENTAL!!! (next item would be 1, after that 2, and so forth)

    "filename": "insane_multitool", //make this the same as the item json file without the .json file extension
    "name": "Insane Multitool", //change this to whatever you want the item to be named as in-game, spaces and capitals allowed
    "itemCanPlace": false,
    "itemSoundPlace": "null", //if the itemCanPlace value is true (if not leave as "null")set it to any of the built-in game sounds (custom audio coming soon)...
                              //available values:
                              // brick, crunch, fire_sound_1, generic_place (default), pop, shale-ish_break, stone_craft, wood_break
    "use": {
        "type": "tool_universal", //here is where you declare use
                                  // CRAFTING ONLY: "type": "other"
                                  // ALL TOOLS: tool_shovel, tool_hammer, tool_knife, tool_pickaxe, tool_axe, tool_sword (not implemented yet)
                                  // PLACE BLOCKS: "type": "block"
                                  // SPAWN ENTITY: "type": "entity"
        "value": "99:99" // here is where you declare the use value
                                  // CRAFTING ONLY: "value": "crafting"
                                  // ALL TOOLS: "value": "<tool tier>:<tool speed multiplier>"
                                  // PLACE BLOCKS: "value": "game:<block_you_want_to_place>"
                                  // SPAWN ENTITY: "value": "game:<entity_you_want_to_spawn>"
    },

    // NOW ONTO THE OPTIONAL VALUES
    "textureBaseFolder": "mods/insane_multitool_mod/texture/", //change this if you want textures in a different base folder (ex. "mods/insane_multitool_mod/images/")
    "textureExtensionFolder": "items" //change this if you want textures in a different folder extension than 'item' (ex. "cool_added_item")
}
```

### Adding Recipes:

1. Under the ***'data'*** directory from earlier create another folder called ***'recipe'.***
2. For each item create a <recipe_name>.json file, replacing <recipe_name> with your recipe name (can be anything) with no uppercase, and no spaces.
3. Edit the recipe file. (heres a **modified json** example from the base Flintforge Game) REMOVE ALL COMMENTS FROM THIS IF YOU COPY IT AND CHANGE NAMES!

```json
{
    "required": [ // EACH STRING IN THIS ARRAY WILL CORRESPOND TO AN ITEM
        "game:raw_mold-anvil", 
        "game:coal",
        "<your_cool_mod>:<required_item>" // replace <your_cool_mod> with your mod's 'permanent' id from earlier.
                                          // replace <required_item> with the "filename" of the item's json file from earlier
    ],
    "required_amount": [ // EACH INT IN THIS ARRAY WILL CORRESPOND THE AMOUNT YOU NEED OF THE ITEM, IN THE SAME ORDER AS THE "required" array
        1,
        4,
        -1  // negatives are equivalent to saying "at least" so you need at least one <required_item> but it will not take it away when crafted.
    ],
    "output": "game:fired_mold-anvil", // the output of the recipe when crafted... modded item would use the same format as <your_cool_mod>:<required_item>

    // NOW ONTO THE OPTIONAL VALUES
    "stations": [ // if the player is close enough to one of these BLOCKS in this array then it will let you craft it. if you aren't you cant. ex. game:dirt
        "game:brick_forge_basic",
    ],
    "required_event": "christmas"  // this is a required seasonal event that the player has to be in to craft. (only christmas is available right now [NOTE: INDEVP-9 DISABLES ALL SEASONAL EVENTS DUE TO TEXTURE CONFLICTS AND RETURNS IN LATER VERSIONS])
}
```
