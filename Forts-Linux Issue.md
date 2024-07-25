### In game
**Abyss (sandbox):** disconnect at around `2:00` seconds. 
>[!example] `2:08`, `2:10`

**Vanilla (private lobby):** disconnect at around `2:00` seconds.
>[!example] `2:26`

### Notions
Speeding up the gaem *(in sandbox)* speeds up the crash appearance. It's "hardwired" to the ingame timer.
`Invalid handle` means that my Linux is not supporting some `win32` functions.
>[!definition] The names of the functions
`CreateToolhelp32Snapshot`
`Module32First`
`Module32Next`
`CloseHandle`
### Linux and those [[win32]] functions
[[API]]
[[ABI]]
##### Ubuntu discussion about dropping 32 bit support
https://discourse.ubuntu.com/t/dropping-32-bit-support-i-e-games-support-will-hurt-ubuntu-big-time/11420

>However, that said, there are some 32bit libraries you need to install on your system to get 32bit programs supported by Proton. There is a complete list of them over on the Proton github page. 
>https://steamcommunity.com/app/221410/discussions/8/1777136225027667054/?l=tchinese

##### Round #1
https://www.reddit.com/r/linux_gaming/comments/99e0kc/comment/efxvry0/
[[Wine-Create prefix]]

##### Round #2
>[!definition] Solution - snap store sucks
>Just download steam from the **official website** and it will download all necessary dependencies along with it.

**Additionally:** Vulkan doesn't affect my GTX1650 card.