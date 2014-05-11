##Lets wrap my crash course in SDL2 up 
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

&nbsp;&nbsp;&nbsp;The first one is so any code I write with this isn't chained to SDL2. 
I could go and write a wrapper for another similar thing and use it in place of this. 
Mostly I am just paranoid here but since this is a learning experiance its okay as its showing how you can make code safe from changes in a library you use. 
The stuff in the middle is easy to understand so I don't have to say much about it. 
Though I will note that Display text is its own bullet point because of it is separate from images. 
In this whole list the only one that might cause problems is the last one as I haven't actually done that yet though I have an idea how I will. 
 
###Actually getting started 
&nbsp;&nbsp;&nbsp;I have a project already setup for making a SDL2 project in my programming folder. 
Having said that I won't be using it as I want to take us through all the steps as just like with a story the best place to start is the beggining. 
Anyway to start just open CodeBlocks and create a new project that is a Empty Project: 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/001.png "You should be able to do this even without this picture") 

&nbsp;&nbsp;&nbsp;Next name it what you will. 
I will be calling mine DragonWrapper_SDL2 because it stands out and gives me a naming convention for future wrappers. 
You will note that I am creating it at C:\Programming\ on my computer. 
I advise if your at all serious about programming on the computer your at have such a folder as it makes organization so much easier and some things are picky about placement. 
You might even want to consider breaking it down even further in that folder if you program in multiple languages by having for instance a C++ folder. 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/002.png "The bit about C:\Programming\ is useful but not a required thing") 

&nbsp;&nbsp;&nbsp;Now a bit which really isn't important. 
Basically if you can't tell what is different here I have the debug and release output set to the base directory rather then having seperate folders for them. 
I generally do this just to make placement of dll's easier on me. 
While you don't have to do this if you don't later on when I put the various things in the base folder you might have to place them elsewhere. 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/003.png "Just something I started doing so I had less folders to go through") 

&nbsp;&nbsp;&nbsp;Now we need to grab all the SDL2 bits we want for this project. 
First off is [from here](http://www.libsdl.org/download-2.0.php "This is to the SDL2 download page") get the mingw dev version of SDL2. 
Next is the mingw dev version of SDL2_image [found here](http://www.libsdl.org/projects/SDL_image/ "This is to the SDL2_image download page"). 
Finally we will want SDL2_ttf [thats here](http://www.libsdl.org/projects/SDL_ttf/ "This is to the SDL2_ttf download page") and once again get the mingw dev version. 
Now with all those files unzip them with something like [7zip](http://www.7-zip.org/ "The program I use for unzipping stuff"). 
Then do it again with what came out and you should have ended up with the following mess: 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/004.png "The numbers may vary if versions have changed. If they did I can't guarantee anything.") 

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

&nbsp;&nbsp;&nbsp;Now that we did that lets hook them up to the project. 
Right click the project and select build options. 
From there select the top level so we can affect both Debug and Release builds. 
As I am using some random things from C++11 which I am not sure of lets just check that off 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/005.png "I don't really have anything interesting to say about this")

&nbsp;&nbsp;&nbsp;Okay now lets select the Linker settings tab and add a few things to the "Other linker options" box. 
We want to put -lmingw32 -lSDL2main -lSDL2 -lSDL2_image -lSDL2_ttf -static-libgcc -static-libstdc++ in there so when we use the stuff it is available. 
The window should now look like this (I put a line break in there so you can see it all, it doesn't do anything): 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/006.png "You could even put a line break after each item but meh") 

&nbsp;&nbsp;&nbsp;Now select the Search directories tab it will be by default on the sub tab called Compiler. 
Click add and browse to wherever you stored your SDL2 stuff. 
In the include folder there is a SDL2 folder and that is what you want. 
It will ask whether you want to keep it a relative path. 
I generally go with saying no to that and you will see I did so though the choice is up to you. 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/007.png "I reopened the browse to show that as well")

&nbsp;&nbsp;&nbsp;Now lets head onto the next sub tab which is called Linker. 
Here we will be doing a similar thing but instead of include\SDL2 you just want the lib folder. 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/008.png "Same song different tune")

&nbsp;&nbsp;&nbsp;Finally (for this bit) head back on over to Compiler settings tab and change over to Debug. 
It will ask if you want to save what you have done when you do the change (I highly advise you do save your work). 
Now for a little quality of life. 
In the options enable Enable all compiler warnings and Enable extra compiler warnings. 
CodeBlocks by default has a very low level of warnings and you really want those warnings because they are a thing. 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/009.png "You might even considerer making them the default or something")

&nbsp;&nbsp;&nbsp;Now to wrap up setup as a whole lets grab the dlls we want. 
For this just head to where ever you stored all the stuff and crack open the bin. 
As I mentioned above all the dlls for SDL2 are contained here, or atleast for our needs. 
In this case our needs are as follows so just select them and copy them into the project folder. 

* SDL2.dll
* SDL2_image.dll
* SDL2_ttf.dll
* libfreetype-6.dll

  This one is for doing text
* libpng16-16.dll

  This is because I am going to use png images. 
  If you are using jpegs for instance you would want libjpeg-9.dll
