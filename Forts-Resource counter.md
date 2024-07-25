[Forts scripting API](https://www.earthworkgames.com/content/docs/FortsAPI.html)
[[Forts-Map-Procedural]] ;;x
>[!example] Task
>Making a togglable, clearable resource expenditure counter.
### Knowledge
`AddTextControl()` - function for outputting text in the window
`GetLinkCost()` - returns the cost of building a new strut.
##### Design
Track the cost (metal and energy separately) of newly built structures, append it to a sum. The value of the sum I'll output with `AddTextControl()` and update with `SetControlText` every time I build a strut. I'll implement the ability to clear the counter by zeroing the sum after a given shortcut combination. The main problem is that I don't know how to track the cost of every newly plank a build, is `GetLinkCost()` responsible for that?
### Script
```lua
dofile("scripts/forts.lua")

local expenditure = { metal=0, energy=0 }

function Load()
	AddTextControl("", "MetalExpenditure", "Metal = 0", ANCHOR_TOP_LEFT, Vec3(600, 10, 0), false, "Heading")	
	AddTextControl("", "EnergyExpenditure", "Energy = 0", ANCHOR_TOP_LEFT, Vec3(600, 40, 0), false, "Heading")	
end 

function OnRestart()
end

function Update()
	SetControlText("", "MetalExpenditure", "Metal = " .. string.format("%.1f", expenditure.metal))
	SetControlText("", "EnergyExpenditure", "Energy = " .. string.format("%.1f", expenditure.energy))
end


local lastNodeWasFoundation = false
function OnNodeCreated(nodeId, teamId, pos, foundation, selectable, extrusion)
	if teamId == GetLocalTeamId() then
		lastNodeWasFoundation = foundation
  	end
end

function OnLinkCreated(teamId, saveName, nodeA, nodeB, pos1, pos2, extrusion)
	if teamId == GetLocalTeamId() then
    		local costs = GetLinkCost(nodeA, pos2, saveName, lastNodeWasFoundation)
    		expenditure.metal  = expenditure.metal  + costs.metal
    		expenditure.energy = expenditure.energy + costs.energy
    		lastNodeWasFoundation = false
	end
end

local keyDown = {}
function OnKey(key, down)
	keyDown[key] = down and true or nil
	if  keyDown['left control'] and keyDown['z'] then
		expenditure = { metal=0, energy=0 }
	end
end

```
### Enhancements
##### Not accounting conversion from fg to bg bracing
`GetLinkMaterialSaveName(nodeIdA, nodeIdB)` - query the `SaveName` of the material connecting 2 nodes.
>[!example] 'In code' differences between conversion and newly created link
>**Conversion** - a material ==already existed== before the "overriding" background bracing creation.
>**Newly created link** - there was no material before the background bracing creation.

>[!algorithm] 
>