###Design It First

&nbsp;&nbsp;&nbsp;I have been on the cusp of making a roguelike for a long time now. 
As of Late I have mostly been stuck at redesigning my map generator over and over. 
My most complete attempt was a couple years ago for a 7drl and it failed because of early design choices. 
This basically means I could have avoided it if I had planned ahead and so this time around I will do so. 

&nbsp;&nbsp;&nbsp;To start let's layout what the game will be like overall. 
I want a simple twelve level dungeon with only a dash of flavor. 
Each level introduces a new enemy type with a few types from previous levels thrown in. 
There will be a "boss" on each level but you are not required to fight them ever. 
The combat will be low hp and probably the most complex bit because of time management. 
With the high level view layed out lets take a closer look at each bit. 

&nbsp;&nbsp;&nbsp;The number of levels was chosen at random. 
I actually had originally planned for 26 levels with each one devoted to a letter. 
That was a bit overboard and I decided to limit it for this. 
Each of the levels will be generated with my simple map gen so that is actually taken care of though I will probably go over that at a future date. 
As for the story there won't be much of it. 
Something really short about wanting to join the adventurers guild and this being the entrance exam.
Probably will fit it on the start screen. 

&nbsp;&nbsp;&nbsp;As for the enemies as I stated each level will introduce a new type. 
The original plan was for me to use the whole alphabet but my requirement for enemies made that not very practical. 
What I required was each enemy type being in some way unique. 
There is actually a little notebook I keep on me and it has a lot of notes in it. 
What my general consensus over a few months of design in that notebook is that 26 is too many for something as simple as I want. 
So yeah, with only 12 things I need to design this should be a lot easier for me to handle. 

&nbsp;&nbsp;&nbsp;Having a boss on each level was originally going to be a secret feature. 
Since I am posting about it that is no longer the case so the second purpose now will take the forefront. 
Basically the plan for the bosses is that they only show up if you defeat all enemies on a level. 
They also are the only form of advancement of your character besides hp. 
If you defeat a boss then when you go down the stairs you will be given an option of 3 power ups to choose from. 
The catch with the bosses is that they break the rules. 
Of course you don't have to fight them as the only goal on a level is to proceed to the next. 

&nbsp;&nbsp;&nbsp;The interesting bit where I will be dabbling the most with is combat. 
I want a bit more positioning and tactics without resorting quite to everything only having a single hitpoint. 
The player character will have a max hp of the level times 5 and it is restored when you go down to the next level. 
Monsters on the other hand will only have 1 hit point or if armored 2. 
Combat itself is where the most complicated bits will probably reside. 
There are pages of notes in my notebook on the time system I want to use and it is much too complicated for this. 
My basic plan to simplify it is reduce the numbers. 
As it is written I have all kinds of interesting mechanics but for this game I can't expect people to learn it. 
By reducing the numbers down to a range of 1 to 9 then even without understanding of the system people can comprehend it. 
Though I will still keep some of the interesting things such as damage happening at the end of the attack. 

&nbsp;&nbsp;&nbsp;The above gives a decent outline though it probably is missing some things. 
While randomly chosen the number of levels feels right. 
I believe I can manage 12 unique feeling enemies. 
The concept behind the bosses has been in my head for a while so should work out. 
With the combat it might take some jury rigging of my original design but that happens. 
So yeah overall it should all fit together but I still need to set this all into a nice bullet pointed list of goals. 

###The Bullet Pointing

&nbsp;&nbsp;&nbsp;Now above I have a lot words but very few talk about concrete requirements. 
Below I will be fixing this by taking what I talked about and some that I didn't and turning it into a nice little list. 
It will of course be based upon the above but go into more detail about the specifics. 
While I do reserve the right to change any of the following I wont do so without going into specifically why I am doing so. 
Anyway here is the list: 

* 12 dungeon levels
 * Generated with already existing dungeon generation code
 * Up and down stairs never generate next to each other
* Story fits on start screen
* 12 unique enemy types
 * Unique means they visibly act differently
 * Bosses are extensions of the current levels enemy type
* Bosses appear after clearing a level
 * They break the rules in some way
 * Defeating a boss gives a choice of 3 powerups
* Each powerup is a part of a category [ex: weapon]
 * There is a limit to one powerup per a category
 * Game warns you if you are picking a powerup that will replace a current one
* The way to advance is go down
 * HP is restored when you proceed to the next dungeon level
 * You can go down stairs at any point but you can't go back up
* Hp will stay relatively low
 * Monsters will have 1 or 2 hp
 * The player has 5 times the level he is on hp
