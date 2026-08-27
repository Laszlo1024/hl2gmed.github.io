## Introduction

### What are Entities?

Nearly everything you can see and touch in Half-Life 2: Garry's Mod Edition is an Entity.  Any object with a position in the game world is an Entity.  The Player is an Entity, props are Entities, even the the Game World itself is an Entity—albiet a special and unique one.

Entities are able to have custom, developer-defined behaviors that can control things like the way they look and the way they can be interacted with.  Entities are often foundational parts of Gamemodes and Addons

### What are the components of an Entity?

Entities have aspects in all 3 Realms

* **Client** - Drawing/Rendering the Entity.
* **Server** - Controling the Entity's behavior and interactions.
* **Shared** - Configuration and properties available to both Server and Client Realms.

Shared isn't really a Realm. It only means that both Client and Server will run the same code that's in a Shared file.

## Setup

### File Location

The file(s) that make up an Entity should be placed either in an Addon or in a Gamemode.  

#### Addon Entity Location
```
addons/
	├── my-addon-name/
    │	├── lua/
    │	│   ├── entities/
	│	│   │   └── ...
```


#### Gamemode Entity Location
```
gamemodes/
	├── my-gamemode-name/
    │	├── entities/
    │	│   ├── entities/
	│	│   │   └── ...
```

### File Structure

Entities can be created either using 
* 3 separate files that each contain one Realm's code and configuration.
	* This approach helps with code organization.
	* The name of the folder containing these files (`my-entity-name` in the example below) will be used as the Entity's <page text="Class Name">Entity:GetClass</page>.
* The files are:
	* `cl_init.lua`
		* The Client Realm
	* `init.lua`
		* The Server Realm
	* `shared.lua`
		* The Shared Realm

```
entities/
   ├── my-entity-name/
   │   ├── cl_init.lua
   │   ├── init.lua
   │   └── shared.lua
```

## Creating an Entity

### Creating an Entity with separate files

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

ENTITY:Initialize() and ENTITY:DrawModel() are considered Hooks. These aren't clickable in the above examples, but you can search for hooks by typing `  is:event` (two spaces) into the top left of this page.

Whenever these Hooks are called by the game, your Entity runs the code you’ve defined for them. They're typed ENT here in order to register your entity's object class.
