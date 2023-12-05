Setup is based on this thread: https://devforum.play.date/t/programming-with-c-on-windows-using-vscode-and-cmake/478

1. Install the Playdate SDK
    a) https://play.date/dev/
    b) set the PLAYDATE_SDK_PATH environment variable to the installation path if it has not already been set

1. Install the ARM toolchain
    a) https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads
    b) set the PLAYDATE_ARM_GCC environment var to the installation path

2. Install CMake
    a) https://cmake.org/download/
    c) Make sure cmake can be executed from a terminal/command prompt. If not, add the path to the cmake executable to your PATH environment variable.
    
3. Extensions: cmake tools (ms), c/c++ (ms)
4. Source directory must exist
5. Install Ninja in the sdk root/bin

Mac

1. Need to set PLAYDATE_ARM_GCC in .bash_profile to location of ggc-arm installed with playdate sdk
2. Set PLAYDATE_SDK_PATH too. 
3. Needed to add strip to makefile as xcode was default