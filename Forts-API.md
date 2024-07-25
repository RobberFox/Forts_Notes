No API functions return multiple values so if it has multiple values it’s in a table

>[!definition] There are two types of functions in the API:
>1. Functions you can call so something happens 
>2. Functions in your script that are called by the game on specific events. So in fact they are event callbacks.

Every mod "runs" somewhat like in it's own sandbox or better say scope. So you don't overwrite any existing "On…" function. You just define what shall happen, when that event occurs and the game tries to call this callback function in your code.
### Events, event functions, event callbacks
https://www.earthworkgames.com/content/docs/FortsAPI.html#events
>[!example] `Load()`, `Update()` - are also event functions
>`Load()` - called when the client is loading the game *(can be at start or when you join later in game)*. 
>`Update()` - called each physical frame[^1]. Every game relevant action happens in a physical frame. 
>There are also graphical frames *(that depend on your hardware)* that can be $><25$. The function for that is `OnUpdate()`

[^1]: Default Forts has 25 physical frames per second *(so game/physic relevant stuff only happens in 1/25 portions)*.

>[!example] Calling event functions on their own, to avoid code replication
>```lua
>function OnDeviceHit(teamId, deviceId, saveName, newHealth, projectileNodeId, projectileTeamId, pos, reflectedByEnemy)
>    if someReasonToBeThatWay then
>        ApplyDamageToDevice(deviceId, newHealth-1)
>    end
>end
>
>function OnDeviceHitBeam(teamId, deviceId, saveName, newHealth, weaponId, projectileSaveName, pos)
>    OnDeviceHit(teamId, deviceId)
>end
>```
>`OnDeviceHit()` event function does something that was told to do, then we "kinda merge events into one whole" by calling `OnDeviceHit()` inside `OnDeviceHitBeam()`