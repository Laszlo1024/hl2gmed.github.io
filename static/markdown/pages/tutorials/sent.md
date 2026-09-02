# First Scripted Entity
<div class="note"><b>💡NOTE:</b><br><i>This tutorial doesn't seem to show anything helpful, don't worry this will be changed!</i></div>

## Introduction
Nearly everything you can see and touch in Half-Life 2: Garry's Mod Edition is an Entity.  Any object with a position in the game world is an Entity.  The Player is an Entity, props are Entities, even the the Game World itself is an Entity—albiet a special and unique one.

Entities are able to have custom, developer-defined behaviors that can control things like the way they look and the way they can be interacted with.  Entities are often foundational parts of Gamemodes and Addons
## Setup
### File Location
The file(s) that make up an Entity should be placed in an Addon
#### Addon Entity Location
```
addons/
	├── my-addon-name/
    │	├── lua/
    │	│   ├── entities/
	│	│   │   └── ...
```
### File Structure
```
entities/
   ├── my-entity-name/
   │   ├── cl_init.lua
   │   ├── init.lua
   │   └── shared.lua
```
## Creating an Entity
#### shared.lua example:
```lua
-- Defines the Entity's type and name for shared access (both server and client)
ENT.Type = "CPhysicsProp" -- Sets the Entity type to 'CPhysicsProp', indicating it's an scripted Entity.
ENT.Name = "Test Entity" -- The name that will appear in the spawn menu.
ENT.Spawnable = true -- Specifies whether this Entity can be spawned by players in the spawn menu.
```
#### init.lua example:
```lua
include("shared.lua")

-- Server-side initialization function for the Entity
function ENT:Initialize()
    self:SetModel( "models/custom_props/hl2gmed.mdl" ) -- Sets the model for the Entity.
    self:SetMoveType( MOVETYPE_VPHYSICS ) -- Sets how the Entity moves, using physics.
    self:SetSolid( SOLID_VPHYSICS ) -- Makes the Entity solid, allowing for collisions.
end
```
#### cl_init.lua example:
```lua
include("shared.lua")

-- Client-side draw function for the Entity
function ENT:DrawModel( flags )
end

-- Client-side think function for the Entity
function ENT:ClientThink()
end
```
