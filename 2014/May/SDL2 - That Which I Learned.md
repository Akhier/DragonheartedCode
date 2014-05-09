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

###Actually getting started
&nbsp;&nbsp;&nbsp;I have a project already setup for making a SDL2 project in my programming folder.
Having said that I won't be using it as I want to take us through all the steps as just like with a story the best place to start is the beggining.
Anyway to start just open CodeBlocks and create a new project that is a Empty Project:
![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](@001 "You should be able to do this even without this picture")
Next name it what you will.
I will be calling mine DragonWrapper_SDL2 because it stands out and gives me a naming convention for future wrappers.
You will note that I am creating it at C:\Programming\ on my computer.
I advise if your at all serious about programming on the computer your at have such a folder as it makes organization so much easier and some things are picky about placement.
You might even want to consider breaking it down even further in that folder if you program in multiple languages by having for instance a C++ folder.
![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](@002 "The bit about C:\Programming\ is useful but not a required thing")
