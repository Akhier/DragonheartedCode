##Lets wrap my crash course in SDL2 up 
&nbsp;&nbsp;&nbsp;By which I mean to say lets go through the steps of creating a simple wrapper for SDL2. 
I will be using C++11, SDL2, SDL2_image, SDL2_ttf, and the IDE CodeBlocks with MinGW on a Windows 7 to do so. 
There are a couple important features I want so lets document them here so we don't end up over complicating things later. 

* Most important is that Nothing public should take nor return anything specifically SDL 
* Display a window 
* Display an image 
* Handle the break down of said image into tiles (basically make tilesets work) 
* Display text 
* Change the font and size of displayed text 

&nbsp;&nbsp;&nbsp;The first one is so any code I write with this isn't chained to SDL2. 
I could go and write a wrapper for another similar thing and use it in place of this. 
Mostly I am just paranoid here but since it is a learning experience its okay. 
this will show how you can make code safe from changes in an external library you use. 
The rest are easy to understand so I don't have to say much about them. 
Though I will note that Display text is its own bullet point because of it is separate from images. 
 
###Actually getting started 
&nbsp;&nbsp;&nbsp;I already have something setup for making SDL2 projects in my programming folder. 
Having said that I won't be using it as I want to take us through all the steps as with a story the best place to start is the beginning. 
Anyway to get started just open CodeBlocks and create a new project that is an "Empty Project": 

![While I did have a picture here it apparently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/001.png "You should be able to do this even without this picture") 

&nbsp;&nbsp;&nbsp;Next name it what you will. 
I will be calling mine DragonWrapper_SDL2 because it stands out and gives me a naming convention for future wrappers. 
You will note that I am creating it at C:\Programming\ on my computer. 
Having such a folder makes organization much easier and helps with those things that are picky about placement. 
You might even want to consider breaking it down even further if you program in multiple languages by having sub folders for each. 

![While I did have a picture here it apparently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/002.png "The bit about C:\Programming\ is useful but not a required thing") 

&nbsp;&nbsp;&nbsp;Now for a bit which really isn't important but more of a personal preference for me. 
Basically if you can't tell what is different here I have the debug and release output set to the base directory rather then having separate folders for them. 
I generally do this just to make placement of dll's easier on me. 
While you don't have to do this if you don't then later on when I put the various things in the base folder you might have to place them elsewhere. 

![While I did have a picture here it apparently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/003.png "Just something I started doing so I had less folders to go through") 

