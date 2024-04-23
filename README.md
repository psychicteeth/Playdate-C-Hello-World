# Playdate-C-Hello-World

Goal: An empty playdate C/Lua project that can be built to the device and to the simulator in VS Code on Windows and Mac.

Status: More or less complete! Builds simulator and device binaries on Windows and Mac in the default build tasks.

## Project setup

The build tasks simply execute the command line instructions from [Inside Playdate With C](https://sdk.play.date/2.1.1/Inside%20Playdate%20with%20C.html#_command_line). If you are having trouble with this project, please check there to see if there are any useful bits of information I may have missed here. Or give me a shout on here or discord (.alexmay).

### macOS

1. Install the Playdate SDK
    1. https://play.date/dev/
    2. Set the environment variable PLAYDATE_SDK_PATH to the path where you install the SDK.
    3. (May be unnecessary?) Set PLAYDATE_ARM_GCC to the location of the arm GCC toolchain installed with the SDK.
2. Install CMake
    1. https://cmake.org/download/ or use homebrew https://brew.sh/
    2. Make sure cmake can be executed from a terminal/command prompt. If not, add the path to the cmake executable to your PATH environment variable.
3. Install VS Code
    1. https://code.visualstudio.com/download
    2. Extensions to install: 
        1. C/C++ (ms)
        3. Lua (sumneko)
        4. Playdate debug (midouest)    
        5. You do NOT need to install the cmake tools / cmake extensions to build playdate software with this repo.

### Windows

1. Install the Playdate SDK
    1. https://play.date/dev/
    2. Set the environment variable PLAYDATE_SDK_PATH to the path where you install the SDK.
1. Install CMake
    1. https://cmake.org/download/ 
    2. Make sure cmake can be executed from a terminal/command prompt. If not, add the path to the cmake executable to your PATH environment variable.
3. Install VS Code
    1. https://code.visualstudio.com/download
    2. Extensions to install: 
        1. C/C++ (ms)
        3. Lua (sumneko)
        4. Playdate debug (midouest)    
        5. You do NOT need to install the cmake tools / cmake extensions to build playdate software with this repo.
1. We need nmake. If you do not have a version of Visual Studio (not Code) installed, you will need to install the MSVC compiler toolset:
    [1. https://code.visualstudio.com/docs/cpp/config-msvc](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2022)
2. Set the VISUAL_STUDIO_TOOLS environment variable to the path to vcvars64.bat. One way to find this is detailed below:
    1. You can find the location of it by going to the start menu, typing "x64 Native" and seeing what comes up.
    2. Right click on it and Open File Location.
    4. Explorer will pop up with some shortcuts to open command prompts. Right click the x64 shortcut and select Properties.
    5. In the Shortcut tab, in the Target property, copy the path to vcvars64.bat. On my machine, after installing VS 2022 tools, the value was `C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\VC\Auxiliary\Build`.
1. Install the ARM toolchain.
    1. This is required to build a device binary. The Playdate has a different kind of processor to your computer so we use a different compiler. The ARM toolchain is installed with the Playdate SDK on Macos so no need to worry about it for that platform.
    1. https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads
    2. get arm-none-eabi. Unzip it somewhere cool.
    3. You need to add the bin folder to your PATH environment variable.

### Environment variables

Environment variables are system- or user-wide information accessible by any application. Restart any applications or terminal windows you have open if you add or change environment variables.

#### Windows

1. Press the Windows key and type "Env"
2. Select "Edit the system environment variables" or similar
3. In the dialog that opes up, click the button at the bottom labelled "Environment variables" or similar
4. Add your new variables here

#### macOS

Add your environment variables to .bash_profile in your home folder. It's a text file. Create it if it's not there.

## Building the project

Use the default build task, ctrl/cmd + shift + B. Select device or simulator. cmake build the make files, nmake or make build the libraries, and pdc builds the PDX.

The Windows simulator build creates a .dll. The mac build produces a .dylib for the simulator. On either system, building a device binary produces a .elf file. The .elf file is turned into a .bin file (legend has it this is a simple rename) by pdc when it is compiled into the pdx folder.

It is OK for your pdx folder to contain more than one, or all 3 of these files. It will mean that the same pdx can be run on both the simulator and device. Obviously you can save some file size by removing simulator binaries when shipping the software for use on the device.

## Known issues

* If no c file changed, but there are lua files in the project that changed, those changes may not be reflected in the PDX. This is because the make step does nothing, so the pdc step is not executed. The logic for this is probably in Panic's cmake files. I need to have a think about how to tackle this, but a brute force call to pdc Source (yourgamename).pdx as a post-build step would be a slightly wasteful but guranteed fix.
* The same is true if you delete the output binaries (dll, pylib, elf). They won't be rebuilt by the build process unless you do a clean first or a full rebuild, and I haven't made tasks to do those yet. If you simply delete the build folders, then this guarantees a rebuild of the binaries.
* Panic's PDC playdate compiler fails on Macos 10.15. Get version 2.0.3 and use the pdc executable from that. https://download-cdn.panic.com/playdate_sdk/
* There may be some differences between shells/command prompts/terminals. For instance, zsh uses a different profile to bash for environment variables. If things are going wrong, check that out.

## To do

* Need to build various launch tasks to debug lua and c.
* Would like to add examples of registering functions and tables with lua.
* It would be good to force a clean build each time, or provide a task to clean the build.

## Credits

Thanks to Will at Panic for helping with mac device build issues, and @joyrider3774 for assistance with vscode tasks. 
