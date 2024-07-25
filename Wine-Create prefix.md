[[Forts-Linux Issue]] ;;up
`sudo apt install wine-stable winetricks` - install wine
**Wine prefix** - special folder with wine-specific files and windows stuff.
There is usually 1 untinkered wine prefix
>[!tip]
>It's good to have multiple wine prefixes to run specific versions of Windows.

### Create 32-bit Wine prefix
`WINEPREFIX` - command to create prefixes.
`Winearch=win32 WINEPREFIX="/path/here" winecfg`
A new folder with with whatever the name you want will be created. Here may appear multiple GUI prompts to install stuff.

>[!example] For forts
>Backup `Steam` folder in prefix:
>```
>cd ~/.steam/steam/steamapps/compatdata/213610/
>cp -r pfx/drive_c/Program\ Files\ \(x86\)/Steam/ ~/Desktop 
>```
>Create a new wine prefix:
>```
>WINEPREFIX=$PWD/pfx WINEARCH=win32 winecfg 
>mkdir pfx/drive_c/windows/syswow64 # proton crashes if you don't do this
>cp -r ~/Desktop/Steam pfx/drive_c/Program\ Files/ # copy 
>```
>Go to Proton-Experimental [[Directory]] and [[sed|edit the stream]]
>```
>sed -i 's/wine64/wine/' proton # because proton defaults to wine64 binary
>```
#### 
[[Microsoft-DOTNET]]