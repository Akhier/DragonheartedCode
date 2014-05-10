###Let us wrap my crash course in SDL2 up together 
&nbsp;&nbsp;&nbsp;By which I mean to say lets go through the steps of creating a simple wrapper for SDL2. 
I will be using C++11, SDL2.0.3, SDL2_image, SDL2_ttf, and the IDE CodeBlocks with MinGW on a Windows 7 to do so. 
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

&nbsp;&nbsp;&nbsp;Now a bit which really isn't important. 
Basically if you can't tell what is different here I have the debug and release output set to the base directory rather then having seperate folders for them. 
I generally do this just to make placement of dll's easier on me. 
While you don't have to do this if you don't later on when I put the various things in the base folder you might have to place them elsewhere. 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](@003 "Just something I started doing so I had less folders to go through") 

&nbsp;&nbsp;&nbsp;Now we need to grab all the SDL2 bits we want for this project. 
First off is [from here](http://www.libsdl.org/download-2.0.php "This is to the SDL2 download page") get the mingw dev version of SDL2. 
Next is the mingw dev version of SDL2_image [found here](http://www.libsdl.org/projects/SDL_image/ "This is to the SDL2_image download page"). 
Finally we will want SDL2_ttf [thats here](http://www.libsdl.org/projects/SDL_ttf/ "This is to the SDL2_ttf download page") and once again get the mingw dev version. 
Now with all those files unzip them with something like [7zip](http://www.7-zip.org/ "The program I use for unzipping stuff"). 
Then do it again with what came out and you should have ended up with the following mess: 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](@004 "The numbers may vary if versions have changed. If they did I can't guarantee anything.") 

&nbsp;&nbsp;&nbsp;Now that we have that all there is a decision to make. 
More to the point I have already made the decision but you should know that I did. 
Basically do we want to use 32 or 64 bit versions. 
Now if you are on a 32bit computer the decision is already made for you. 
My decision was made because I even had to state that.
I have slight tendancies to want to actually destribute my code to the world at large so if I even have to consider a programmer using a 32bit computer I better go with that.

&nbsp;&nbsp;&nbsp;Now that is out of the way lets make our lives easier. 
We could leave everything where it is but lets not. 
In each of the folders is a folder called i686-w64-mingw32. 
Then in that folder is three folders (bin, include, and lib) and these are the important ones. 
Throw them all into one folder (I called mine "SDL2 32" cause it is SDL2 and 32bit). 
This will let you just link to one include and one lib folder. 
Also all the dll's you need will be in one bin folder which is nice. 
