###Let us wrap my crash course in SDL2 up together
&nbsp;&nbsp;&nbsp;By which I mean to say lets go through the steps of creating a simple wrapper for SDL2.
I will be using C++11, SDL2.0.3, SDL2_image, SDL2_ttf, and the IDE CodeBlocks to do so.
There are a couple important bits so lets document them here and now so we don't end up over complicating things later.
* Most important is that Nothing public should take nor return anything specifically SDL
* Display a window (just a window, later I can add the support for multiple windows but we don't need that now)
* Display the window without borders
* Display an image
* Handle the break down of said image into tiles (basically make tilesets work)
* Display text
* Change the font and size of displayed text
* Handle input for mouse and keyboard
The first one is so any code I write with this isn't chained to SDL2.
I could go and write a wrapper for another similar thing and use it in place of this.
Mostly I am just paranoid here but since this is a learning experiance its okay as its showing how you can make code safe from changes in a library you use.
The stuff in the middle is easy to understand so I don't have to say much about it.
Though I will note that Display text is its own bullet point because of it is separate from images.
In this whole list the only one that might cause problems is the last one as I haven't actually done that yet though I have an idea how I will.