>[!warning] Rope node is 60 metal *(regular is 50)*
>Thus try using "double wood" connection when possible
##### Peculiarities
1. It has high angular limit - this is why [[Coreswing|coreswings]] work
##### Uses
**Rope to wood:** making a rope *(max 109 energy)* connecting to the ground node and converting it to wood.[^1]
**But:** the ground node for a rope is 60 metal, for regular foundation it's 50.

[^1]: So you won't waste resources on making wooden obstructions

### Reverse engineering the physics
```lua
Stiffness = 50000 -- armor is 250000
SpringDamping = 100,
AirDrag = 0.9,
MaxCompression = 0.6, -- armor is 0.9
MaxExpansion = 1.5, -- armor is 1.1
Pretension = 0.02,
MinLength = 100,
MaxLength = 800,
MaxSegmentLength = 75,
Mass = 0.001,
HitPoints = 50,
ReflectionMomentumThreshold = 30,
RicochetVariationFactor = 0,
SpeedLossFactor = 1,
RequiresFoundationSupport = false,
AttachesCladding = false,
SupportsDevices = false,
AlignedLinksAllowed = true,
CanBeTempBraced = false,
ReflectsBeams = false,
CatchesFire = true,
ShowEndFireSegments = true,
DegreesPerSecondMin = 20,
DegreesPerSecondMax = 100,
FireLateralOffsetStdDev = 3,
CollidesWithFriendlyProjectiles = false,
CollidesWithEnemyProjectiles = false,
CollidesWithFriendlyBeams = false,
CollidesWithEnemyBeams = true,
AngleStressPrimaryThreshold = 360, -- no breakage
AngleStressSecondaryThreshold = 360,
Node = CableNode,
IsBehindDevices = false,
CollidesWithWind = false,
ConductsPower = false,
KeySpriteByDamage = true,
NodeImpacts =
```