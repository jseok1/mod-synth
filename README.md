# mod-synth
A self descriptive modular synth

## purpose
Physical modular synths look like this:
![image](https://github.com/jseok1/mod-synth/assets/19198104/22cfc3c8-5705-4be7-85be-c80772767572)

In order to understand how these devices work, you have to have a mental understanding of how each knob and module changes the input sound.

This requirement of understanding makes it hard for beginners to get started with modular synths. 

**Our goal will be to visualize your sound as it moves through each module so anyone can understand what's happening with your synth**

Moreover working (or playing) with modular synths is a creative, iterative process, traditionally hearing the output of your synth can be inspiration on how to tweak your synth as it's running creating a feedback loop to aid you. We believe adding a visual aspect can only enrich this feedback loop.

since we are building a software synth, then we are not bound by physical restrictions, so we will create a 

## potential tech stack
* c++
* [glfw](https://www.glfw.org/): window and device input
* [imgui](https://github.com/ocornut/imgui): minimal gui
* [opengl](https://www.opengl.org/): performant graphics ([cairo](https://www.cairographics.org/) too?)
* TODO: sound synthesis library (or do we do that ourselves?)

## resources
* https://gamedev.stackexchange.com/questions/59161/is-opengl-appropriate-for-2d-games
