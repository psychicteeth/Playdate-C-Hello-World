# Playdate-C-Hello-World

Goal: An empty playdate C/Lua project that can be built to the device and to the simulator in VS Code on Windows and Mac.

Status: Builds simulator binaries on Windows and Mac in the sdefault build task.

## Project setup

### macOS

1. Install the Playdate SDK
    1. https://play.date/dev/
    2. Set the environment variable PLAYDATE_SDK_PATH to the path where you install the SDK.
    3. Set PLAYDATE_ARM_GCC to the location of the arm GCC toolchain installed with the SDK.
2. Install CMake
    1. https://cmake.org/download/ or use homebrew https://brew.sh/
    2. Make sure cmake can be executed from a terminal/command prompt. If not, add the path to the cmake executable to your PATH environment variable.
3. Install VS Code
    1. https://code.visualstudio.com/download
    2. Extensions to install: 
        1. C/C++ (ms)
        3. Lua (sumneko)
        4. Playdate debug (midouest)    
        5. You do NOT need to install the cmake tools / cmake extensions for this repository. In fact, they may interfere with it.

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
        5. You do NOT need to install the cmake tools / cmake extensions for this repository. In fact, they may interfere with it.
1. We need nmake. If you do not have a version of Visual Studio (not Code) installed, you will need to install the MSVC compiler toolset:
    1. https://code.visualstudio.com/docs/cpp/config-msvc
2. Set the VISUAL_STUDIO_TOOLS environment variable to the path to vcvars64.bat. One way to find this is detailed below:
    1. You can find the location of it by going to the start menu, typing "x64 Native" and seeing what comes up.
    2. Right click on it and Open File Location.
    4. Explorer will pop up with some shortcuts to open command prompts. Right click the x64 shortcut and select Properties.
    5. In the Shortcut tab, in the Target property, copy the path to vcvars64.bat. On my machine, after installing VS 2022 tools, the value was `C:\Program Files (x86)\Microsoft Visual Studio\2022\BuildTools\VC\Auxiliary\Build`.

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

Use the default build task, ctrl/cmd + shift + B. cmake build the make files, nmake or make build the libraries, and pdc builds the PDX.

## Known issues

* Nobody's tested this but me, to my knowledge.
* You can only build for the simulator as yet.
* I haven't tested lua yet.
* I haven't worked out attaching a C debugger yet.
* macOS build process leaves a lot of intermediate files lying around in the project root.