* Every action takes a specific amount of time
 * The amount goes from 1 to 9
 * A basic attack or move takes 5
* Displaying it will be using Libtcod and not SDL
* I will not be touching the dungeon generation code

And that is the most I can plan out right now without getting to far into it. 
As a bit of a look into what I have been planning though below I will transcribe some of what I have about the time system. 
Of course this is also partly so that its backed up and not stuck in a fragile paper form. 

Basic move - 100

Basic attack - 100

1-hand small - 70

2-hand attack - 140 X

Sword and board - 120 X

Weapon speed mod - -10 to 10

2 weapon & shield should balance

sword and board - the weapon has normal attack and what the shield does is cost a certain number of action points each time it blocks and can only block one attack at a time. 
Chance to block goes down if also attacking at the same time. 

Where does the damage happen? 
The end is best of the simple but the middle or somewhere in that area would be more realistic. 
Damage happens at the end of the base attack time then the weapon speed mod happens. 
Speed mod from 0 to 20 instead of -10 to 10 and maybe take 10 off basic attack. 
Could still put weapon mod at -10 to 10 and have it 0 to 20 behind scene. 
No just 0 to 20. 

Shields have base 50% block and down to 25% during the time when you are attacking. 
The shields mod adds 4% a point (+2 is 8%) with +10 max for 90%/65%. 
~~Change block 1 attack at a time to one enemies attack at a time so if~~

How should speed work? 
Magical haste is simply half costs. 
Maybe in percentages? 
Lower is better and strictly a percentage. 
Basic is 100%. 
Physical improvement or worsening of speed is additive so -5 to speed causes 95% and always stacks with itself to min of -30 and is added first. 
~~Static magical affects stacks with itself~~
Static magical affects partially stacks. 
It can't cause below -80 after physical is counted in. 
The lowest is counted first and each successive gives a percentage which is equal to the current speed of the static magical. 

```
(-10 -5 5 10) 100 - 10 = 90 so 90% of -5 is -4.5 round up 90 - 5 = 85 so 85% of 5 is 4.25 round down 85 + 4 = 89 so 89% of 10 is 8.9 round up 89 + 9 = 98

-20 -5 +2 +13 = 90
100 - 20 = 80 - 4 = 76 + 2 = 78 + 10 = 88

-5 -5 -5 +10 = 95
100 - 5 = 95 - 5 = 90 - 5 = 85 + 9 = 94

-10 -10 -5 +25 = 100
100 - 10 = 90 - 9 = 81 - 4 = 77 + 19 = 96

-25 +5 +10 +10 = 100
100 - 25 = 75 + 4 = 79 + 8 = 87 + 9 = 96

-25 +10 +10 +5 = 100
100 - 25 = 75 + 8 = 83 + 8 = 95 + 5 = 100

+10 +5 +5 = 120
100 + 10 = 110 + 6 = 116 + 6 = 122

-25 -12 -5 +5 +12 +25 = 100
100 - 25 = 75 - 9 = 64 - 3 = 61 + 3 = 64 + 8 = 72 + 18 = 90

-25 -12 -5 +25 +12 +5 = 100
100 - 25 = 75 - 9 = 64 - 3 = 61 + 15 = 76 + 9 = 85 + 4 = 89

-25 +25 -12 +12 -5 +5 = 100
100 - 25 = 75 + 19 = 94 - 11 = 105 + 13 = 118 - 6 = 112 + 6 = 118

+25 -25 +12 -12 +5 -5 = 100
100 + 25 = 125 - 31 = 94 + 11 = 105 - 13 = 92 + 5 = 97 - 5 = 92
```

Need to make program to do more tests. 
Temp affects do not stack but apply last and are multiplicative. 
While they do not stack they don't cancel out so a 50% haste for 100 and a 10% for 1000 means after the 100 at 50% you still have 900 at 10%. 
The difference from static and active is static is something you don't have a choice about. 
Toggle affects or ones that cost something are active. 
Artifacts break the rules. 
The only thing for certain is min 1% total so it doesn't break the game. 

```
-10 -5 +15
100 - 10 = 90 - 4.5 = 86.5 + 12.975 = 99.475
100 - 10 = 90 - 5 = 85 + 13 = 98

-15 +5 +10
100 - 15 = 85 + 4.25 = 89.75 + 8.975 = 98.725
100 - 15 = 85 + 4 = 89 + 9 = 98
```

And then I complain about not being home and wanting to write a program to help test various ways of rounding the numbers. 
I also have a little drawing where I figure out various item slots I want. 
There is also a bit where I start figuring out what each letter will end up being. 
The one that I will probably keep is having 'a' being an ant and 'A' the ant queen.