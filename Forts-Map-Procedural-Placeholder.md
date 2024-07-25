![[Pasted image 20240325195612.png]]
>[!tip] The Idea
[[Lua-Table|Table]] of coordinates $(x;y)$ with relative positions.

```lua
positions = {
    {x = 200, y = 150},
    {x = 300, y = 150},
    {x = 300, y = 300},
    {x = 200, y = 300}
}
```
And then you could loop through it, like:
```lua
-- for terrainPos, parse the position that you want to spawn the block
-- for coords, parse the previously established positions table
function SpawnTerrain(terrainPos, coords)
    local blockIndex = CreateBlock()
   
    for _, coord in pairs(coords) do
        local vertex = AddBLockVertex(blockIndex, coord, 0) -- last parameter controls the edge type, play around with this
    end
end
```
Use [GetRandomInteger](https://www.earthworkgames.com/content/docs/FortsAPI.html#GetRandomFloat) and [GetRandomFloat](https://www.earthworkgames.com/content/docs/FortsAPI.html#GetRandomInteger) for random numbers, do not use the in built random functions
