# How to install/about wine on mac

As this question keeps appearing more recently I'm making this basic guide.
&NewLine;
&NewLine;
</br>
</br>
__Prerequisites:__
- Install [XQuartz 2.7.7](https://www.xquartz.org/releases/index.html) or above
- [Gatekeeper must allow block unsigned packages](https://www.imore.com/how-open-apps-anywhere-macos-catalina-and-mojave)
- Running OS X 10.8 to macOS 10.14* ([macOS Catalina](https://github.com/Gcenx/wine-on-mac#im-running-macos-catalina-how-do-i-use-wine))

## Recommended way to install Winehq packages;
Installing wine using [homebrew](https://docs.brew.sh/Installation)
Once homebrew is installed you the following command to install your selected wine package
```
brew cask install xquartz wine-staging
```
The above command will install `XQuartz` and the most recent `wine-staging` pkg available on winehq but it will also add `wine` for use in `Terminal` meaning you no longer need to launch the installed __Wine Staging__ app each time you want to access wine.  
__Please Note__  
Only a single wine package can be installed using `brew`

### How to manually install wine on mac using Winehq releases;
Grab a [wine package](https://dl.winehq.org/wine-builds/macosx/download.html) usually using the latest `wine-devel` is recommended, but most agree it's best to use the latest `wine-staging` due to additional patches.
If your intention is to have a more stable environment use `wine-stable`

The above is the __Winehq__ way to install wine on mac but that makes it cumbersome to use considering you must launch the `Wine Stable`, `Wine Devel` or `Wine Staging` app each time to get access to wine within `Terminal`
&NewLine;
&NewLine;
</br>
</br>
## Wine basics
The default `WINEPREFIX` will be `~/.wine` so anything you install will be placed into the hidden `~/.wine` folder.
You can override this by using the `WINEPREFIX` command

The default architecture of a `WINEPREFIX` will be 64Bit meaning 32Bit and 64Bit applications & games are supported but that's not always ideal for several reasons.
A new `WINEPREFIX` can be created and also setting `WINEARCH`

Here is an example of using both commands to create a 32Bit only `WINEPREFIX`

```
WINEARCH=win32 WINEPREFIX=~/.wine32 winecfg
```
The above command will create a new `WINEPREFIX` thats also 32Bit only and launch `winecfg`

#### Basic wine tools
- wine (32Bit loader)
- wine64 (64Bit loader)
- msiexec (execute msi files
- notepad
- regedit (Wines Registry editor)
- regsvr32 (Provides DLL registration services)
- wineboot
- winecfg (wine configuration utility)
- wineconsole (windows like shell aka cmd)
- winedbg (wine debug utility)
- winefile (wine file manager)
- winemine (wines version of the game mine)
- winepath
&NewLine;
</br>

## What's this winetricks everyone keeps saying to use?
*Winetricks is an easy way to work around problems in Wine.*

While `winetricks` *can* be installed directly from [GitHub](https://github.com/Winetricks/winetricks) you will be missing packages `winetricks` requires, instead install again using `homebrew`
```
brew install winetricks
```
Now you will also have access to `winetricks` command within `Terminal`
&NewLine;
&NewLine;
</br>
</br>
## Why doesn't __Virtual Desktop__ work?
By default wine on mac uses what's known as *mac driver* using `winetricks`  run the following command
```
winetricks macdriver=x11
```
This will swap from `mad driver` to `x11` now wine will make use of `XQuartz` 
&NewLine;
&NewLine;
</br>
</br>
## Why doesn't my game work on mac but Winehq says it does?
This usually happens when the game uses DirectX10 or above, the version of OpenGL included on macOS hasn't been updated in years so its missing some needed extensions.
&NewLine;
&NewLine;
</br>
</br>
## Can I use DXVK on mac?
No not currently.  
`MoltenVK` is currently Vulkan 1.0 compliant, without additional extensions needed by DXVK, newer versions of DXVK require Vulkan 1.1.  
`MoltenVK` uses Metal meaning only `wine64` has Vulkan support (currently `wine32on64` doesn't support MoltenVK).
&NewLine;
&NewLine;
</br>
</br>
## I'm running macOS Catalina, how do I use wine?
The short answer is you don't.
Currently only CrossOver-19 and above function on macOS Catalina.

However there are some free alternatives;
- [Unofficial Wineskin](https://github.com/Gcenx/WineskinServer/releases) Use a WS11 Engine
- [PortingKit](http://portingkit.com/) Should automatically select a working Engine
- My brew tap 
```
brew tap gcenx/wine && brew cask install wine-crossover
```
All require changing security settings from Recovery Mode
macOS Catalina 10.15.4 can use the following;
```
nvram boot-args="no32exec=0"
```
This will allow `wine32on64` to change the state of `i386_set_ldt`
macOS Catalian 10.15.3 and below SIP needs to be disabled

Phoenicis has a build of [WineCX19.0.0](https://www.playonlinux.com/wine/binaries/phoenicis/cx-darwin-x86on64/PlayOnLinux-winecx-19.0.0-cx-darwin-x86on64.tar.gz) but the PlayOnMac GUI currently doesn't function and dylibs aren't mapped correctly this needs to be done manually

__Please Note__
`wine32on64` currently does not support 16Bit executable so some things just won't work 
&NewLine;
&NewLine;
</br>
</br>
## How to build wine from source;
*__TODO__*
&NewLine;
&NewLine;
</br>
</br>
Found this information helpful?  
[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://paypal.me/gcenx?locale.x=en_US)
