# Introduction

In this tutorial we will create a weapon that fires chairs.

#  File Layout 

* Open your half-life 2: garry's mod edition folder. 
* Open the 'addons' folder.
* Create a folder called 'chairlauncher'
* Create a folder inside called 'lua'
* Create a folder inside called 'weapons'
* Create a folder inside called 'weapon_chairgun'
* Create a file called 'shared.lua

Your folder structure should be like this:

```

  hl2gmed/addons/chairlauncher/lua/weapons/weapon_chairgun
```


You have created an addon called **chairlauncher** which contains a weapon called **weapon_chairgun**. Whenever you create a new weapon, most people use the **weapon_** prefix, since most of the default weapons names also start with **weapon_**.

#  The Code 

Add these to your weapon after you understand them.

##  Informational 

This code is just informational. It shows up in the spawnmenu and the weapon selection menu.. so it will help people out if your weapon is complicated to use. You can also put your name in the author field so people know who made it.


```lua
SWEP.PrintName			= "Chair Thrower" -- This will be shown in the spawn menu, and in the weapon selection menu
```


##  Spawn Info 

Defines whether players can spawn this weapon from the spawnmenu.. and whether only admins can spawn it.


```lua
SWEP.Spawnable = true
SWEP.AdminOnly = true
```


##  Clip Info 

Our weapon doesn't use any ammo or clips, so we just set the clip sizes to -1 and the ammo to "none".

We set primary to be automatic. This means that the player doesn't have to release the mouse button and press it again - it will continually fire.


```lua
SWEP.Primary.ClipSize		= -1
SWEP.Primary.DefaultClip	= -1
SWEP.Primary.Automatic		= true
SWEP.Primary.Ammo		= "none"

SWEP.Secondary.ClipSize		= -1
SWEP.Secondary.DefaultClip	= -1
SWEP.Secondary.Automatic	= false
SWEP.Secondary.Ammo		= "none"
```


##  More Info 

These are mostly self explanatory. The higher the weight the more likely you are to switch to it. Slot and SlotPos decide where in your weapon menu the weapon will be.


```lua
SWEP.Weight			= 5
SWEP.AutoSwitchTo		= false
SWEP.AutoSwitchFrom		= false

SWEP.Slot			= 1
SWEP.SlotPos			= 2
SWEP.DrawAmmo			= false
SWEP.DrawCrosshair		= true
```


##  Models 

The view-model and the world-model to use.


```lua
SWEP.ViewModel			= "models/weapons/v_pistol.mdl"
SWEP.WorldModel			= "models/weapons/w_pistol.mdl"
```



##  Sounds 

```lua
SWEP.ShootSound = "Metal.SawbladeStick"
```


##  The actual chair throwing code 

Commented for your learning pleasure


```lua
-- Called when the left mouse button is pressed
function SWEP:PrimaryAttack()
	-- This weapon is 'automatic'. This function call below defines
	-- the rate of fire. Here we set it to shoot every 0.5 seconds.
	self.m_flNextPrimaryAttack = gpGlobals.curtime() + 0.5

	-- Call 'ThrowChair' on self with this model
	self:ThrowChair( "models/props/cs_office/Chair_office.mdl" )
end
 

-- Called when the rightmouse button is pressed
function SWEP:SecondaryAttack()
	-- Though the secondary fire isn't automatic
	-- players shouldn't be able to fire too fast
	self.m_flNextSecondaryAttack = gpGlobals.curtime() + 0.1

	self:ThrowChair( "models/props_c17/FurnitureChair001a.mdl" )
end

-- A custom function we added. When you call this the player will fire a chair!
function SWEP:ThrowChair( model_file )
	local owner = self:GetOwner()

	-- Make sure the weapon is being held before trying to throw a chair
	if ( ToBaseEntity( owner ) == NULL ) then return end

	-- Play the shoot sound we precached earlier!
	self:EmitSound( self.ShootSound )

	-- Create a prop_physics entity
	local ent = ToCPhysicsProp( CreateEntityByName( "prop_physics" ) )

	-- Always make sure that created entities are actually created!
	if ( ToBaseEntity( ent ) == NULL ) then return end

	-- Set the entity's model to the passed in model
	ent:SetModel( model_file )

	-- This is the same as owner:EyePos() + (self:GetOwner():GetAimVector() * 16)
	-- but the vector methods prevent duplicitous objects from being created
	-- which is faster and more memory efficient
	-- AimVector is not directly modified as it is used again later in the function
   local aimvec = owner:Weapon_ShootPosition();

	local forward = Vector()
	local right = Vector()
	local up = Vector()
	
	owner:EyeVectors( forward, right, up )

	-- Set the position to the player's eye position plus 16 units forward.
	ent:SetAbsOrigin( aimvec + forward * 16  )

	-- Set the angles to the player'e eye angles. Then spawn it.
	ent:SetAbsAngles( owner:GetAbsAngles() )
	ent:Spawn()
 
	-- Now get the physics object. Whenever we get a physics object
	-- we need to test to make sure its valid before using it.
	-- If it isn't then we'll remove the entity.
	local phys = ent:VPhysicsGetObject()
	if ( phys == NULL ) then ent:Remove() return end
 
	-- Now we apply the force - so the chair actually throws instead 
	-- of just falling to the ground. You can play with this value here
	-- to adjust how fast we throw it.
	-- Now that this is the last use of the aimvector vector we created,
	-- we can directly modify it instead of creating another copy
	phys:ApplyForceCenter( ent:GetForward() * 1000 )
 
	timer.Simple( 10, function() if ToBaseEntity( ent ) ~= NULL then ent:Remove() end end )
end
```


# Challenges

Can you edit the new weapon to:

* Use a different firing sound for left/right click
* Throw a melon when you press reload? (tip: <page>WEAPON:Reload</page>)
* Throw 3 chairs at a time
