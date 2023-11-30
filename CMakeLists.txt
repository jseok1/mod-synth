cmake_minimum_required(VERSION 3.10)

project(Synth VERSION 0.1.0 LANGUAGES C CXX)

add_executable(Synth main.cpp)

include_directories(lib/portaudio/include)

add_subdirectory(lib/portaudio)

target_link_libraries(Synth PortAudio)
