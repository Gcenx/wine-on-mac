# How to install/about wine on mac

As this question keeps appearing more recently I'm making this basic guide.
&NewLine;
&NewLine;
</br>
</br>
### How to manually install wine on mac using Winehq releases;
Prerequisites:
- Install [XQuartz 2.7.7](https://www.xquartz.org/releases/index.html) or above
- [Gatekeeper must allow block unsigned packages](https://www.imore.com/how-open-apps-anywhere-macos-catalina-and-mojave)
- Running OS X 10.8 to macOS 10.14* ([macOS Catalina](https://github.com/Gcenx/wine-on-mac#im-running-macos-catalina-how-do-i-use-wine))

Grab a [wine package](https://dl.winehq.org/wine-builds/macosx/download.html) usually using the latest `wine-devel` is recommended, but most agree it's best to use the latest `wine-staging` due to additinal patches.
If your intention is to have a more stable envirument use `wine-stable`

The above is the __Winehq__ way to install wine on mac but that makes it cumbersome to use considering you must launch the `Wine Stable`, `Wine Devel` or `Wine Staging` app each time to get access to wine within `terminal`
&NewLine;
&NewLine;
</br>
</br>
## Recommended way to install Winehq packages;
An alternative is installing wine using [homebrew](https://docs.brew.sh/Installation)
Once homebrew is installed you the following command to install your selected wine package
```
brew cask install xquartz wine-staging
```
The above command will install `XQuartz` and the most recent `wine-staging` pkg available on winehq but it will also add `wine` for use in `terminal` meaning you no longer need to launch the installed __Wine Staging__ app each time you want to access wine.
&NewLine;
&NewLine;
</br>
</br>
## What's this winetricks everyone keeps saying to use?
*Winetricks is an easy way to work around problems in Wine.*

While this can be installed directly from [GitHub](https://github.com/Winetricks/winetricks) you will be missing common packages required to make use to winetricks instead install again using `homebrew`
```
brew install winetricks
```
Now you will also have access to `winetricks` command within `terminal`
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
Not currently, wine on mac can only function on wine64 using MoltenVK running 10.11 and above, currently it's missing required Vulkan extensions to support DXVK so for now it's not possible, also Winehq builds aren't built with MoltenVK support.
&NewLine;
&NewLine;
</br>
</br>
## I'm running macOS Catalina, how do I use wine?
The short answer is you don't.
Currently only CrossOver-19 and above function on macOS Catalina.

However there are some free options but all require SIP to be disabled
- [Unofficial Wineskin](https://github.com/Gcenx/WineskinServer/releases) Use a WS11 Engine
- [PortingKit](http://portingkit.com/) Should automatically select a working Engine
- My brew tap 
```
brew tap gcenx/wine && brew cask install wine-crossover
```
Alternatively Phoenicis has a build for [WineCX19.0.0](https://www.playonlinux.com/wine/binaries/phoenicis/cx-darwin-x86on64/PlayOnLinux-winecx-19.0.0-cx-darwin-x86on64.tar.gz) but the PlayOnMac GUI currently doesn't function and dylibs aren't mapped correctly that needs to be done manually
&NewLine;
&NewLine;
</br>
</br>
## How to build wine from source;
Might add later
