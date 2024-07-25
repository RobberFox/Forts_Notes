### Camera variables in `data/db/constant_user.lua`
>[!example] My configuration
>```lua
>View =
>{
>	UserScreen =
>	​{
>		TransitionTime = 0.0,
>		EaseFraction = 0.5,
>	},
>
>	Rates =
>	​{
>		MouseScroll = 0,
>		KeyboardScroll = 700,
>		MouseZoom = 0.003,
>		KeyboardZoom = 0.25,
>		CameraCatchup = 100.0,
>	},
>}
>```

**Transition Time** - time to pan when switching cameras *(0 = instant)*
**Ease Fraction** - is how whether it accelerates to do it, or maintains the same speed.


**MouseScroll** - screen edge mouse panning speed.
**KeyboardScroll** - WASD speed.
**MouseZoom** - zoom in/out speed.
**KeyboardZoom** - zoom in/out speed

**CameraCatchup** - Instant panning with cursor (which looks really jerky at 0) vs a slight lag, which is easier to follow.
##### Zoom in rate, Zoom out rate
