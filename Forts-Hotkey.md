![[Layout-Forts.png]]

### For coding
```lua
local keyDown = {}
function OnKey(key, down)
  keyDown[key] = down and true or nil
  
  if  keyDown['left control']
  and keyDown['left shift']
  and keyDown['left alt']
  and keyDown['s'] then
    SendScriptEvent("LimitStorage", '', '', false)
  end
end
```

>[!warning] WIP
So the script event is triggered, when the player presses ctrl + alt + shift + s
So the relevant part is just the first 3 lines… then you have in keyDown just every currently pressed keys of the user…
So keyDown is a table that stores what keys are currently pressed down and so you can just check in the table if the key is currently pressed (so you can check multiple keys)