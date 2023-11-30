# mod-synth
A self descriptive modular synth

## Set Up
1. Install MSYS2.
2. Open a MSYS2 MINGW64 terminal. (The filesystem is in C:/msys64 by default.)
3. Run `pacman -S mingw-w64-x86_64-gcc mingw-w64-x86_64-cmake` to install mingw-w64-x86_64-gcc and mingw-w64-x86_64-cmake. These are specific versions for MinGW. Running `pacman -S gcc cmake` will install generic versions of gcc and cmake onto MSYS2 MSYS.
4. Run `cmake -S . -B build` in the project directory to generate the build files inside the directory "build".
5. Run `cmake --build build` to run those build files and generate executables.

## purpose
Physical modular synths look like this:
![image](https://github.com/jseok1/mod-synth/assets/19198104/22cfc3c8-5705-4be7-85be-c80772767572)

In order to understand how these devices work, you have to have a mental understanding of how each knob and module changes the input sound.

This requirement of understanding makes it hard for beginners to get started with modular synths. 

**Our goal will be to visualize your sound as it moves through each module so anyone can understand what's happening with your synth**

Moreover working (or playing) with modular synths is a creative, iterative process. Traditionally hearing the output of your synth can be inspiration on how to tweak your synth as it's running creating a feedback loop to aid you. We believe adding a visual aspect can only enrich this feedback loop.

## potential tech stack
* c++
* [glfw](https://www.glfw.org/): window and device input
* [imgui](https://github.com/ocornut/imgui): minimal gui
* [opengl](https://www.opengl.org/): performant graphics ([cairo](https://www.cairographics.org/) too?)
* TODO: sound synthesis library (or do we do that ourselves?)

## resources
* https://gamedev.stackexchange.com/questions/59161/is-opengl-appropriate-for-2d-games

## how to add 3rd party libraries
When using cmake the main thing to understand is what you need to get your program working, the first thing is a base `CMakeLists.txt`
```cpp
cmake_minimum_required(VERSION 3.10)

project(Synth)

add_executable(Synth synth.cpp)
```
Next you want to add a 3rd party library to your project. Firstly inspect that library and see it has it's own `CMakeLists.txt`, if it does then you should add this project as a git submodule to your project which will pretty much freezes that library as a versioned package as if you were working with a `package.json` file.

When you clone down your project you'll want to bulid this library alongside of your executable on the first compile (on subsequent compiles it won't be rebuilt), to make sure that happens we add it as a subdirectory (1) (read cmake's docs on this to understand this fully).

The library you're working with with probably give you a working example of how to run their program, and at the top of such an example file you'll most likely find an `#include "library_thing.h"` for those includes to work properly you need to add the library to your include directories so your compiler will know where to find these files (2).

The header file you've included will actually need an implementation, so to provide an implementation, during the linking phase you need to link the `PortAudio` target against your executable target, the way we know to get the `PortAudio` is that we look in the 3rd parties `CMakeLists.txt` to find the name of their project, and use that (3).


```cpp
cmake_minimum_required(VERSION 3.10)

project(Synth)

add_executable(Synth synth.cpp)

#(1)
add_subdirectory(portaudio)

#(2)
include_directories(portaudio/include)

#(3)
target_link_libraries(Synth PortAudio)
```

At this point you should have a bare bones understanding of how cmake works and how to add 3rd party libraries.