* zlib.dll

###Start of Actual Code
&nbsp;&nbsp;&nbsp;Now lets get some actual code on a page. 
Well actually, lets get an actual page on the project though that is easy enough to do. 
Just add a new class file, I will be calling mine DrW_SDL2. 
Mostly because the Dr makes you think Doctor W which is cool, that and the three letters are relatively unique to help with autocomplete. 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](@010 "I don't know if this is all default so I included this image." 

&nbsp;&nbsp;&nbsp;Now you have two files. 
[name].cpp and [name].h which is fine but since I aim to have a library at the end of this so lets make one more file. 
I just called it libtest.cpp as that is exactly what it will do. 
With that though I must admit I lied about being done with setup. 
Go back to Project and select properties. 
Now select the build target tab and then select the release. 
You will note the Type is set to something like Console application. 
Change that to Dynamic library and then in the Build target files uncheck the libtest file. 
Now when you build the release you will get a .dll file. 

![While I did have a picture here it apperently failed. Inform me and I will try to fix it.](@011 "You probably where able to do this but images are fun I guess.")

&nbsp;&nbsp;&nbsp;With this I can say we are trully done with setup but there is one thing to bring up. 
Basically all of my code for this and even this post itself will be on [Github](https://github.com/ "Where I go storing the code I don't mind people seeing"). 
I use Git for source control even when I am not publishing it to Github. 
So with that said at this point is where I did the first commit at this point and you can see [the code here](https://github.com/Akhier/DragonWrapper_SDL2 "I guess you could have technically just read to here and get the code but you wont learn anything that way"). 
Also of interest as I mentioned I have my blog posts up there so you can [see them here](https://github.com/Akhier/DragonheartedCode "Also see what editing I did to a blog post before it goes up and maybe fix my past posts and submit your own pull request") and even see what is in the workings. 
So with that all out of the way time to put code on the page. 

&nbsp;&nbsp;&nbsp;Now there are many ways to start on a project but for this there are a few things I think are important to get out of the way. 
The very first of which is putting all the includes into the .h file. 
As just a quick run down of what I will start with (I might add more later but this is what I know of now). 
Also note I am just putting what goes in the angle brackets below so the full form is #include <[whats below]> 

* SDL.h
* SDL_image.h
* SDL_ttf.h
* iostream
* vector
* map

&nbsp;&nbsp;&nbsp;With that in time for some private variables and such in the header file. 
This will be somewhat forward looking as I am including some stuff before it is needed but they where easy to see. 
Anyway we want SDL_Window, a SDL_Render for it, the TTF_Font, and a vector of SDL_Texture. 
A thing to note about these is that we need to use pointers for this. 

```C++
SDL_Window* _window;
SDL_Renderer* _renderer;
SDL_Font* _font;
std::vector<SDL_Texture*> _textures;
```

&nbsp;&nbsp;&nbsp;You will note that I have a bit of a naming convention for private names. 
Mainly I start them with a underscore '_' and I use it on all private names and they tend to be all lowercase. 
This is just personal choice so do as you will but I like be able to tell at glance that something is private. 
With this let me explain the one interesting bit here which is the vector. 
The wrapper needs to be able to hold many textures to be useful and a vector is the simplest and without getting to far into it the most effeciant way for me to store them all. 
It also lets me refer to all textures by the int for where they are in the vector. 
Mind you this is only possible if you don't remove from the vector but I don't intend to. 
The other thing I considered was using a map so I could for instance use a string as the key. 
In the end though I found that a vector was the easiest way to make sure I had as much space as I needed. 

&nbsp;&nbsp;&nbsp;Now with those basics setup lets do a little more work in the header file before we move onto implementing this stuff. 
First we want a way to log an error with SDL which is simple enough. 
I actually just implemented this in the header when I tried this before but lets leave implementation in the .cpp files. 
Next up we need something that will actually return a SDL_Texture that we want to load and a similar thing for text. 
Because the first deals with actual errors from SDL and the others return an SDL2 object these will be private as well. 

```C++
void _logerror (const std::string &message);
SDL_Texture* _loadtexture (const std::string &file);
SDL_Texture* _rendertextastexture (const std::string &message, SDL_Color color);
```

&nbsp;&nbsp;&nbsp;With this all done let's head over to the .cpp file and do some work. 
First we want to initiate SDL itself so in the constructor we want to put the following:

```C++
if (SDL_Init(SDL_INIT_EVERYTHING) != 0){
   _logerror("SDL_Init");
}
if (TTF_Init() != 0){
   _logerror("TTF_Init");
}
```

&nbsp;&nbsp;&nbsp;You will note that I just init everything. 
I don't know specifically what I need so I don't really feel like holding back on this. 
You will notice of course that I am using the _logerror before I have actually shown it. 
This is partly because I already know how it will be coded but mostly because this is how it will be used. 
I don't need to know the specifics if I know this is the data it will accept. 
Anyway lets do the code for SDL error handling. 

```C++
void DrW_SDL2::_logerror(const std::string &message){
    std::cout << message << " Error: " << SDL_GetError() << std::endl;
}
```

&nbsp;&nbsp;&nbsp;And it is really that simple. 
