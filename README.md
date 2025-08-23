# blockland-dump
A dump of all my most significant blockland mods.\
Some of these have already been released in the past, but were either left outdated (blg releases) or never had easy download links (aebase)
Some of these have went untested/unused for multiple years, but should all be fully functional. Hopefully.

I am not planning on returning to Blockland, so please don't ask for me to update any of these.\
Feel free to use any code or assets from any of these for your own mods.

Add-on categories:
- [Clients](#clients)
- [Events](#events)
- [Gamemodes](#gamemodes)
- [Items](#items)
- [Players](#players)
- [Scripts](#scripts)
- [Servers](#servers)
- [Sounds](#sounds)
- [Supports](#supports)
- [Vehicles](#vehicles)
- [Weapons](#weapons)

<sub>*Click on an add-on's name to download it*</sub>

## Clients
### [Client_BetterMissionEdit](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Client_BetterMissionEdit.zip)
<sup>*Originally made for V20. Useless on V21, likely does not work on Rebuilt due to editor differences.*</sup>\
Adds various useful tools to the Mission Editor, and replaces file select dialogs with nicer ones that feature image previews.

### [Client_ReadFile](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Client_ReadFile.zip)
Adds two console commands to read out the clipboard's contents or an entire file to the server's chat eval.\
Originally made to work with Anthonyrules144's eval mod, but supports Port's<sup>(?)</sup> eval by passing 1 as the last argument to the commands.\

### [Client_SlayerSaveList](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Client_SlayerSaveList.zip)
Adds a new 'favorites' system to Slayer, allowing you to save more than 10 minigame presets with names.

## Events
### [Event_AESpawnAmmo](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Event_AESpawnAmmo.zip)
<sup>*Requires [Weapon_AEBase](#Weapon_AEBase).*</sup>\
Adds an `AESpawnAmmo` event to bricks, which spawns a single ammo drop for the brick's attached item.\
For example, triggering this on a brick that has an AK-47 attached will cause it to spawn a 7.62 ammo drop.

### [Event_FireRelayPlus](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Event_FireRelayPlus.zip)
Adds various different variations of the fireRelay event.\
Allows you to trigger relays in a radius and/or on one of 8 specific channels.\
For example, `fireRelayChannel [Self] [1]` will only trigger `onRelayChannel1` events.

### [Event_KillZone](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Event_KillZone.zip)
<sup>*Originally made for AlexK's battle royale.*</sup>\
Adds multiple battle royale shrinking killzone events, as well as a static rectangle killzone for delimiting non-battle royale maps.

Brick events:
> `KZSpawnBounds [end brick name] [damage]` - Spawns a static, rectangular killzone spanning from this brick to the end brick, and deals [damage] every second

> `KZSpawn [size] <delay> <time> <damage>` - Spawns a circular, shrinking killzone.\
> `size`: Initial size of the killzone, in torque units<sup>(?)</sup>.\
> `delay`: Delay until the killzone starts shrinking, in seconds. *Ignored if using phases*\
> `time`: Time until the killzone finishes shrinking, in seconds. *Ignored if using phases*\
> `damage`: Initial killzone damage per second. *Ignored if using phases<sup>(?)</sup>*

> `KZAddPhase [brick name | size] [delay] [time] [damage]` - Adds a new phase to the killzone.\
> `brick name | size`: Brick name to center the killzone on, followed by the size to shrink (or grow!) to during this phase.\
> `delay`: Delay until this phase starts. *If this is the first phase, it overrides the killzone's own `delay`*\
> `time`: Phase length, in seconds. Moves to the target brick and shrinks to the target size in `time` seconds. *If this is the first phase, it overrides the killzone's own `time`*\
> `damage`: Killzone damage during this phase. *If this is the first phase, it overrides the killzone's own `damage`<sup>(?)</sup>*\
> (1) Brick name and size are put into the same input due to events' 4 parameter limit.\
> (2) Phase delay and time are *not* absolute; if your phase has a length of 20 seconds, it will *always* take 20 seconds to complete, even if it begins more than 20 seconds after the killzone spawns.

> `KZDespawn` - Despawns the killzone.

> `KZColorHex [hex]` - Changes the killzone's color to a specific hex code.\
> *Unsure if this actually works*

> `onKZSpawn` - Triggered when a killzone is spawned on this brick.\
> `onKZPhaseStart` - Triggered when this brick's killzone starts a new phase.\
> `onKZPhaseEnd` - Triggered when this brick's killzone completes its current phase.\
> `onKZPhasesComplete` - Triggered when this brick's killzone has completed all of its phases.

Player events:
> `KZMakeImmune [immune]` - Makes this player immune to all killzones.

Minigame events:
> `KZLinkLast` - Links the last spawned killzone to this minigame, making it ignore other minigames.\
> This is not necessary if you only have one default minigame, as killzones affect *all* minigames by default.

### [Event_Loadouts](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Event_Loadouts.zip)
<sup>*Uses events exclusively. If you want a complete, customizable loadout/class system, see [Server_Loadouts](#Server_Loadouts) instead.*</sup>\
Adds a couple events to create player loadouts for modular spawn rooms.

Player events:
> `setLoadoutItem [slot] [item]` - Adds an item to the player's current loadout.\
> *This will not give the player the item right away, see `applyLoadout`*

> `setLoadoutGrenade [slot] [grenade/trap] [count]` - Adds a grenade or trap item to the player's current loadout.\
> `count`: Reserve ammo to give for the grenade.\
> *Requires [Weapon_Grenades](#Weapon_Grenades) to appear*

> `applyLoadout [clear]` - Applies the player's loadout, giving them all their items.
> `clear`: Clears the player's inventory prior to applying the loadout. If unchecked, empty slots are left untouched.

> `clearLoadout` - Resets the player's loadout.

> `saveLoadout [name]` - Saves the player's current loadout to a file with a specific `name`.
> `loadLoadout [name]` - Loads an existing loadout for this player with this `name`.
> Saves are separated per BLID.

Brick events:
> `loadoutCheck [slot]` - Checks if the triggering player has an item in their loadout at `slot`.
> Triggers `onLoadoutCheckFail` if the `slot` is empty. Otherwise, triggers `onLoadoutCheckSuccess`.

### [Event_MinigameAll](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Event_MinigameAll.zip)
Adds a (badly named...) `doPlayerLoop [name]` minigame event that triggers the `onMinigamePlayerLoop` input event for every player in a minigame.\
Allows you to run player/client events on everyone inside a minigame.\
If `name` is omitted, the input event is triggered on all bricks.\
Otherwise, it is only triggered on bricks with a matching name.

### [Event_PrintNear](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Event_PrintNear.zip)
Adds a `printNearby [message] [range] [action] <time>` event to players, bots and bricks, allowing you to display a bottomprint, centerprint or chat message to all players within `range`.\
`action` indicates which type of message to display, and `time` is ignored if using chat messages.

### [Event_ResAll](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Event_ResAll.zip)
<sup>*Requires Slayer.*</sup>\
Adds a `resurrectAll [lives]` minigame event that revives all dead players in the minigame and gives them back `lives`.\
*Already living players do not get granted any more lives.*

### [Event_ScoreAll](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Event_ScoreAll.zip)
Adds a `scoreAll [points]` minigame event that grants `points` to all players inside the minigame.

## Gamemodes
### [Gamemode_OxMining](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Gamemode_OxMining.zip)
<sup>*Requires various, mostly common brick packs.
Inside gamemode.txt, all addons under the 'Extras' category can be removed and are not necessary (except for Event_onBrickLoadedCarbon?). <sup>(Why can't you just pick modlists in addition to required addons!!!)</sup>\
If you can't find the addons to run this, contact me.*</sup>\
The millionth mining gamemode to have graced Blockland. Was originally going to be completely reworked to have more depth than just dirt go boom, but that never came.\
Features multiple layers, pickaxes, drills, bombs and other utilities.\
Some ore types can and will kill you.

This was never rehosted mainly because the save system really needed to be rewritten, as it had already gotten corrupted and reset once.\
I wanted to at least add backups and per-player saves before rehosting, but never got around to doing that...

## Items
### [Item_BrickBuilder](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Item_BrickBuilder.zip)
<sup>*Requires [Server_Resources](#Server_Resources).*</sup>\
Adds a 'Brick Builder' item that allows players to build destructible defenses.\
Uses Plastic as a resource to build. Bricks built with this can be destroyed by guns and explosives.\
Players can undo bricks built with this tool, and bricks drop plastic upon being destroyed.\
Was originally made for use in a Trench esque gamemode, but never went anywhere.

### [Item_KevlarPlus](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Item_KevlarPlus.zip)
<sup>*An edit of the old Kevlar Vest item.*</sup>\
Features three tiers of armor: Light, Medium and Heavy.\
Adds a `setArmor [type]` player event which automatically mounts a specific `type` of armor to a player, and item versions of each armor type.\
Each tier has different damage resistance stats, with high damage weapons being able to pierce through Light armor easily, but not Heavy armor.\
Upon taking too much damage, the armor breaks.

Can easily be extended by copy-pasting an existing armor item's code and editing its values.\
All custom armor types are automatically added to the `setArmor` list.

### [Item_Medical](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Item_Medical.zip)
<a name="Item_Medical"></a>
<sup>*An edit of the old Tier+Tactical<sup>(?)</sup> medical items.*</sup>\
Features two limited use healing items: the Pills and Medkit, as well as three infinite healing items: the Syringe, Gauze Gun and Stim Gun.\
The pills can only heal the user, while the medkit and syringe can be used to heal other players with the right click.\
Gauze/Stim gun can only be used to heal other players.

The Gauze Gun and Stim Gun are functionally identical, except the Stim Gun was meant to be used to revive downed players from a distance when using Swollow's Downed mod.\
I don't think I ever made use of either variant for very long...\
The syringe and medkit can both also revive players<sup>(?)</sup>.

## Players
### [Player_Dasher](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Player_Dasher.zip)
<sup>*Tumble on hit code by Carbon Zypher/Darksaber, released with permission.*</sup>\
Adds a 'Dasher' playertype that can right click to perform a short dash in their current movement direction.\
Crouching before dashing causes them to always dash straight forwards, but costs more energy when dashing away from their movement direction.\
Hitting a player or vehicle while dashing causes it to tumble and get knocked back.

### [Player_Hidden](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Player_Hidden.zip)
<sup>*Originally made for my The Hidden server.\
Requires Selective Ghosting for night vision.*</sup>\
Adds a 'The Hidden' playertype that is entirely invisible, jumps higher and silently, moves faster and has a night vision light.\
The Hidden can leap with right click, and regains health and energy by damaging enemies.\
Its light is much bigger and brighter, and can not be seen by other players.

### [Player_Tribal](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Player_Tribal.zip)
<sup>*Originally made for my Tribal Warfare server.*</sup>\
Features three 'Tribal' playertypes: Light (100 HP), Medium (150 HP) and Heavy (200 HP).\
Each playertype has fuel jets, different movement speeds and a rudimentary "skiing" feature. *Requires [Script_CustomBinds](#Script_CustomBinds) to ski*\
<sub>*Also features a commented out, bad attempt at making the skiing more useful by boosting players upon landing...*</sub>

## Scripts
### [Script_AutoEnvSave](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_AutoEnvSave.zip)
<sup>*Requires Support_AutoSaver.*</sup>\
A simple extension for Support_AutoSaver that saves the current environment settings alongside each autosave.

### [Script_CusHealthBar](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_CusHealthBar.zip)
A customizable health/energy bar mod. The code for this is *atrocious*, and none of the customization options are exposed to commands or BLG prefs...\
See `prefs.cs` for health bar setting descriptions.\
Use `/nohealthmod` to disable the health bar entirely for yourself.

Features a `setGlobalTarget [bool]` player event that displays that player's health bar to everyone else at all times. Useful for boss battles.\
If `bool` is unchecked, the player will be unmarked. Only one player can be marked at a time.

### [Script_CustomBinds](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_CustomBinds.zip)
<a name="Script_CustomBinds"></a>
<sup>*Originally made for my Tribal Warfare server.*</sup>\
Allows servers to register custom client keybinds. Required on both the server and client to work.\
See the bottom of `server.cs` for example usage.

### [Script_DevUtilities](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_DevUtilities.zip)
A collection of random functions I use for developing mods.\
All functions below `locateDuplicates` were meant for porting Tribes 2 maps to V20/Rebuilt.\
This is really just a mess of many completely unrelated functions I didn't feel like making separate mods for. It's just here for posterity.

### [Script_EventDescriptions](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_EventDescriptions.zip)
Adds description tooltips to the event menu. Mods can define custom descriptions on the server side, and any clients with the mod will see them.\
Features built-in descriptions for most default events as well as some common ones that will display even if the server doesn't have the mod installed.

### [Script_EventFix](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_EventFix.zip)
Adds an SA-only `/eventFix` command that will re-apply every single brick's events. Useful when duplicating large amounts of bricks around causes some events to not be registered properly.\
Some input events like the `onMinigame...` events sometimes don't register properly when duplicating bricks around, and this command allows you to reapply all of them without having to manually go and wrench every evented brick.

Also features a `/eventCopy [from] [to]` command that allows you to mass copy events from one `from` brick to all `to` bricks.\
<sub>*`/claimBricks` will not work on any named or evented bricks as it doesn't carry ntobject data over. It was meant to be moved to a different add-on.*</sub>\
<sub>*`/clearNamedBricks [name]` is self explanatory. It was meant to be moved to a different add-on.*</sub>

### [Script_GhostAll](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_GhostAll.zip)
Adds a `/ghost` command that forces all objects to be ghosted to you, on a 30 second cooldown.\
`/ghostAll` is admin only and does the same thing as `/ghost`, but for all connected players.\
<sub>*`/locateFar [distance]` dumps a list of bricks more than `distance` units away. It was meant to be moved to a different add-on.*</sub>\
<sub>*`/gotoBrick [id]` teleports you to a specific brick. It was meant to be moved to a different add-on.*</sub>\
<sub>*`/eventWatch` displays a log of all brick events as they happen, to catch spammers. It was meant to be moved to a different add-on.*</sub>

### [Script_HighVehicleLimit](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_HighVehicleLimit.zip)
A small script that increases the vehicle limit to 2000. Made because the limit I set in the server settings would never save and it pissed me off...

### [Script_InventorySort](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_InventorySort.zip)
<a name="Script_InventorySort"></a>
Adds a `/invsort` command that pulls up a centerprint menu to reorder your inventory.\
Useful on battle royales and similar gamemode to reorder weapons without having to drop them.\
Features a function to package to handle (or prevent) reordering weapons.\
Transfers over ammo values for Tier Tactical (untested), the [Item_Medical](#Item_Medical) edit, as well as [Weapon_Grenades](#Weapon_Grenades) to avoid ammo duplication tricks.

### [Script_ItemDrops](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_ItemDrops.zip)
<sup>*Requires Slayer.*</sup>\
Adds various Slayer minigame settings to control item dropping.

> `Drop items on death` - Causes players to drop all their items on death. Unlike other such mods, this one will not reset weapon ammo.\
> `Keep items until reset` - Causes all dropped items to remain until the minigame resets.\
> `Despawn Time` - How long until dropped items despawn. Default is 10 seconds.\
> `Allow dropping items` - Prevents players from manually dropping items.

Adds an admin only `/clearItems` command that deletes all dropped items belonging to the minigame you are in.\
Also adds a (confusingly named) `/clearAllItems` command that deletes all dropped items.

### [Script_KeepVehicles](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_KeepVehicles.zip)
<sup>*Originally made for my Tribal Warfare server.*</sup>\
A small script that makes all vehicles stay when their owner leaves the server.\
Avoids vehicles respawning (or even breaking entirely) in gamemodes when the host leaves.

### [Script_LocalChat](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_LocalChat.zip)
A small script that adds proximity text chat. Essentially a watered down roleplay mod, but does not feature RP names.\
Start your message with ! to yell and @ to whisper.\
Disabled by default, check preferences to enable and tweak settings.

### [Script_MapReload](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_MapReload.zip)
<sup>*Brick save to file code taken from Support_AutoSaver.*</sup>\
A custom made autosaver & map rotation system. Originally made for V20 to automatically reload the last played map when starting up a dedicated server (hence the name MapReload), but later revamped to support Rebuilt & V21.\
Saves the current environment setup alongside your build, and automatically reloads the last save when starting up the server.\
Features multiple preferences.\
Use `/savebricks <name>` or `/sb <name>` to save your build, and `/loadbricks <name>` or `/lb <name>` to load a save.\
Saving with no name timestamps your save like an autosave, and loading with no name reloads the last save.\

Map rotation system is made for Slayer (but may work with non slayer default minigames), and supports /rtv and map voting.\
To set up map rotation:
1. Enable map rotation through preferences.
2. Set a map playlist using `/setMapPlaylist [name]`. If no playlist is set, map rotation will be disabled.
3. Go through each map save and add them to the playlist with `/savePlaylistMap [name]`.
	- Check the existing list of maps with `/maplist`.
	- Remove unwanted maps with `/removePlaylistMap [name]`.
	- Saving the same map twice will overwrite the existing save.
4. Start up a default minigame.
	- Map rotation will now automatically kick in after a set number of rounds.
	- Check the preferences to adjust the number of rounds per map, disable map voting or RTV voting, or tweak other settings.

*Some people have had issues with brick prints being broken when loading a save with this mod, though I have not myself...*

### [Script_Minimap](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_Minimap.zip) <sup>[(repo)](https://github.com/Zinlock/Script_Minimap)</sup>
<a name="Script_Minimap"></a>
<sup>*Originally made for my Tribal Warfare server.*</sup>\
Adds a minimap to the top right of the screen. Required on both the server and client to work.\
Can be opened up in a full-screen view where you can click on the minimap to ping areas or trigger events on waypoints by clicking them.\
Features a couple preferences to change the minimap's view scale and hide enemy players in minigames.\
Also includes a few events to display text under the minimap and change the minimap icon of players or display waypoints on bricks and vehicles.

### [Script_NoLightFix](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_NoLightFix.zip)
A small script that adds a better 'Disable lights' Slayer preference.\
The default one causes issues with many add-ons that rely on the light key. This one is less intrusive and will not interfere.

### [Script_NoSit](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_NoSit.zip)
A small script that adds 'Disable /sit' and 'Disable crouch sitting' Slayer preferences.\
The first simply disables sitting entirely, while the latter only prevents sitting while crouching to avoid the 'dry hump' bug.

### [Script_VehicleMinigameFix](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Script_VehicleMinigameFix.zip)
<sup>*Originally made for my Tribal Warfare server.*</sup>\
A small script that gives the currently running default minigame ownership of all vehicles.\
Avoids vehicles becoming unusable when the host leaves.

## Servers
### [Server_AdminUtilities](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Server_AdminUtilities.zip)
A collection of various admin tools to moderate servers (or troll people :D)\
Features force killing, reviving, admin chat, giving items, build banning, event banning and more.\
Use `/auhelp` for a list of all available commands.

### [Server_AkimboAnything](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Server_AkimboAnything.zip)
An old, *extremely* jank mod that allows players to pick up any weapon in their left hand.\
When enabled, trying to pick up any item with your inventory open will mount it to your left hand, and right clicking will fire it.\
Unsurprisingly, this tends to look bad and can cause issues especially with ammo-based guns, normal akimbo weapons and two-handed weapons.

### [Server_HatMod](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Server_HatMod.zip)
<sup>*An edit of the old Hat Mod.\
Requires Selective Ghosting.*</sup>\
An edit of Hat Mod that uses bots instead of images to mount hats, allows players to use up to 4 hats at a time, and includes the node hiding system built in.\
Also supports recoloring hats, but since they were all made out of images, no existing hats support this lol

### [Server_Loadouts](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Server_Loadouts.zip) <sup>[(repo)](https://github.com/Zinlock/Server_Loadouts)</sup>
<a name="Server_Loadouts"></a>
<sup>*Originally made for Pacer's Randomizer DM server, then expanded for Tribal Warfare and Trench CTF.*</sup>\
A customizable loadout system. Supports preset classes as well as customizable loadouts with class-locked weapons, and a randomizer mode to make players spawn with random loadouts or classes.\
Allows you to create gamemodes with multiple classes or customizable loadouts without having to rely on specific events or tie your loadouts to specific maps. Makes it easy to modify loadout sets without having to go through all of your maps to update spawn rooms.\
Use `/lohelp` for help setting up loadouts. Only the server host can set them up by creating config files for each loadout set. If you use vscode, use .ini highlighting for the set files to separate comments clearly.

Slayer preferences and events can be used to control which loadout sets are in use for a minigame, team or even individual players.\
A loadout set controls which classes players can use, and even allow players to customize their loadout and pick their own weapons.\
Sets can trigger various events when applying loadouts or when dying with a specific loadout.\
By default, class-locked weapons can only be picked up by players with the same class, and item order is enforced. (e.g rifles can only be put in slot 1)

Use `/loadout` or `/class` to edit your loadout or pick a class.

Client events:
> `LOOverrideSet [name]` - Changes this client's current loadout set to `name` until the minigame resets or the client leaves the minigame.\
> `LORandomizeLoadout <seed>` - Randomizes this client's loadout.

Player events:
> `LOApplyLoadout [force] [silent]` - Applies this player's current loadout, giving them their weapons and playertype.\
> `force`: Applies their loadout even if it was already equipped before.\
> `silent`: Hides the centerprint message.

> `LOResupplyLoadout [force] [silent]` - Reapplies this player's last used loadout.\
> `force`: Applies their new loadout if it changed since they last had it applied.
> `silent`: Hides the centerprint message.

### [Server_Resources](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Server_Resources.zip) <sup>[(repo)](https://github.com/Zinlock/Server_Resources)</sup>
<a name="Server_Resources"></a>
<sup>*Originally made for aebaadcode's Prison Breakout server.*</sup>\
A resource system that allows players to pick up various scrap items, and adds events to allow crafting with those resources.\
Adds wood, plastic, metal scrap, ropes, tape, diamonds, glue and more.\
Resources do not go into the inventory when picked up, and are all dropped on death.\
Also features resource storage which allows players to stash resources in bricks, and save/load storage contents to a file.

### [Server_SlayerTeamBeacons](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Server_SlayerTeamBeacons.zip)
<a name="Server_SlayerTeamBeacons"></a>
<sup>*Requires Slayer and Selective Ghosting.*</sup>\
Adds beacons over players' heads in Slayer minigames to make locating teammates easier in large maps.\
Includes Slayer team preferences to control beacon visibility.\
This version *should* work, but I noticed issues with it sometimes showing enemy positions too last time I hosted...

### [Server_Trench](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Server_Trench.zip) <sup>[(repo)](https://github.com/Zinlock/Server_Trench)</sup>
<sup>*An edit of the old Trench mod.*</sup>\
This version of the Trench mod features explosive damage, saving & reloading Trench maps (supported by [Script_MapReload](#Script_MapReload)), picking block colors before building and new models for the tool.\
I believe the shovel model was made by Radio Star/Nikod?

Disable trench building and destruction while working on your map with `/xtToggle`.\
Once your map is complete, make sure to run `/xtRebuildFullSource`. Otherwise, trying to reload the map will cause deleted bricks to reappear.\
After clearing your map, run `/xtClearSource` so you can't accidentally respawn it.\
To undo all damage done to your map, run `/xtRebuildDirt`.\
The saving and loading commands only save trench bricks and went largely unused. *If you want to have map rotation with Trench, see [Script_MapReload](#Script_MapReload)*\
Avoid saving the map after or during a match. The loading logic is broken and will put player built bricks into the source even though it isn't supposed to.\
Use `/xthelp` for a list of all commands.

The 'Disable Floating Bricks' preference does not work. Float checks were never implemented.\
The 'Explosive Radius Multiplier' preference defaults to `1`, which causes massive holes when blowing up terrain. I recommend running with `0.25`.

## Sounds
### [Sound_Tribes2Flags](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Sound_Tribes2Flags.zip)
<sup>*Originally made for my Tribal Warfare server.*</sup>\
Adds the flag pickup, drop, capture and respawn sounds from Tribes 2, alongside a Slayer preference to play them in CTF minigames.

## Supports
### [Support_BulletHoles](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Support_BulletHoles.zip)
Makes projectile impacts spawn bullet hole decals.\
I don't know why this is a "support" mod.

### [Support_XStateSys](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Support_XStateSys.zip)
<a name="Support_XStateSys"></a>
An entirely custom bot weapon state system made for [Weapon_XArena](#Weapon_XArena).\
States work similarly to the normal image state system, but with a bunch of extra utilities.\
Does not add any content on its own.

## Vehicles
### [Vehicle_AbramsTank](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Vehicle_AbramsTank.zip)
<sup>*Originally made for Cordax's Hartham server.\
Requires [Weapon_AEBase](#Weapon_AEBase).*</sup>\
The M1 Abrams with a cannon and machine gun, as well as an external M2 Browning gunner seat.\
Was originally planned to have more than just the Abrams...

### [Vehicle_Tribal](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Vehicle_Tribal.zip) <sup>[(repo)](https://github.com/Zinlock/Vehicle_Tribal)</sup>
<sup>*Originally made for my Tribal Warfare server.*</sup>\
A mostly faithful recreation of every Tribes 2 vehicle.\
Features a hoverbike, a scout plane with mounted guns, a hover tank with a cannon and machine gun, a bomber plane and a transport plane.

If [Weapon_Turrets](#Weapon_Turrets) is also enabled, it will include a Vehicle Pad to spawn vehicles with as well as the Jericho MPB truck with a mounted inventory station and sentry turret.\
To set up a vehicle pad:
1. Place a Base Vehicle Spawner where you want to spawn vehicles
	- It will place a static shape that may block the wrench, but the New Duplicator should be able to click through and reach the vehicle spawn. I know, this is dumb.
2. Place a Base Vehicle Station where you want players to spawn vehicles from
3. Wrench the Station's vehicle spawn and add the following events, in order:
	- onStationSpawn > Station > vpadLinkSpawner \[nearest] \[]
	- onStationSpawn > Station > vpadClearVehicleList *(yes this is necessary) (i know, this is dumb)*
4. Add any number of vehicles to the list:
	- onStationSpawn > Station > vpadAddVehicleList \[vehicle] \[limit]
		- If the limit is 0, then this vehicle can be spawned infinitely.
		- Unoccupied vehicles will always be destroyed after being left empty for over a minute, except for the Jericho MPB. You can allow other vehicles to remain indefinitely by setting the `vpadNeverTimeOut` datablock field to `true`.

## Weapons
### [Weapon_AEBase](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Weapon_AEBase.zip) <sup>[(repo)](https://github.com/Zinlock/Weapon_AEBase)</sup>
<a name="Weapon_AEBase"></a>
A weapon base with a million billion features, made by me and aebaadcode. Does not add any content on its own besides ammo items.\
Has support for [Script_InventorySort](#Script_InventorySort), ammo is transfered when sorting inventory to avoid ammo duplication tricks.

### [Weapon_AEBase_BreachEnter](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Weapon_AEBase_BreachEnter.zip) <sup>[(repo)](https://github.com/Zinlock/Weapon_AEBase_BreachEnter)</sup>
<sup>*Requires [Weapon_AEBase](#Weapon_AEBase).*</sup>\
A 'remaster' of the old H&K pack, put on AEBase. Features various edits of H&K guns with some entirely new models by ZeUberMedic, all reanimated by me and aebaadcode, with some sounds by Cowtastic.\
This pack contains around *80 guns.*

### [Weapon_AEBase_Rallypack](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Weapon_AEBase_Rallypack.zip) <sup>[(repo)](https://github.com/Zinlock/Weapon_AEBase_Rallypack)</sup>
<sup>*Requires [Weapon_AEBase](#Weapon_AEBase).*</sup>\
A 'remaster' of Rallypack, put on AEBase. Features various edits of rallypack guns, all reanimated by me, with some sounds by Cowtastic.\
Was originally planned to be bigger... Most weapons lack ADS.

### [Weapon_AEBase_TranqGun](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Weapon_AEBase_TranqGun.zip)
<sup>*Requires [Weapon_AEBase](#Weapon_AEBase) and [Emote_Snore](https://blockland.online/rtb/addons/1135/snore-emote).*</sup>\
A tranquilizer gun. Puts players to sleep, preventing them from moving, shooting or talking. Spam clicking them, shoving them or damaging them will wake them up.\
Headshots instantly put them to sleep while body shots have a delayed effect, slowing them before putting them to sleep a couple seconds later.

### [Weapon_AirSupport](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Weapon_AirSupport.zip)
<sup>*Requires [Vehicle_A10](https://blockland.online/rtb/addons/4107/a-10-thunderbolt-ii).*</sup>\
Adds an Air Strike Radio item that calls in an A-10 strafing run.
Was originally planned to have more call-ins...

### [Weapon_Grenades](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Weapon_Grenades.zip) <sup>[(repo)](https://github.com/Zinlock/Weapon_Grenades)</sup>
<a name="Weapon_Grenades"></a>
A pack of 16 different grenades. Adds frag grenades, clusters, molotovs, thermite, flashbangs, smokes, electric grenades, C4 and more.

### [Weapon_Traps](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Weapon_Traps.zip) <sup>[(repo)](https://github.com/Zinlock/Weapon_Traps)</sup>
<sup>*Requires [Weapon_Grenades](#Weapon_Grenades).*</sup>\
A pack of 12 placeable traps as well as a health station and an energy station. Adds anti-personnel and anti-tank mines, proximity mines, bear traps and more.

### [Weapon_TribalWar](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Weapon_TribalWar.zip) <sup>[(repo)](https://github.com/Zinlock/Weapon_TribalWar)</sup>
<a name="Weapon_TribalWar"></a>
<sup>*Originally made for my Tribal Warfare server.
Requires [Weapon_AEBase](#Weapon_AEBase) and [Weapon_Grenades](#Weapon_Grenades)*</sup>\
A pack of 23 Tribes 2 esque weapons. Adds lock-on launchers, grenade launchers, snipers, machine guns and more.\
Includes a Repair Gun, mainly for use with turrets and vehicles (though it works on players too.)\
Also includes an Energy Pack, which makes jet fuel recharge faster. Some items are meant to be used with fuel jet playertypes, and are energy-fed rather than using ammo.\
The shocklance and charge cannon require a minigame and a valid target to work.

### [Weapon_Turrets](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Weapon_Turrets.zip) <sup>[(repo)](https://github.com/Zinlock/Weapon_Turrets)</sup>
<a name="Weapon_Turrets"></a>
<sup>*Originally made for my Tribal Warfare server.*</sup>\
A mostly faithful recreation of the Tribes 2 base turrets and assets.\
Features multiple turret types, events for turrets and deployable versions of each turret. Barrels allow switching turret types on the fly by players.\
Turrets and base assets will not respawn once destroyed. Instead, they must be repaired manually.\
Turrets spawned on Slayer vehicle spawns will be friendly to whichever team the spawn belongs to. Turrets will target enemies, and inventory stations will refuse to heal or resupply enemies.\
*For some reason, it tries to execute the ShapeLinesV2 script from the add-ons folder without checking if it exists. If this causes any errors, remove line 15 from `server.cs`.*

The Inventory Station heals players and recharges energy while using it.\
Sensors will spot players and makes their beacons & minimap icons visible to all. *Requires [Script_Minimap](#Script_Minimap) or [Server_SlayerTeamBeacons](#Server_SlayerTeamBeacons) to work*\
Generators can be used to power base assets. When set up, once all generators are destroyed, all linked assets (stations and turrets) are disabled until they are repaired.

To set up generator power:
1. Place any number of Turrets, Stations and Generators or Solar Panels.
2. Wrench the vehicle spawn for each of them, and add the following event to them:
	- onStationSpawn > Station > turretPowerLink \[group]
		- The group that you link to is used to determine which stations share power. If all generators within a group go down, all stations within are also disabled.
		- If an asset has no group, it will always be powered.

Other turret events:
> `turretMountImage [name] [force]` - Changes this turret's type. Useful for setting default turret types on maps.\
> `name`: The name of the turret type. This can be either the item name, or the name displayed in the centerprint description.\
> `force`: Mounts the turret barrel even if this turret can't normally change types.

> `turretWallMount [ground/wall/ceiling]` - Attaches this turret to a nearby surface. This allows you to mount it to walls and ceilings to put it sideways or upside down.\
> (1) The maximum distance for the mount ray is fairly short, so make sure the vehicle spawn is close enough to it.\
> (2) This may completely break non-turret assets.\
> (3) The `wall` option only checks forwards, so make sure your spawn faces the wall you want to mount to when using it.

> `turretTurn [angle]` - Rotates the turret by a specific angle in degrees, from -180 to 180. Useful to make stations in corner face directly away from the corner, or to adjust a turret's rotation after mounting it to a wall.\
> This event is a little jank and can sometimes refuse to turn turrets to specific angles.

If [Weapon_TribalWar](#Weapon_TribalWar) is also enabled, it will include 4 more turret types (Mortar, Repair, ELF, Heat Seeker).
If [Server_Loadouts](#Server_Loadouts) is also enabled, inventory stations will automatically apply player loadouts when used.

### [Weapon_XArena](https://github.com/Zinlock/blockland-dump/raw/refs/heads/main/Weapon_XArena.zip)
<a name="Weapon_XArena"></a>
<sup>*Requires [Support_XStateSys](#Support_XStateSys).*</sup>\
A very incomplete "pack" of fantasy melee weapons that never went anywhere.\
Includes two weapons, the Scythe and Crystal Sword.

Each weapon has 4 attacks (LMB tap, LMB hold, E, R) and can block (hold RMB)\
A well timed block will parry incoming hits, staggering the target.\
Holding block reduces incoming damage, but doesn't block it entirely. Holding, being damaged while holding block or failing a parry will all cost stamina.\
If you run out of stamina, you can no longer block until it recharges.