&nbsp;&nbsp;&nbsp;Now we need to grab all the SDL2 bits we want for this project. 
First off is [from here](http://www.libsdl.org/download-2.0.php "This is to the SDL2 download page") get the mingw dev version of SDL2. 
Next is the mingw dev version of SDL2_image [found here](http://www.libsdl.org/projects/SDL_image/ "This is to the SDL2_image download page"). 
Finally we will want SDL2_ttf [that is here](http://www.libsdl.org/projects/SDL_ttf/ "This is to the SDL2_ttf download page") and once again get the mingw dev version. 
Now with all those files unzip them with something like [7zip](http://www.7-zip.org/ "The program I use for unzipping stuff"). 
Then unzip what came out once more and you should have ended up with the following stuff: 

![While I did have a picture here it apparently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/004.png "The numbers may vary if versions have changed. If they did I can't guarantee anything.") 

&nbsp;&nbsp;&nbsp;Now that we have that all done there is a decision to make. 
More to the point I have already made the decision but you should know that I did. 
Basically do we want to use the 32 bit or 64 bit versions. 
Now if you are on a 32bit computer the decision is already made for you. 
My decision was made because I even had to state that.
I have slight tendencies to want to actually distribute my programs to the world at large so if I even have to consider about a programmer using a 32bit computer I better go with that.

&nbsp;&nbsp;&nbsp;Now that is out of the way let's make our lives easier. 
We could leave everything where it is but let's not. 
In each of the folders is another folder called i686-w64-mingw32. 
Then in that folder is bin, include, and lib which are the important ones for us. 
Throw them all into one folder (I called mine "SDL2 32" because it is SDL2 and 32bit). 
This will let us link to just one place when it comes time for that. 
Also all the dll's you will need are in one bin folder which is convenient. 

&nbsp;&nbsp;&nbsp;Now that we did that let's hook them up to our project. 
Right click on the project and select build options. 
From there select the top level so we can affect both Debug and Release builds. 
As I am using some random things from C++11 let's just check that off right away. 

![While I did have a picture here it apparently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/005.png "I don't really have anything interesting to say about this")

&nbsp;&nbsp;&nbsp;Okay now let's select the Linker settings tab and add a few things to the "Other linker options" box. 
We want to put -lmingw32 -lSDL2main -lSDL2 -lSDL2_image -lSDL2_ttf -static-libgcc -static-libstdc++ in there so when we use the stuff it will be available right away. 
The window should now look like this (I put line breaks in there so you can see it all, it doesn't do anything): 

![While I did have a picture here it apparently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/006.png "You could even put a line break after each item but meh") 

&nbsp;&nbsp;&nbsp;Now select the Search directories tab and then the sub tab called Compiler. 
Click add and then browse to wherever you stored your SDL2 stuff. 
In there select the include folder and inside it is a folder called SDL2 which is what we want so select it and click ok. 
It will then ask whether you want to keep it a relative path. 
I generally go with saying no and you will see I did so though the choice is up to you as each case has its own reasons for choosing it. 

![While I did have a picture here it apparently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/007.png "I reopened the browse to show that as well")

&nbsp;&nbsp;&nbsp;Now let's head onto the next sub tab which is called Linker. 
Here we will be doing a similar thing but instead of the include\SDL2 folder you just want the lib folder. 

![While I did have a picture here it apparently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/008.png "Same song different tune")

&nbsp;&nbsp;&nbsp;Finally (for this bit) head back over to the Compiler settings tab and change over to Debug. 
It will ask if you want to save what you have done when you do the change and just say yes. 
Now we change something for a little quality of life. 
In the options enable "Enable all compiler warnings" and "Enable extra compiler warnings". 
CodeBlocks by default uses a low level of warnings and you really want more of them then the default because they can help later on. 

![While I did have a picture here it apparently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/Blog%20Images/SDL2%20-%20That%20Which%20I%20Learned/009.png "You might even consider making them the default or something")

&nbsp;&nbsp;&nbsp;Now to finish the basic setup so let's grab the dlls we want. 
For this just head to where ever you stored all the stuff and crack open the bin folder. 
As I mentioned above all the dlls for SDL2 are contained here, or at least for our needs. 
In this case what we need is as follows, so just select them and copy them into the project folder. 

* SDL2.dll
* SDL2_image.dll
* SDL2_ttf.dll
* libfreetype-6.dll

  This one is for doing text
* libpng16-16.dll

  we need this because I am going to use png images. 
  If you are using jpegs for instance you would want libjpeg-9.dll
* zlib.dll

###Start of Actual Code
&nbsp;&nbsp;&nbsp;Now let's get some actual code on a page. 
Well actually, let's get an actual page on the project. 
To start just add a new class file, I will be calling mine DrW_SDL2. 
Mostly because the Dr makes you think Doctor W which is cool, that and the three letters are relatively unique to help with auto-complete. 

![While I did have a picture here it apparently failed. Inform me and I will try to fix it.](@010 "I don't know if this is all default so I included this image." 

&nbsp;&nbsp;&nbsp;Now we have two files. 
[name].cpp and [name].h which is fine but since I aim to have a library at the end of this we should add one more file to test with. 
I just called it libtest.cpp as that is exactly what it will do. 
With that though I must admit I lied about being done with setup. 
Go back to Project and select properties. 
Now select the build target tab and then select the release. 
You will note the Type is set to something like Console application. 
Change that to Dynamic library and then in the Build target files uncheck the libtest file. 
Now when you build the release you will get a .dll file. 

![While I did have a picture here it apparently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/011.png "You probably were able to do this but images are fun I guess.")

&nbsp;&nbsp;&nbsp;With this I can say we are truly done with setup but there is one thing to bring up. 
Basically all of my code for this and even this post itself will be on [Github](https://github.com/ "Where I go storing the code I don't mind people seeing"). 
I use Git for source control even when I am not publishing it to Github. 
So with that said it was at this point where I did the first commit on the project. 
You can see [the code here](https://github.com/Akhier/DragonWrapper_SDL2 "I guess you could have technically just read to here and get the code but you wont learn anything that way"). 
Also of interest, as I mentioned, I have my blog posts up on my Github so you can [see my posts here](https://github.com/Akhier/DragonheartedCode "Also see what editing I did to a blog post before it goes up and maybe fix my past posts and submit your own pull request") and even see what is in the workings. 
So with that all out of the way time to put code on the page. 

&nbsp;&nbsp;&nbsp;Now there are many ways to start on a project but for this there are a few things I think are important to get out of the way. 
The very first of which is putting all the includes into the .h file. 
Below is just a quick run down of what I will start with (I might add more later but this is what I know of now). 
Also note I am just putting what goes in the angle brackets below so the full form is #include <[whats below]> 

* SDL.h
* SDL_image.h
* SDL_ttf.h
* iostream
* vector
* map

&nbsp;&nbsp;&nbsp;With that it is time for some private variables. 
This will be somewhat forward looking as I am including some stuff before it is needed but they where easy to see coming. 
Anyway we want an SDL_Window, an SDL_Render for it, the TTF_Font, and a vector of SDL_Texture. 

```C++
SDL_Window* _window;
SDL_Renderer* _renderer;
SDL_Font* _font = NULL;
std::vector<SDL_Texture*> _textures;
```

&nbsp;&nbsp;&nbsp;You will note that I have a bit of a naming convention for private names. 
Mainly I start them with an underscore '_' and I use it on all private names. 
They also tend to all be lowercase. 
This is just personal choice for me so do as you will but I like be able to tell at glance that something is private. 
With this let me explain the one slightly different bit here which is the vector. 
The wrapper needs to be able to hold many textures to be useful and a vector was the simplest and quickest way for me to store them all. 
It also lets me refer to all textures by the int for where they are in the vector. 
Mind you this is only possible if you don't remove from the vector but I don't intend to. 
The other thing I considered was using a map so I could for instance use a string as the key. 
In the end though I found that a vector was the easiest way to make sure I had as much space as I needed without over-complicating it. 

&nbsp;&nbsp;&nbsp;Now with that done let's do a little more work in the header file before we move onto implementing it all. 
First we want a way to log an error with SDL which is simple enough. 
I actually just implemented this in the header when I tried this before but let's leave implementation of things in the .cpp files. 
After that we need something that will actually return a SDL_Texture that we want to load and a similar thing for text. 
Because the first deals with actual errors from SDL and the others return an SDL2 object these will be private as well. 

```C++
void _logerror (const std::string &message);
SDL_Texture* _loadtexture (const std::string &file);
SDL_Texture* _rendertextastexture (const std::string &message, SDL_Color color);
```

&nbsp;&nbsp;&nbsp;Now let's head over to the .cpp file and get some of this stuff working. 
We want to first initiate SDL itself so in the constructor we want to put the following:

```C++
DrW_SDL2::DrW_SDL2()
{
    if (SDL_Init(SDL_INIT_EVERYTHING) != 0){
       _logerror("SDL_Init");
    }
    if (TTF_Init() != 0){
       _logerror("TTF_Init");
    }
}
```

&nbsp;&nbsp;&nbsp;You will note that I just init everything. 
I don't know specifically what I need so I don't really feel like holding back on this. 
You will also notice of course that I am using the _logerror before I have actually shown it. 
This is partly because I already know how it will be coded, but mostly because this is how it will be used. 
I don't need to know the specifics if I know this is the data it will accept. 
Anyway let's do the actual code for SDL error handling. 

```C++
void DrW_SDL2::_logerror(const std::string &message){
    std::cout << message << " Error: " << SDL_GetError() << std::endl;
}
```

&nbsp;&nbsp;&nbsp;And it is really that simple. 
Next we can do texture loading. 
I will include loading text as a texture here as well. 
Rendering text as a texture is a bit more complex but that is fine.

```C++
SDL_Texture* DrW_SDL2::_loadtexture(const std::string &file){
    SDL_Texture* outputTexture = IMG_LoadTexture(_renderer, file.c_str());
    if (outputTexture == nullptr){
        _logerror("IMG_LoadTexture");
    }
    return outputTexture;
}

SDL_Texture* DrW_SDL2::_rendertextastexture(const std::string &message, SDL_Color color){
    if (_font == nullptr){
        return nullptr;
    }
    SDL_Surface* tempSurface = TTF_RenderText_Blended(_font, message.c_str(), color);
    if (tempSurface == nullptr){
        _logerror("TTF_RenderText_Blended");
        return nullptr;
    }
    SDL_Texture* outputTexture = SDL_CreateTextureFromSurface(_renderer, tempSurface);
    if (outputTexture == nullptr){
        _logerror("SDL_CreateTextureFromSurface");
    }
    SDL_FreeSurface(tempSurface);
    return outputTexture;
}
```

&nbsp;&nbsp;&nbsp;I will note at this point that I am not really handling the errors so much as just noting when they happen. 
Later I might come back and replace cout with writing the errors to a text file. 
As it is I would not really call it complete but it is good enough for this. 
Also of note is that for the text I am using Blended mode. 
That would be the fancy way of rendering text and depending on how it performs I may add in the ability to choose Shaded or even Solid as needed. 
Anyway we have finished all the private functions we need at the moment. 
Now I know I have been doing a lot of setup here with this code but that is because I know what I want it to do. 
If you where to start from scratch this would probably be a little more haphazard. 
With this out of the way though I will be stepping into more fluid territory. 
The first step in this is simple enough though, let's write something to create a window. 

```C++
void createWindow(const std::string &windowtitle, int x, int y, int width, int height, bool resizable);
```

&nbsp;&nbsp;&nbsp;This could be enough but I want to add one thing. 
While it is nice to specify exactly the x and y of your window but sometimes you just want it to open wherever. 
We will now add another createWindow which doesn't have the x and y arguments. 

```C+
void createWindow(const std::string &windowtitle, int width, int height, bool resizable);
```

&nbsp;&nbsp;&nbsp;With that let's write the actual code but first I will be explaining something slightly tricky I plan to use. 
Seeing as it is something a little beyond the basics I will explain it first. 
I am going to use an "inline if" in the code. 
What happens is exactly the same as a normal if but as noted inline. 
The way it works is [argument]?[true]:[false] so you could say x = (a > b)?y:z. 
If 'a' is greater than 'b' then 'x' is equal to 'y' else it is equal to 'z'. 
Anyway here is the code for creating a window. 

```C++
void DrW_SDL2::createWindow(const std::string windowtitle, int x, int y, int width, int height, bool resizable){
    _window = SDL_CreateWindow(windowtitle.c_str(), x >= 0 ? x : SDL_WINDOWPOS_UNDEFINED, y >= 0 ? y : SDL_WINDOWPOS_UNDEFINED, width, height, resizable ? SDL_WINDOW_RESIZABLE : (SDL_WINDOW_SHOWN | SDL_WINDOW_RESIZABLE));
    if (_window == nullptr){
        _logerror("SDL_CreateWindow");
    }
    _renderer = SDL_CreateRenderer(_window, -1, SDL_RENDERER_ACCELERATED | SDL_RENDERER_PRESENTVSYNC);
    if (_renderer == nullptr){
        _logerror("SDL_CreateRenderer");
    }
}

void DrW_SDL2::createWindow(const std::string windowtitle, int width, int height, bool resizable){
    createWindow(windowtitle, -1, -1, width, height, resizable);
}
```

&nbsp;&nbsp;&nbsp;You will note I used the inline if three times and to be honest I didn't need to. 
It is mostly just my own aesthetics when it comes to coding. 
I could have created ```int X = x;``` and then wrote ```if(x < 0) {X = SDL_WINDOWPOS_UNDEFINED;}``` and do the same for y and the flags. 
Anyway you will have noticed that I also set the renderer here and applied some flags to it as well. 
The renderer is set here because it is basically attached to the window and I don't plan to do anything fancy with it. 
If you wanted to do something more with your renderer you may want to separate that out. 
As for the flags the accelerated one is basically just telling it to use hardware acceleration. 
The present vsync flag means that the render limits itself to your monitors refresh rate so you don't end up with insanely high but unneeded fps. 

&nbsp;&nbsp;&nbsp;With this we have reached an important point. 
Basically we can finally test that this whole mess is working though we probably want to added a couple things first. 
So let's add the following to the deconstructor: 

```C++
DrW_SDL2::~DrW_SDL2(){
    for (size_t iter = 0; iter < _textures.size(); ++iter){
        SDL_DestroyTexture(_textures[iter]);
    }
    if (_font != NULL){
        TTF_CloseFont(_font);
    }
    SDL_DestroyRenderer(_renderer);
    SDL_DestroyWindow(_window);
    IMG_Quit();
    TTF_Quit();
    SDL_Quit();
}

```

&nbsp;&nbsp;&nbsp;Those lines will take care of getting rid of what we will be making in this next step. 
Which of course means we will be doing something with the libtest file. 
I will be using an SDL command in the test at this time as there isn't a need for it in the wrapper yet. 

```C++
#include "drw_sdl2.h"

const int SCREEN_WIDTH = 640, SCREEN_HEIGHT = 480;

int main(int argc, char **argv){
    DrW_SDL2 sdl;
    sdl.createWindow("test window", SCREEN_WIDTH, SCREEN_HEIGHT, true);
    SDL_Delay(2000);
    return 0;
}
``` 

&nbsp;&nbsp;&nbsp;With that in, running the project should open up a blank window for a couple seconds and there should be a couple warnings in the build messages. 
The warnings are about argc and argv not being used. 
They from what I can tell don't matter and are in because SDL requires them for compatibility reasons. 
As for it staying up for those couple seconds this is because of the SDL_Delay command. 
It accepts an int representing the number of milliseconds to delay. 
Of course this causes the window to be unresponsive but its just for testing at this point so that is okay. 
Now to actually load a texture. 

```C++
int DrW_SDL2::createText(const std::string &message){
    SDL_Color color = {0, 0, 0, 255};
    _textures.push_back(_rendertextastexture(message, color));
    return _textures.size() - 1;
}

int DrW_SDL2::createTexture(const std::string &file){
    _textures.push_back(_loadtexture(file));
    return _textures.size() - 1;
}
```

&nbsp;&nbsp;&nbsp;They both return an int which is the location the texture is at. 
This means that on the libtest side of things you just keep track of textures by an int which is simple and straightforward. 
With the createText code I am just having black as the color of the text. 
I will probably at a later date add the ability to change the color, mostly likely with an enum for various colors. 
Anyway with this we are halfway to the goal of displaying an image. 

&nbsp;&nbsp;&nbsp;We do have a bit of a thing now to decide. 
Rendering a texture has a few options and half require the use of SDL_Rect. 
When I did some work while learning SDL I just used  and int array to represent this but I want a better option. 
From what I can tell there are about 4 of ways to do this. 
Just use the int array as it is simple and works, Make my own struct Rect, use a function that hides the use of SDL_Rect, and finally make a class Rect. 
Because of some stuff I looked into we will be using the last option. 
But let's write the class and then I will explain what I did. 
Do note I will be putting the class in its own files named drw_sdl2_rect while the class itself is just called Rect. 

drw_sdl2_rect.h
```C++
#include <SDL.h>

class Rect{
    public:
        Rect(int x, int y, int w, int h);
        Rect(int x, int y);
        int X, Y, W, H;
    private:
        SDL_Rect _getsdlrect();
    friend class DrW_SDL2;
};
```

drw_sdl2_rect.cpp
```C++
Rect::Rect(int x, int y, int w, int h){
    X = x;
    Y = y;
    W = w;
    H = h;
}

Rect::Rect(int x, int y){
    X = x;
    Y = y;
    W = -1;
    H = -1;
}

SDL_Rect* Rect::_getsdlrect(){
    SDL_Rect* output = new SDL_Rect;
    output->x = X;
    output->y = Y;
    output->w = W;
    output->h = H;
    return output;
}
```

&nbsp;&nbsp;&nbsp;With this we can continue but first let's look at what I did with the Rect class. 
In the constructor that only takes x and y I set the width and height to -1. 
This will tell me I need to set those later on and if I forget definitely throw an error. 
If I used a 0 or some other way to show it wasn't set I might end up not setting them somewhere and wondering why the texture isn't rendering. 
The big thing is that I declare my base class DrW_SDL2 as a friend. 
This means that even though it is private the wrapper class will be able to use the function. 
Now this doesn't seem much but it does means I get to use this class as SDL_Rect without exposing it outside the wrapper. 

&nbsp;&nbsp;&nbsp;Now that we have the Rect squared away we need to write the functions that will actually render the textures. 
When I learned this I had a bunch of replication in these functions as there are 4 options for rendering textures and they are quite similar. 
I have since figured a better way of doing it so I can reduce the unneeded duplication of code. 
It will start with a private function. 

```C++
void DrW_SDL2::_rendertexture(const int textureid, const SDL_Rect* source, const SDL_Rect* destination){
    SDL_RenderCopy(_renderer, _textures[textureid], source, destination);
}
```

&nbsp;&nbsp;&nbsp;And now for four more public functions and one private helper. 
The four can be public as they won't be accepting SDL_Rect but rather our own Rect class. 

```C++
Rect DrW_SDL2::_gettexturesize(const int textureid, int x, int y){
    Rect output(x, y);
    SDL_QueryTexture(_textures[textureid], NULL, NULL, &output.W, &output.H);
    return output;
}

void DrW_SDL2::renderTexture(const int textureid, Rect destination){
    _rendertexture(textureid, NULL, destination._getsdlrect());
}

void DrW_SDL2::renderTexture(const int textureid, int x, int y){
    renderTexture(textureid, _gettexturesize(textureid, x, y));
}

void DrW_SDL2::renderTexture(const int textureid, Rect source, Rect destination){
    _rendertexture(textureid, source._getsdlrect(), destination._getsdlrect());
}

void DrW_SDL2::renderTexture(const int textureid, Rect source, int x, int y){
    renderTexture(textureid, source, _gettexturesize(textureid, x, y));
}
```

&nbsp;&nbsp;&nbsp;I definitely prefer this to how my original try at it worked out. 
Even only counting the internal bits and not including any bracket only lines I used 34 lines of code previously. 
Here even with 2 extra functions and counting all lines the total comes out to only 20. 
While shorter is not always better in this case it definitely is. 
A couple more functions are needed before we can render a texture but these are basically just the thinnest of wrappings.

```C++
void DrW_SDL2::renderclear(){
    SDL_RenderClear(_renderer);
}

void DrW_SDL2::renderpresent(){
    SDL_RenderPresent(_renderer);
}
```

&nbsp;&nbsp;&nbsp;Very straightforward with these as they just letting us access the clear and render functions without actually touching SDL. 
Anyway to test this we need an image and I have prepared one for us. 
I have made a wonderful 64x22 png in the colors of Dwarf Fortress microline and a wonderful eye burn magenta. 

![While I did have a picture here it apparently failed. Inform me and I will try to fix it.](http://i607.photobucket.com/albums/tt156/akhierthedragonhearted/TestTexture.png "Truly a lovely image") 

&nbsp;&nbsp;&nbsp;With this let's render it to the screen. 
I placed the image in the base folder for the project and we just need to add the following lines right before SDL_Delay in libtest.cpp

```C++
int test = sdl.createTexture("TestTexture.png");
sdl.renderclear();
sdl.renderTexture(test, 10, 10);
sdl.renderpresent();
```

&nbsp;&nbsp;&nbsp;With that the screen should pop up as all black but with our little image at 10,10 on the screen. 
But of course you could probably tell by the test image it is setup so we can use it as a mini tileset. 
So let's add that functionality in now. 
First to add a private Map with int as the key and a Vector of Rect. 
Next we will also want a couple public functions. 

```C++
std::map<int, std::vector<Rect>> _tilesetdefinition;
```

```C++
int DrW_SDL2::setupTileset(const int textureid, Rect source){
    _tilesetdefinition[textureid].push_back(source);
    return _tilesetdefinition[textureid].size() - 1;
}

Rect DrW_SDL2::getSourceRect (const int textureid, const int tileid){
    return _tilesetdefinition[textureid][tileid];
}
```

&nbsp;&nbsp;&nbsp;This setup can only set one tile of a tileset at a time but any automation should really be elsewhere. 
Basically I would be wanting to import the tile info from a file or something similar. 
Anyway let's break the picture up and paste it all over the place in our libtest. 
Because of needing to replace some lines I will be replacing everything between int test and sdl.renderpresent() 

```C++
int solidPink = sdl.setupTileset(test, Rect(1, 1, 20, 20));
int halfandhalf = sdl.setupTileset(test, Rect(22, 1, 20, 20));
int solidBlue = sdl.setupTileset(test, Rect(43, 1, 20, 20));
sdl.renderclear();
sdl.renderTexture(test, sdl.getSourceRect(test, solidPink), Rect(20, 20, 20, 20));
sdl.renderTexture(test, sdl.getSourceRect(test, solidBlue), Rect(40, 40, 20, 20));
sdl.renderTexture(test, sdl.getSourceRect(test, halfandhalf), Rect(40, 20, 20, 20));
sdl.renderTexture(test, sdl.getSourceRect(test, halfandhalf), Rect(20, 40, 20, 20));
```

&nbsp;&nbsp;&nbsp;These lines will make something that looks very much like the middle image of the png appear. 
Of course it is actually a pink square, a blue square, and a couple half and half squares. 
Seeing as that works we should probably get it so we can print text on the screen. 
First we need to be able to set the font. 

```C++
void DrW_SDL2::setFont(const std::string &font, int fontsize){
    _font = TTF_OpenFont(font.c_str(), fontsize);
}
```

&nbsp;&nbsp;&nbsp;And that is it basically. 
Because of a lot of the setup that was previously done we can just plug in some stuff and have it work. 
Sadly I can't just have it work because we don't have an actual font to use yet. 
Luckily for us everyone tends to have some ttf files lying around but just in case [here are some free fonts](http://ftp.gnu.org/gnu/freefont/ "gnu some of you would need this"). 
I just grabbed Mono, Sans, and Serif from there and threw them in a fonts folder. 
Now we can toss the following code just above the renderpresent and get it running.

```C++
sdl.setFont("fonts/freeserif.ttf", 16);
int text = sdl.createText("test");
sdl.renderTexture(text, 20, 20);

```
&nbsp;&nbsp;&nbsp;Now when you run it there will be the word test in your square. 
Of course with this done we have finished with implementing what I outlined way at the top. 
There are a lot of stuff that could still be done but that is for later. 
You can now take the code and switch it the build target to release and get a dll which you can use or even just take the files and use them as is. 
At the very bottom I have the final code as done in this post as I will definitely be adding to the wrapper in the future as I need to. 
This is the barest boned structure and if you can follow it up to here and want to use it I advise you not wait for me to do so. 
The best way to learn this stuff is by doing and I might not need the features you want. 
Also if there is any errors in the code or I did something that while technically correct isn't proper please tell me. 
It is much better for me to be told I am wrong so I can fix it rather having it stay wrong and misinform people with this post. 

drw_sdl2.h
```C++
#ifndef DRW_SDL2_H
#define DRW_SDL2_H

#include <SDL.h>
#include <SDL_image.h>
#include <SDL_ttf.h>
#include <iostream>
#include <map>
#include <vector>
#include "drw_sdl2_rect.h"

class DrW_SDL2
{
    public:
        DrW_SDL2();
        void createWindow(const std::string windowtitle, int x, int y, int width, int height, bool resizable);
        void createWindow(const std::string windowtitle, int width, int height, bool resizable);
        int createText(const std::string &message);
        int createTexture(const std::string &file);
        void renderTexture(const int textureid, Rect destination);
        void renderTexture(const int textureid, int x, int y);
        void renderTexture(const int textureid, Rect source, Rect destination);
        void renderTexture(const int textureid, Rect source, int x, int y);
        void renderclear();
        void renderpresent();
        int setupTileset(const int textureid, Rect source);
        Rect getSourceRect (const int textureid, const int tileid);
        void setFont(const std::string &font, int fontsize);
        virtual ~DrW_SDL2();
    private:
        SDL_Window* _window;
        SDL_Renderer* _renderer;
        TTF_Font* _font = NULL;
        std::vector<SDL_Texture*> _textures;
        void _logerror (const std::string &message);
        SDL_Texture* _loadtexture (const std::string &file);
        SDL_Texture* _rendertextastexture (const std::string &message, SDL_Color color);
        void _rendertexture(const int textureid, const SDL_Rect* source, const SDL_Rect* destination);
        Rect _gettexturesize(const int textureid, int x, int y);
        std::map<int, std::vector<Rect>> _tilesetdefinition;
};

#endif // DRW_SDL2_H
```

drw_sdl2.cpp
```C++
#include "drw_sdl2.h"

DrW_SDL2::DrW_SDL2(){
    if (SDL_Init(SDL_INIT_EVERYTHING) != 0){
       _logerror("SDL_Init");
    }
    if (TTF_Init() != 0){
       _logerror("TTF_Init");
    }
}

void DrW_SDL2::_logerror(const std::string &message){
    std::cout << message << " Error: " << SDL_GetError() << std::endl;
}

SDL_Texture* DrW_SDL2::_loadtexture(const std::string &file){
    SDL_Texture* outputTexture = IMG_LoadTexture(_renderer, file.c_str());
    if (outputTexture == nullptr){
        _logerror("IMG_LoadTexture");
    }
    return outputTexture;
}

SDL_Texture* DrW_SDL2::_rendertextastexture(const std::string &message, SDL_Color color){
    if (_font == nullptr){
        return nullptr;
    }
    SDL_Surface* tempSurface = TTF_RenderText_Blended(_font, message.c_str(), color);
    if (tempSurface == nullptr){
        _logerror("TTF_RenderText_Blended");
        return nullptr;
    }
    SDL_Texture* outputTexture = SDL_CreateTextureFromSurface(_renderer, tempSurface);
    if (outputTexture == nullptr){
        _logerror("SDL_CreateTextureFromSurface");
    }
    SDL_FreeSurface(tempSurface);
    return outputTexture;
}

void DrW_SDL2::createWindow(const std::string windowtitle, int x, int y, int width, int height, bool resizable){
    _window = SDL_CreateWindow(windowtitle.c_str(), x >= 0 ? x : SDL_WINDOWPOS_UNDEFINED, y >= 0 ? y : SDL_WINDOWPOS_UNDEFINED, width, height, resizable ? SDL_WINDOW_RESIZABLE : (SDL_WINDOW_SHOWN | SDL_WINDOW_RESIZABLE));
    if (_window == nullptr){
        _logerror("SDL_CreateWindow");
    }
    _renderer = SDL_CreateRenderer(_window, -1, SDL_RENDERER_ACCELERATED | SDL_RENDERER_PRESENTVSYNC);
    if (_renderer == nullptr){
        _logerror("SDL_CreateRenderer");
    }
}

void DrW_SDL2::createWindow(const std::string windowtitle, int width, int height, bool resizable){
    createWindow(windowtitle, -1, -1, width, height, resizable);
}

int DrW_SDL2::createText(const std::string &message){
    SDL_Color color = {0, 0, 0, 255};
    _textures.push_back(_rendertextastexture(message, color));
    return _textures.size() - 1;
}

int DrW_SDL2::createTexture(const std::string &file){
    _textures.push_back(_loadtexture(file));
    return _textures.size() - 1;
}

void DrW_SDL2::_rendertexture(const int textureid, const SDL_Rect* source, const SDL_Rect* destination){
    SDL_RenderCopy(_renderer, _textures[textureid], source, destination);
}

Rect DrW_SDL2::_gettexturesize(const int textureid, int x, int y){
    Rect output(x, y);
    SDL_QueryTexture(_textures[textureid], NULL, NULL, &output.W, &output.H);
    return output;
}

void DrW_SDL2::renderTexture(const int textureid, Rect destination){
    _rendertexture(textureid, NULL, destination._getsdlrect());
}

void DrW_SDL2::renderTexture(const int textureid, int x, int y){
    renderTexture(textureid, _gettexturesize(textureid, x, y));
}

void DrW_SDL2::renderTexture(const int textureid, Rect source, Rect destination){
    _rendertexture(textureid, source._getsdlrect(), destination._getsdlrect());
}

void DrW_SDL2::renderTexture(const int textureid, Rect source, int x, int y){
    renderTexture(textureid, source, _gettexturesize(textureid, x, y));
}

void DrW_SDL2::renderclear(){
    SDL_RenderClear(_renderer);
}

void DrW_SDL2::renderpresent(){
    SDL_RenderPresent(_renderer);
}

int DrW_SDL2::setupTileset(const int textureid, Rect source){
    _tilesetdefinition[textureid].push_back(source);
    return _tilesetdefinition[textureid].size() - 1;
}

Rect DrW_SDL2::getSourceRect (const int textureid, const int tileid){
    return _tilesetdefinition[textureid][tileid];
}

void DrW_SDL2::setFont(const std::string &font, int fontsize){
    _font = TTF_OpenFont(font.c_str(), fontsize);
}

DrW_SDL2::~DrW_SDL2(){
    for (size_t iter = 0; iter < _textures.size(); ++iter){
        SDL_DestroyTexture(_textures[iter]);
    }
    if (_font != NULL){
        TTF_CloseFont(_font);
    }
    SDL_DestroyRenderer(_renderer);
    SDL_DestroyWindow(_window);
    IMG_Quit();
    TTF_Quit();
    SDL_Quit();
}
```

drw_sdl2_rect.h
```C++
#ifndef RECT_H
#define RECT_H

#include <SDL.h>

class Rect{
    public:
        Rect(int x, int y, int w, int h);
        Rect(int x, int y);
        int X, Y, W, H;
    private:
        SDL_Rect* _getsdlrect();
    friend class DrW_SDL2;
};

#endif // RECT_H
```

drw_sdl2_rect.cpp
```C++
#include "drw_sdl2_rect.h"

Rect::Rect(int x, int y, int w, int h){
    X = x;
    Y = y;
    W = w;
    H = h;
}

Rect::Rect(int x, int y){
    X = x;
    Y = y;
    W = -1;
    H = -1;
}

SDL_Rect* Rect::_getsdlrect(){
    SDL_Rect* output = new SDL_Rect;
    output->x = X;
    output->y = Y;
    output->w = W;
    output->h = H;
    return output;
}
```

libtest.cpp
```C++
#include "drw_sdl2.h"

const int SCREEN_WIDTH = 640, SCREEN_HEIGHT = 480;

int main(int argc, char **argv){
    DrW_SDL2 sdl;
    sdl.createWindow("test window", SCREEN_WIDTH, SCREEN_HEIGHT, true);
    int test = sdl.createTexture("TestTexture.png");
    int solidPink = sdl.setupTileset(test, Rect(1, 1, 20, 20));
    int halfandhalf = sdl.setupTileset(test, Rect(22, 1, 20, 20));
    int solidBlue = sdl.setupTileset(test, Rect(43, 1, 20, 20));
    sdl.renderclear();
    sdl.renderTexture(test, sdl.getSourceRect(test, solidPink), Rect(20, 20, 20, 20));
    sdl.renderTexture(test, sdl.getSourceRect(test, solidBlue), Rect(40, 40, 20, 20));
    sdl.renderTexture(test, sdl.getSourceRect(test, halfandhalf), Rect(40, 20, 20, 20));
    sdl.renderTexture(test, sdl.getSourceRect(test, halfandhalf), Rect(20, 40, 20, 20));
    sdl.setFont("fonts/freeserif.ttf", 16);
    int text = sdl.createText("test");
    sdl.renderTexture(text, 20, 20);
    sdl.renderpresent();
    SDL_Delay(2000);
    return 0;
}
```
