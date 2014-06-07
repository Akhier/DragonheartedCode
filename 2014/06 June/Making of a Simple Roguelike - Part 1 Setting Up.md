###So Libtcod

&nbsp;&nbsp;&nbsp;As I noted in the planning post and in the heading just above here, I am going to use Libtcod for my roguelike. 
If you don't know of Libtcod it is a free API for roguelike development and provides many useful things like advanced true color console and input. 
Now we have that out of the way we need a project to work on and add it too. 
I start with a blank project called JoiningTheAdventurersGuild but if your following along you can call yours whatever you want.

&nbsp;&nbsp;&nbsp;To get Libtcod up and running in our project we need to grab it first. 
I am using [the 1.5.2 Windows version](http://doryen.eptalys.net/libtcod/download/ "There are a number of options for other languages there as well") to do this. 
In it there are a number of files but the ones we need to stick in our project folder are as follows:

* libtcod-mingw.dll
* libtcod-mingw-debug.dll
* SDL.dll
* terminal.png

&nbsp;&nbsp;&nbsp;The png is very important as without it your program won't run. 
I had a good bit of trouble when I was working with the C# binding of libtcod as it didn't have it include at the time for some reason. 
The next step is to make sure the project knows what to do those files so into build options. 
Under debug in linker settings add a link to the libtcod\lib\libtcod-mingw-debug.a and then switch over to release and link to libtcod\lib\libtcod-mingw.a. 
Of course doing all this wont put anything on the screen and this isn't quite the point to go into how to use libtcod so I will just note that I copied the main.cpp from my default setup of libtcod to test it. 
If you want to take a look at it the first commit for [the project on github](https://github.com/Akhier/JoiningTheAdventurersGuild "The file tests not only opening a window but catching input") has the code. 
With that I built and subsequently ran the project and everything worked. 
Now if you had problems there are some really good tutorials so take a look around or you can ask on [the Libtcod forum](http://doryen.eptalys.net/forum/index.php?board=12.0 "Even if you don't want to post take a look there as if your having a problem someone else probably did too"). 
My suggestion for a C++ roguelike tutorial using Libtcod is [here at Code::Umbra](http://codeumbra.eu/complete-roguelike-tutorial-using-c-and-libtcod-part-1-setting-up "It may or may not be a bit out of date, I have only used bits and never actually fully followed it") 

###Foundations

&nbsp;&nbsp;&nbsp;Now to get some basic things hashed out. 
I looked into various ways of managing the game state and have decided I don't want any of the more complex stuff. 
There will be a start/home screen, the in-game stuff, and a menu for saving and quitting. 
They all stack one right on top of another and I will be dealing with this using some functions each with a while loop in it. 
Mind you the proper way would be to make an actual game state manager but that can be put in later 
(If you haven't been programming for long this is like saying I will clean my room tomorrow. You almost never go back and do stuff you put off if what you have it works). 
Anyway I want to do some coding so I am going to try and mock up what I want with this and put what I end up with below. 

```C++
#include "libtcod.hpp"
int MainScreen() {
    bool done = false;
    while (!done) {
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
        drawScreen(&mainscreen);
    }
    return 1;
}

int GameScreen(int seed) {
    bool ingame = true;
    int gameoutput = 0;
    while (ingame) {
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
        drawScreen(&gamescreen);
    }
    return gameoutput;
}

int PauseScreen(const /*some map or custom struct array*/ &gamescreen) {
    bool paused = true;
    int pauseoutput = 0;
    while (paused) {
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
        drawScreen(&pausescreen);
    }
    return pauseoutput;
}

int main() {
    TCODConsole::initRoot(80,50,"Joining The Adventurers Guild",false);
    return MainScreen();
}
```

&nbsp;&nbsp;&nbsp;The above code wont work but it should show what I intend. 
I am basically stacking the states one on top of another with the only complicated bit being going to the pause screen. 
What is happening there is that I want the game screen to be in the background and maybe grayed out so I pass the current game screen to it. 
It is being passed as a const because I don't want it to be changed and this enforces that. 
Anyway this was the easy setup bit, all the fun and hard stuff goes in those comments mentioning logic and possibly whatever happens in handleInput. 

&nbsp;&nbsp;&nbsp;Speaking of handleInput I have figured out how I want to do it. 
Really when it comes down to it there is two control schemes only. 
A menu control scheme and the ingame control scheme. 
Since two of three are the menu version I can use a bool as the argument and the menu version will be true. 
Also lets rename it to getInput as I have decided to have it just return an int depending on what key is pressed with any result that doesn't do anything returning -1. 
The actual function code will be a simple switch statement. 
Code for both the change to the call and the implementation are just below. 

```C++
int inputcode = getInput(true);
```

```C++
int getInput(bool menuscheme) {
    TCOD_key_t key = TCODConsole::checkForKeypress();
    if (menuscheme){
        if (key.vk == TCODK_ENTER || key.vk == TCODK_KPENTER) {
            return 0;
        }
        else if (key.vk == TCODK_ESCAPE || TCODK_BACKSPACE) {
            return 1;
        }
        else if (key.vk == TCODK_DOWN || key.vk == TCODK_KP2) {
            return 2;
        }
        else if (key.vk == TCODK_UP || key.vk == TCODK_KP8) {
            return 3;
        }
        else {
            return -1;
        }
    }
    else {
        switch(key.vk) {
            case TCODK_ESCAPE:
                return 0;
                break;
            case TCODK_CHAR:
                switch (key.c) {
                    default:
                        return -1;
                        break;
                }
                break;
            default:
                return -1;
                break;
        }
    }
}
```

&nbsp;&nbsp;&nbsp;Do note that I have only filled out the menu keys. 
I only put how to deal with characters and the escape key in the game keys as I wanted to show how to do it. 
With that in place I now need to figure out how I will handle what to draw. 
It could be easy if I only wanted to use characters and everything was the same color. 
That is not the case though as I want colored enemies. 
This means a struct which contains the character and the color as follows:

```C++
struct Tile {
    char Symbol = ' ';
    TCODColor foreColor = TCODColor.lightestGrey;
    TCODColor backColor = new TCODColor(15,15,15);
};
```

&nbsp;&nbsp;&nbsp;Take note of the default backColor. 
While not important programmatically it is for the color as a pure black can be to severe a contrast. 
Now to decide how the screen data is stored. 
Because the screen is always the same size I am thinking a simple 2d array of Tiles.
With this decided I can write the drawScreen function.

```C++
void drawScreen(const Tile screen[][WINDOW_HEIGHT]) {
    TCODConsole::root->clear();
    for (int column = 0; column < WINDOW_HEIGHT; ++column){
        for (int row = 0; row < WINDOW_WIDTH; ++row){
            TCODConsole::root->putCharEx(row, column, screen[row][column].Symbol, screen[row][column].foreColor, screen[row][column].backColor);
        }
    }
    TCODConsole::flush();
}
```

&nbsp;&nbsp;&nbsp;And that along with a couple of updates to the code all the remaining errors end up being about things not existing. 
More importantly those things don't exist because they are to be implimented in the logic. 
I now have some of the framework needed to get it running in some form. 
About all I can see needing to have the basic start up screen working is said start up screen. 
That will require what ends up being me just hardcoding the menu screens. 

####Small Addon

&nbsp;&nbsp;&nbsp;As a bit of a fun addition I will layout how I plan to make dogs act. 
They will be the new monster on the 4th dungeon level and represented by a brown 'd'.
Anyway I figured out a simple state machine setup for them that will make them hunt in a pack or so I hope. 
A dog will have three states depending on whether it can see other dogs or the player. 
The one they start in is alone and would be something like the following:

```
If see_player
   move_away
Else If saw_player
   reverse_of_last_move
Else
   rand_walk
If see_dog
   leave alone enter inpack
```

Next as you might intuit from the above will be the state of inpack

```
If see_player
   leave inpack enter hunting
If see_hunting_dog
   move_closer
else
   If distance_to_nearest_dog < 3
      move_away
   If !_see_dog
      leave inpack enter alone
   If distance_to_nearest_dog > 6
      move_closer
   else
      rand_walk
```

Finally of course is the state called hunting

```
If next_to_player
   attack_player
Else If see_player
   If other_dog_closer_to_player
      move_closer
   Else
      keep_distance_but_move
If saw_player
   move_towards_player
Else
   leave hunting enter alone
```

&nbsp;&nbsp;&nbsp;And with that I hope to make an interesting pack behavior. 
If the dog is alone just wander or avoid the player but only just. 
When he finds another dog they will try to stay together but not too close. 
Finally if a dog that is currently in a pack sees the player other dogs that can see it will go to it. 
All dogs that can see the player will try to be just as close to the player as any other dog. 
In the end no dog will actually try to attack the player directly but if the player approachs a dog they will all get closer. 
I am basically trying to get the dogs to stay on the edge until the player either purposefully approaches them or ends up having to do so. 

&nbsp;&nbsp;&nbsp;Really it will be a interesting choice for the player. 
Do you deal with the dog now even though it will run away till it has a friend?
How many do you let follow you before it is too many?
And finally now that you let them follow you so far and you see a dog at the other end of the room how will you survive?

At least that is my hope for them