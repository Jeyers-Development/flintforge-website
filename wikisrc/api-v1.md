
# Flintforge Modding API v1 Documentation

# Mod Creation Instructions

## Step 1: Workspace Setup

Replace your_mod_name with whatever you want to call your mod with no uppercase, and no spaces.

![MOD SETUP GIF FILE, LOADING...](https://github.com/Jeyers-Development/flintforge-website/blob/main/wikisrc/setup.gif?raw=true)

## Step 2: Mod Declaration Files

The mod declaration files are the _‘title’, ‘authors’, ‘permanent’, and ‘version’_ files. Without these, your mod will not import.

1. Edit the _‘permanent’_ file: this files contents will be along the lines of _‘example_mod’ or ‘jacobs_recipe_mod’ (just make it the same as the workspace dir name, that just makes things easier)_, NO SPACES, NO CAPITALS. DO NOT CHANGE THIS AFTER PUBLISHING. Saves may corrupt for players if you change _permanent_’s contents after they first install it and then update it. The file name implies that it is permanent.
2. Edit the _‘version’_ file: for this API version set the contents to exactly (don’t include the quotes) “InDevp_mod”
3. Edit the _‘title’_ file: set the contents to whatever you want the mod’s name to be when it says it is imported, (ex. _‘Example Mod’, ‘Jacobs Recipe Mod’_)
4. Edit the _‘authors’_ file: set this files contents to whoever needs credit to this project. If you set this to “John Doe, Jace Marie, and James Kanes” on import it will say “Mod Imported: Example Mod (example_mod) - By John Doe, Jace Marie, and James Kanes”

## Step 3: Add content

As of now you can add ***items*** and ***recipes***. The rest of this document will be dedicated to that.

### Adding Items

1. Under the ***‘data’*** directory from earlier create another folder called ***‘item’.***
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

### Adding Recipes

1. Under the ***‘data’*** directory from earlier create another folder called ***‘recipe’.***
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

## Step 4: Build Mod

### Python Build File (recommended)
Under the base workspace directory create a file with the name ***'build.py'*** .

Set the contents of this file to:
```python
import shutil
import os

source_dir = os.getcwd()

if os.path.exists(source_dir + ".zip"):
  os.remove(source_dir + ".zip")
shutil.make_archive(source_dir, 'zip', source_dir)
if os.path.exists(source_dir + ".jop"):
  os.remove(source_dir + ".jop")
os.rename(source_dir + ".zip", source_dir + ".jop")
```
Run the python build file to get the compressed .jop Flintforge mod!

### Manual Build (7zip)
Compress the contents of the folder to .zip and rename extension to .jop
![BUILD-WITH-7ZIP GIF FILE, LOADING...](https://github.com/Jeyers-Development/flintforge-website/blob/main/wikisrc/build.gif?raw=true)

# Mod Publishing

[Mod DB Uploading Tool](https://flintforge.pnc3.net/mod/uploader.html)

 Access the Mod DB Uploading Tool to make a Mod DB user. Enter your desired username, then click the ***"Register New User"*** button. This will generate a command for you to copy under ***"CMD curl to register (or copy):"*** . Copy the command, open command prompt and paste it in.  

   Should look something like this:
    
    PS C:\Users\admin> curl.exe -X POST "https://mod-uploader-worker.jakejem2010.workers.dev?action=register&username=TestingUser"
    {"success":true,"username":"TestingUser","userKey":"e8e3fad27f2c27ace299fafc01ea7fb3ffa7d1ad0eaaacb90bc6aabf6dcd2268"}
    PS C:\Users\admin>

Copy the ***"userKey"*** (dont include quotes, ex: e8e3fad27f2c27ace299fafc01ea7fb3ffa7d1ad0eaaacb90bc6aabf6dcd2268).

Go back to the Mod DB Uploading Tool and paste in the use key along with your username and click ***"Next"***

FILL IN ALL INFORMATION AND PASTE THE COMMAND INTO COMMAND PROMPT LIKE BEFORE!!!

Check if mod shows up, if it doesn't then make sure you've followed all the steps correctly. If you still have problems contact support at support@pnc3.net.

# Support Flintforge
[Buy the Flinforge Support Package on Itch.io](https://jeyers-development.itch.io/flintforge-support) ($2.00+)
[Download My Modrinth Minecraft Mods](https://modrinth.com/user/TeamJEM) (FREE)
Join the [Discord - This link gives you 'Modder Role'](https://discord.gg/zPEqgP9hgU) and tell your friends! (FREE)

# Help?
Contact support at support@pnc3.net.









