# How to install/about wine on mac

As this question keeps appearing more recently I'm making this basic guide.

#### Prerequisites;  
- Install [XQuartz 2.7.7](https://www.xquartz.org/releases/index.html) or above
- [Gatekeeper must allow block unsigned packages](https://www.imore.com/how-open-apps-anywhere-macos-catalina-and-mojave)
- Running OS X 10.8 to macOS 10.14* ([macOS Catalina](https://github.com/Gcenx/wine-on-mac#im-running-macos-catalina-how-do-i-use-wine))

## Recommended way to install Winehq packages;
Installing wine using [homebrew](https://docs.brew.sh/Installation)
Once homebrew is installed you the following command to install your selected wine package

```
brew cask install xquartz
brew tap homebrew/cask-versions
brew cask install --no-quarantine wine-staging
```
The above command will install `XQuartz` and the most recent `wine-staging` pkg available on winehq but it will also add `wine` for use in `Terminal` meaning you no longer need to launch the installed __Wine Staging__ app each time you want to access wine.
  
__Please Note;__  
Only a single wine package can be installed using `brew`  
The `--no-quarantine` command is required as homebrew by default adds the quarantine flag to downloaded casks, this causes Gatekeeper to treat the bundle as damaged.

Winehq is currently not providing recent packages for macOS so I decided to upload my own builds.

```
brew tap gcenx/wine
brew cask install --no-quarantine gcenx-wine-staging
```
This command will add my brew tap and the second command will install my custom cask of `Wine Staging`
#### The tap contains the following
- `gcenx-wine-stable`
- `gcenx-wine-devel`
- `gcenx-wine-staging`
- `wine-crossover`

### How to manually install wine on mac using Winehq releases;
Grab a [wine package](https://dl.winehq.org/wine-builds/macosx/download.html) usually using the latest `wine-devel` is recommended, but most agree it's best to use the latest `wine-staging` due to additional patches.  
If your intention is to have a more stable environment use `wine-stable`

The above is the __Winehq__ way to install wine on mac but that makes it cumbersome to use considering you must launch the `Wine Stable`, `Wine Devel` or `Wine Staging` app each time to get access to wine within `Terminal`

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

## What's this winetricks everyone keeps saying to use?
*Winetricks is an easy way to work around problems in Wine.*

While `winetricks` *can* be installed directly from [GitHub](https://github.com/Winetricks/winetricks) you will be missing packages `winetricks` requires, instead install again using `homebrew`

```
brew install winetricks
```
Now you will also have access to `winetricks` command within `Terminal`

## Why doesn't __Virtual Desktop__ work?
By default wine on mac uses what's known as *macDriver* using `winetricks`  run the following command

```
winetricks macdriver=x11
```
This will swap from `macDriver` to `x11` now wine will make use of `XQuartz` 

## Why doesn't my game work on mac but Winehq says it does?
This usually happens when the game uses DirectX10 or above, the version of OpenGL included on macOS hasn't been updated in years so it's missing some needed extensions.

## Can I use DXVK on mac?
No not currently.  
`MoltenVK` is Vulkan 1.1 compliant, but still missing additional extensions needed by DXVK.  
`MoltenVK` uses Metal meaning only `wine64` has Vulkan support (currently `wine32on64` doesn't support MoltenVK).

*__Please Note;__*  
CrossOver-20 does include DXVK support, this provides DirectX10 and DirectX11 support. CodeWeavers patched MoltenVK to fake unsupported extensions and a custom version of DXVK that's modified specifically for macOS.

## macOS Catalina/macOS Big Sur, how do I use wine?
Currently only CrossOver-19 and later will run

#### Here are some free alternatives;
 - [Unofficial Wineskin](https://github.com/Gcenx/WineskinServer/releases) Use a WS11 Engine
 - [PortingKit](http://portingkit.com/) Should automatically select a working Engine
 - My brew tap 

```
brew tap gcenx/wine && brew cask install --no-quarantine wine-crossover
```

Gatekeeper will give a warning for each Windows binary that is ran as these won't be code-signed in a way Apple expects, to avoid this you could disabled Gatekeeper using the following command

```
sudo spctl --master-disable
```
*__Please Note;__*  
macOS Catalina 10.15.0 to 10.15.3, [SIP](https://support.apple.com/en-us/HT204899) needs to be disabled this will allow `wine32on64` to change the state of `i386_set_ldt`

My current wine-crossover package can be downloaded directly [WineCX19.02](https://github.com/Gcenx/homebrew-wine/releases/download/19.0.2/wine-crossover-19.0.2-osx64.tar.7z)\
Phoenicis has a build of [WineCX19.0.0](https://www.playonlinux.com/wine/binaries/phoenicis/cx-darwin-x86on64/PlayOnLinux-winecx-19.0.0-cx-darwin-x86on64.tar.gz)

__Also;__  
`wine32on64` currently does not support 16Bit executable so some things just won't work 

## Apple Silicon support?
Only CrossOver-20.0.2 includes support for Apple Silicon at this time, this requires macOS Big Sur 11.1 and install Rosetta2.  
I will be adding support for Apple Silicon into [Wineskin](https://github.com/Gcenx/WineskinServer) once I'm able to obtain an M1 Mac mini, currently checking where would be the best place to purchase from.

## Using wine in a macOS Virtual Machine
From Wine-4.15 to Wine-5.16 macDriver (the default display driver) won't function within a Virtual Machine, however the X11 display driver works.\
You can edit the wine registry manually or use winetricks
```
winetricks macdriver=x11
```

*__Please Note;__*
The macDriver regression was resolved from Wine-5.17

## Wine-5.9 to Wine-5.18 file limit regression;
```
wineserver ran out of file handles, and the code in ntdll was missing a macos specific quirk...
```
The upstream patch was applied to my recently uploaded Wine-5.17 packages\
The most commonly noticed issues was wine-gecko was always crashing.

## How to build wine from source;
*__TODO__*
&NewLine;
&NewLine;
</br>
</br>
