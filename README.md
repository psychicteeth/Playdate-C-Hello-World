# Playdate-C-Hello-World

Goal: An empty playdate C/Lua project that can be built to the device and to the simulator in VS Code on Windows and Mac.

Status: Builds device binaries on Windows; build device binaries on Mac crashes with a segfault; simulator binaries can't be built

## Project setup

# macos

1. Install the Playdate SDK
    1. https://play.date/dev/
2. Install CMake
    1. https://cmake.org/download/
    2. Make sure cmake can be executed from a terminal/command prompt. If not, add the path to the cmake executable to your PATH environment variable.
5. (Windows only) Install Ninja
    1. https://ninja-build.org/
    2. Again make sure this is in an accessible PATH location; the Playdate SDK bin folder is a good one.
5. (Windows only) Install MSVC compiler toolset
    1. https://code.visualstudio.com/docs/cpp/config-msvc
3. Install VS Code
    1. https://code.visualstudio.com/download
    2. Extensions to install: 
        1. CMake tools (ms)
        1. CMake (twxs)
        2. C/C++ (ms)
        3. Lua (sumneko)
        4. Playdate debug (midouest)    

### Environment variables

Environment variables are system- or user-wide information accessible by any application. Restart any applications or terminal windows you have open if you add or change environment variables.

#### Windows

1. Press the Windows key and type "Env"
2. Select "Edit the system environment variables" or similar
3. In the dialog that opes up, click the button at the bottom labelled "Environment variables" or similar
4. Add your new variables here

#### Macos

Add your environment variables to .bash_profile in your home folder. It's a text file. Create it if it's not there.

## Building the project

When you open the project folder in VS Code, cmake should configure itself and offer you a dropdown of available kits - select the Playdate Device kit (more kits, for example for the simulator, are TBD).

Building should be as simple as hitting F7. I say 'should', because things often do not go to plan with building software so please let me know if there is more or different information needed in this document.

## Known issues

* The Mac build segfaults on my machine while running pdc to compile the Source elf into a PDX.
* There is only one build target at the moment - Device. You won't be able to run this build on the Simulator.
