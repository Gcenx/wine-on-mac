# How to install/about wine on mac

As this question keeps appearing more recently I'm making this basic guide.

#### Prerequisites;  
- [Gatekeeper must allow block unsigned packages](https://www.imore.com/how-open-apps-anywhere-macos-catalina-and-mojave)
- Running OS X 10.8 to macOS 10.14* ([macOS Catalina & later](https://github.com/Gcenx/wine-on-mac/blob/master/README.md#macos-catalina-and-later))

## Recommended way to install Winehq packages;
Installing wine using [homebrew](https://docs.brew.sh/Installation)
Once homebrew is installed you the following command to install your selected wine package

```
brew tap homebrew/cask-versions
brew install --cask --no-quarantine wine-staging
```
The above command will install the most recent `wine-staging` pkg available on winehq but it will also add `wine` for use in `Terminal` meaning you no longer need to launch the installed __Wine Staging__ app each time you want to access wine.
  
__Please Note;__  
Only a single wine package can be installed using `brew`  
The `--no-quarantine` command is required as homebrew by default adds the quarantine flag to downloaded casks, this causes Gatekeeper to treat the bundle as damaged.

### How to manually install wine on mac using Winehq releases;
Grab a [wine package](https://dl.winehq.org/wine-builds/macosx/download.html) usually using the latest `wine-devel` is recommended, but most agree it's best to use the latest `wine-staging` due to additional patches.  
If your intention is to have a more stable environment use `wine-stable`\
_Currenty WIP macOS packages are not uploaded to Winehq, those can be downloaded from [here](https://github.com/Gcenx/macOS_Wine_builds/releases)_

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

## Why doesn't my game work on mac but Winehq says it does?
This usually happens when the game uses DirectX10 or above, the version of OpenGL included on macOS hasn't been updated in years so it's missing some needed extensions.

## Can I use DXVK on mac?
No not currently.  
`MoltenVK` is Vulkan 1.1 compliant, but still missing additional extensions needed by DXVK.  
`MoltenVK` uses Metal meaning only `wine64` has Vulkan support (currently `wine32on64` doesn't support MoltenVK).

*__Please Note;__*  
CrossOver-20 and later include DXVK support, this provides DirectX10 and DirectX11 support. CodeWeavers patched MoltenVK to fake unsupported extensions and a custom version of DXVK that's modified specifically for macOS.

## macOS Catalina and later
Currently only CrossOver-19 and later suppot 32Bit on 64Bit only versions of macOS.

#### Here are some free alternatives;
 - [Unofficial Wineskin](https://github.com/Gcenx/WineskinServer/releases) Use a WS11 Engine
 - [PortingKit](http://portingkit.com/) Should automatically select a working Engine
 - My brew tap

Install the lastest `wine-crossover` package I provide from my brew tap;
```
brew install --no-quarantine gcenx/wine/wine-crossover
```

Gatekeeper will give a warning for each Windows binary that is ran as these won't be code-signed in a way Apple expects, to avoid this you could disabled Gatekeeper using the following command
```
sudo spctl --master-disable
```
*__Please Note;__*  
macOS Catalina 10.15.0 to 10.15.3, [SIP](https://support.apple.com/en-us/HT204899) needs to be disabled this will allow `wine32on64` to change the state of `i386_set_ldt`\
The current `wine-crossover` package can be downloaded directly [WineCX20.02](https://github.com/Gcenx/homebrew-wine/releases/download/20.0.2/wine-crossover-20.0.2-osx64.tar.7z)

__Also;__  
`wine32on64` does not support 16Bit executables so somethings just won't work 

## Apple Silicon support?
Only CrossOver-20.0.2 includes 32Bit support for Apple Silicon at this time, this requires macOS Big Sur 11.1 and Rosetta2 installed.\
Wine-6.0.1/Wine-6.1 only support 64Bit Windows Binaries at this time.

## How to build wine from source;
*__TODO__*
&NewLine;
&NewLine;
</br>
</br>
