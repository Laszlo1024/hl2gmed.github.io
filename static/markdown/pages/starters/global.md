# Global Variables

<br/>

## Global Tables

There are various global tables containing the active game  
state some of which are only available in specific scopes.

| Variable | Value | Scope |
|:--------:|:------|:------|
| `GAMEMODE` | The active gamemode | Available anywhere <br/> Only available if the gamemode has been loaded 
| `GM` | The loading gamemode | Available inside the gamemode's files <br/> Only available while the gamemode is loading <br/><br/> `gamemodes/<Gamemode>/gamemode/*.lua`
| `ENT` | The current scripted entity | Available inside the entity's files <br/><br/> `lua/entities/*.lua`
| `NPC` | The current scripted npc | Available inside the entity's files <br/><br/> `lua/npcs/*.lua`
| `SWEP` | The current scripted weapon | Available inside the weapon's files <br/><br/> `lua/weapons/*.lua`
| `EFFECT` | The current scripted effect | Available inside the effect's files <br/><br/> `lua/effects/*.lua`
| `TOOL` | The current scripted tool | Available inside the tool's files <br/> Only exists in Sandbox derived gamemodes <br/><br/> `lua/weapons/gmod_tool/stools/*.lua`
| `_G` | All globals, including itself | Available anywhere
| `_MODULES` | List of all `/modules/` | Available anywhere 

<br/>


# NON CONSTANTS

## CLIENT
This is true whenever the current script is executed on the client. ( client and menu states ) See <page>States</page>. Always present.

## CLIENT_DLL
This is true whenever the current script is executed on the client state. See <page>States</page>.

## SERVER
This is true whenever the current script is executed on the server state. See <page>States</page>. Always present.

## GAME_DLL
This is true whenever the current script is executed on the server state.

## MENU_DLL
This is true when the script is being executed in the menu state. See <page>States</page>.

## GAMEMODE_NAME
Contains the name of the current active gamemode.

## NULL
Represents a non existent entity.

## VERSION
Contains the version number of GMod. Example: `201211`

## VERSIONSTR
Contains a nicely formatted version of GMod. Example: `"2020.12.11"`

## BRANCH
The branch the game is running on. This will be `"unknown"` on main branch. While this variable is always available in the <page text="Client">States#client</page> & <page text="Menu">States#menu</page> realms, it is only defined in the <page text="Server">States#server</page>  realm on local servers.

## _VERSION
Current Lua version. This contains `"Lua 5.1"` in GMod at the moment.

## NETVERSIONSTR
Contains the current networking version. Example: `"2023.06.28"`
<note>This only exists in the Menu state</note>

## MAX_EDICT_BITS
Contains the maximum number of bits needed to network any entity. Used for <page>net.WriteEntity</page>. <page>bit.lshift</page> can be used to turn this value into maximum number of networked entities `(1 << MAX_EDICT_BITS)`

## MAX_PLAYER_BITS
Contains the maximum number of bits needed to network player. Used for <page>net.WritePlayer</page>. Depends on the maximum slots count on the server

## g_ Shortcuts
```
Shortcut pointers to important clientside objects.
```

|   Variable   | Source | Description |
|:------------:|:------:|:------------|
| `g_SkyPaint` | [![GitHub]][g_SkyPaint] | The active *env_skypaint* entity.
| `g_ContextMenu` | [![GitHub]][g_ContextMenu] | Base panel used for context menus.
| `g_VoicePanelList` | [![GitHub]][g_VoicePanelList] | Base panel for displaying incoming/outgoing voice messages.
| `g_SpawnMenu` | [![GitHub]][g_SpawnMenu] | Base panel for the spawn menu.
| `pnlMainMenu` | [![GitHub]][pnlMainMenu] | Main menu of Gmod. (only available in the menu state) 


[GitHub]: https://files.facepunch.com/wiki/files/b5608/8dc55c44e553869.webp

[g_VoicePanelList]: https://github.com/Facepunch/garrysmod/blob/master/garrysmod/gamemodes/base/gamemode/cl_voice.lua#L133
[g_ContextMenu]: https://github.com/Facepunch/garrysmod/blob/master/garrysmod/gamemodes/sandbox/gamemode/spawnmenu/contextmenu.lua#L145
[g_SpawnMenu]: https://github.com/Facepunch/garrysmod/blob/master/garrysmod/gamemodes/sandbox/gamemode/spawnmenu/spawnmenu.lua#L243
[pnlMainMenu]: https://github.com/Facepunch/garrysmod/blob/master/garrysmod/lua/menu/mainmenu.lua#L481
[g_SkyPaint]: https://github.com/Facepunch/garrysmod/blob/master/garrysmod/gamemodes/base/entities/entities/env_skypaint.lua

# CONSTANTS

## MISC

```
vector_origin		= Vector( 0, 0, 0 )
vector_up	 		= Vector( 0, 0, 1 )
angle_zero			= Angle( 0, 0, 0 )

color_white 		= Color( 255, 255, 255, 255 )
color_black 		= Color( 0, 0, 0, 255 )
color_transparent 	= Color( 255, 255, 255, 0 )
```

## ENUMS
Almost all enumerations are globals.
