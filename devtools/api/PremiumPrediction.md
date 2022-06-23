# PremiumPrediction API

### Namespace - _G.PremiumPrediction

#### Example
```lua
	local spellData = {speed = 1800, range = 1200, delay = 0.25, radius = 60, collision = {"minion"}, type = "linear"}	
	local prediction = _G.PremiumPrediction:GetPrediction(myHero, unit, spellData)
```

#### Structure
##### Spell Data
- Speed - _projectile speed_
- Range - _maximum projectile travel distance_
- Dange - _animation time for cast(time between button pressed and projectile appearing)_
- Radius - _width of the projectile (Ezreal Q is 120 units wide), or collision radius(spherical spells, Ziggs Q - 150 units)_
- Angle - _only used with conic spells_
- Collision - _array of what the projectile can hit (values: "windwall", "hero", "minion")_
- Type - _projectile type (values: "linear", "circular", "conic")_

Example
```lua
local ezrealQSpellData = {speed = 1200, range = 2000, delay = 0.25, radius = 120, type = "linear", collision = {"minion", "hero", "windwall"}} 
local cassiopeiaRSpellData = {speed = math.huge, range = 850, delay = 0.5, angle = 80, type = "conic", collision = {"windwall"}} 
```
Spells info can be found at https://leagueoflegends.fandom.com. Example: https://leagueoflegends.fandom.com/wiki/Zeri/LoL

##### HitChance values
In API represented as functions. HitChance can be used as `HitChance.High(valueFromPrediction)` and will return a boolean, did pass a HitChance.High check
| Key | Value |
| ------ | ------ |
| Impossible | -2 |
| Collision | -1 |
| OutOfRange | 0 |
| Low | > 0 |
| Medium | >= 0.25 |
| High | >= 0.5 |
| VeryHigh | >= 0.75 |
| Dashing | 1 |
| Immobile | 1 |
	


### API
##### Brief oveview 
Namespace for library is PremiumPrediction. Accesed by `_G.PremiumPrediction:Method()`
Example `var isMoving = _G.PremiumPrediction:IsMoving(enemy)`
#### Available functions
```
Loaded()
        returns boolean if script has initialized
    
PredictUnitPosition(source, unit, spellData)
        returns {CastPos, PredPos, TimeToHit, CanHit}
    
GetPrediction(source, unit, spellData)
        returns {CastPos, PredPos, HitChance, HitCount, TimeToHit}
    
GetAOEPrediction(source, unit, spellData) 
        returns {CastPos, PredPos, HitChance, HitCount, TimeToHit}
    
GetDashPrediction(source, unit, spellData)
        returns {CastPos, PredPos, TimeToHit, CanHit}
        
GetFastPrediction(source, unit, spellData)
        returns PredPos
    
GetHitChance(source, unit, castPos, spellData, timeToHit, canHit) 
        returns HitChance
    
GetImmobileDuration(unit)
        returns duration (in seconds)
    
GetMEC(points)
        returns {Center, Radius}
     
GetMovementSpeed(unit)
        returns speed (units per second)
    
GetPositionAfterTime(unit, time)
        returns future position (3D Vector)
    
GetWaypoints(unit)
        returns table with waypoints
    
IsColliding(source, position, spellData, flags, exclude)
        returns table of units or false
    
IsDashing(unit)
        returns boolean
    
IsFacing(source, unit, angle)
        returns boolean
    
IsMoving(unit)
        returns boolean
    
IsPointInArc(sourcePos, unitPos, endPos, range, angle)
        returns boolean
    
OnDash(unit, function)
        calls function when unit started dashing
    
OnGainVision(unit, function)
        calls function when unit has been revealed
    
OnLoseVision(unit, function)
        calls function when unit has disappeared
    
OnProcessSpell(unit, function)
        calls function when unit has casted channeling spell
    
OnProcessWaypoint(unit, function)
        calls function when unit has changed pathing
    
To2D(position)
        converts 3D vector to 2D Point {x, y}
    
To3D(point, height)
        converts 2D Point {x, y} to 3D Vector
    
HitChance.<Name>(hitChance)
        returns boolean if <Name> matches given HitChance
```

#### Parameters breakdown
**source** - origin of calculation or Obj_AI_Base, spell cast position
**source** - origin of calculation, spell cast position
