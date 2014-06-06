###So Libtcod
As I noted in the planning post and the heading just above here I am going to use Libtcod for my roguelike. 
If you don't know of Libtcod it is a free API for roguelike development which provides many useful things like advanced true color console and input. 
Now we have that out of the way we need a project to work on and add it too. 
I start with a blank project called JoiningTheAdventurersGuild but if your following along you can call yours whatever you want.

To get Libtcod up and running in our project we need to grab it first. 
I am using [the 1.5.2 Windows version](http://doryen.eptalys.net/libtcod/download/ "There are a number of options for other languages there as well") to do this. 
In it there are a number of files but the ones we need to stick in our project folder are as follows:

* libtcod-mingw.dll
* libtcod-mingw-debug.dll
* SDL.dll
* terminal.png

The png is very important as without it your program won't run. 
I had a good bit of trouble when I was working with the C# binding of libtcod as it didn't have it include for some reason. 
Anyway with that the next step is to make sure the project knows what to do with it all so into build options. 
Under debug in linker settings add a link to the libtcod\lib\libtcod-mingw-debug.a and then switch over to release and link to libtcod\lib\libtcod-mingw.a and we are good. 
Of course doing all this wont put anything on the screen and this isn't quite the point to go into how to use libtcod so I will just note that I copied the main.cpp from my default setup of libtcod to test it. 
If you want to take a look at it the first commit for [the project on github](https://github.com/Akhier/JoiningTheAdventurersGuild "The file tests not only opening a window but catching input") has the code. 
With that I built and subsequently ran the project and everything worked. 
Now if you had problems there are some really good tutorials so take a look around or you can ask on [the Libtcod forum](http://doryen.eptalys.net/forum/index.php?board=12.0 "Even if you don't want to post take a look there as if your having a problem someone else probably did too"). 
My suggestion for a C++ roguelike tutorial using Libtcod is [here at Code::Umbra](http://codeumbra.eu/complete-roguelike-tutorial-using-c-and-libtcod-part-1-setting-up "It may or may not be a bit out of date, I hav eonly used bits and never actually fully followed it") 

###Foundations

Now to get some basic things hashed out. 
I looked into various ways of managing the game state and have decided I don't want any of the more complex stuff. 
There will be a start/home screen, the ingame stuff, and a menu for saving and quiting. 
They all stack one right on top of another and I will be dealing with this using some functions each with a while loop in it. 
Mind you the proper way would be to make an actual game state manager but that can be put in later 
(If you haven't been programming for long this is like saying I will clean my room tommorow. You almost never go back and do stuff you put off if it works.). 
Anyway I want to do some coding so I am going to try and mock up what I want with this and put what I end up with below. 

```C++
#include "libtcod.hpp"
int main() {
    TCODConsole::initRoot(80,50,"Joining The Adventurers Guild",false);
    return MainScreen();
}

int MainScreen() {
    bool done = false;
    while (!done) {
        drawScreen(&mainscreen);
        handleInput();
        //MainScreen Logic
        int gameoutput;
        if (gamestart) {
            gameoutput = GameScreen(randseed);
        }
        if (gameload) {
            gameoutput = GameScreen(levelseed);
        }
        if (gameoutput > 0) {
            setLoadSlot(gameoutput);
        }
        if (quit || gameoutput == -1) {
            done = true;
        }
    }
    return 1;
}

int GameScreen(int seed) {
    bool ingame = true;
    int gameoutput = 0;
    while (ingame) {
        drawScreen(&gamescreen);
        handleInput();
        //GameScreen Logic
        int pauseoutput
        if (paused) {
            pauseoutput = PauseScreen(&gamescreen);
        }
        if (pauseoutput == 1) {
            gameoutput = level;
            ingame = false;
        }
        if (gameover || pauseoutput == -1) {
            gameoutput = -1;
            ingame = false;
        }
    }
    return gameoutput;
}

int PauseScreen(/*some map or custom struct*/ &gamescreen) {
    bool paused = true;
    int pauseoutput = 0;
    while (paused) {
        drawScreen(&pausescreen);
        handleInput();
        //PauseScreen Logic
        if (quitgame) {
            pauseoutput = -1;
            paused = false;
        }
        if (savegame) {
            pauseoutput = 1;
            paused = false;
        }
    }
    return pauseoutput;
}
```

