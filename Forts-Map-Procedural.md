[Forts scripting API](https://www.earthworkgames.com/content/docs/FortsAPI.html)
>[!example] Task
>Making aim trainer with procedurally generated floating enemy bases
### Knowledge
##### Code
- Mission scripts don't work in sandbox - use Skirmish or Multiplayer for testing.
- Reloading the map in multiplayer/skirmish game is enough to test the changes.

##### Design
>[!algorithm] Brainstorming process
>First working with terrain *(and its randomized placement)*, then with structures

[[Forts-Map-Procedural-Placeholder]]
##### Debugging
Use Forts API's `Log()` as a `print()` debugger.
Negative value *(usually `-1`)* is a sign for the terminal to output an Error ~~... scripts/mission.lua for team -1~~
# Terrain
1. Making the initial shape, adding texture to the block. *(optionally: splitting the block in two to have a dedicated mine space)*
>[!warning] My initial problem - i.e. why I couldn't texture blocks even though I don't get any errors
>Didn't use `UpdateGroundTriangles` as stated in the [Forts' API](https://www.earthworkgames.com/content/docs/FortsAPI.html#AddBlockVertex)
1. Creating 7 blocks in predefined spots:
```lua
function SpawnTerrain(coords, terPositions)

	for _, terPosition in ipairs(terPositions) do
		local blockIndex = CreateBlock()

		for _, coord in ipairs(coords) do
			local absoluteCoord = { x = coord["x"]+terPosition["x"], y = coord["y"]+terPosition["y"] }
			local vertexIndex = AddBlockVertex(blockIndex, absoluteCoord , 0)
		end

		SetBlockTexture(blockIndex, terrainName)
	end
end
```
*- Adding randomness in this code is ez*
>[!warning] My initial problem
>Instead of having  `{ x = coord["x ... }` [[Lua-Key|table keys]] I had an [[Lua-Table-Array|table-array]] with `1`, `2` keys *(instead of `x` and `y`)*: `{ coord["x ... }`
# Structures
### Loading structure files
>[!definition] Structure files 
`.spr` file in the `/maps/MAPNAME/FILENAME.spr` folder.
`LoadStructureFile()` - the function for loading structure files.
 
Create a "dummy map" with base that interests my and copy the structure file into my base map.

>[!graveyard]- Precautions
>The nodes cannot [[coincide]] with any existing node ID's. You'll have to intentionally manipulate the node ID's by spamming structure to ensure they don't coincide.
>On the base map, spam nodes until it's well above whatever the highest base is. Node ID's are never reused so it's important that they start high, essentially reserving space for loaded structure files *(which DO reuse)*
>It might also be worth recreating the same base $x$[^1] times

[^1]: It's how many times you want to spawn it in.

>[!warning] Issue
>I can't load structure files and place bases where I want - the placement is predefined and is the same as the "dummy map"

>[!tip] I can load single node bases and then "expand" them where I need
### Creating structures programmatically 
- I can't move foundations nodes

>[!warning] Issue
>There is no basic function to create a structure out of nothingness, you always need at least one node to start with.

>[!example] Idea
>Making 7 "root" nodes that I'll move *(if possible)* then "expand" the rest of the base per node *(7 bases in total)*
##### Making singular node
>[!example] 
>```lua
>local createdNodeId = CreateNode(102, "bracing", 55, { x = 800, y = -1100})
>local result = CreateLink(102, "bracing", createdNodeId, 55)
>```
>*- Don't forget `""` for the material name*

>[!tip] Asca - different solutions
>Create a mod with special material for making temporary struts. Use `SaveName` for picking material type.
>1. Build helping struts from the "mother" fort
>2. Use `.spr` files for spawning singles nodes and building helping structure from those

>[!look]
>If I just create a node *(without linking)* then I don't need to care about collision