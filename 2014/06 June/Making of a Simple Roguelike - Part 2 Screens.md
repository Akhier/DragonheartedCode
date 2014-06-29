###Wherein I Admit to My Failure

First of my failures is not getting another post up. 
Sorry about that as I just started my internship and it is a bit of a sharp turn about for my mind. 
Anyway my lack of posting is only partly having to learn another language in only a couple days. 
Honestly at this point I have the basics so its only learning the specific keywords for it. 

The big problem and failure on my part is not being able to pick something and stick with it. 
I have in my spare time coded and recoded my method of storing the three default screens. 
There is no way to get around the fact that it is just a few giant blobs of characters. 
So yeah, at the point where I am typing this I am going to stick with just hardcoding them in. 

###Now for the Screens Themselves

The game screen where you will spend most of your time is important and thus I will begin with it.
It was the easiest and probably hardest screen to design. 
Even now the design isn't complete. 
I was doing some tests on my map gen and figured out that a short map made with it feels best for this. 
This means that I actually ended up with too much room. 

```
                                                                                
 +----------------------------------------------------+ +---------------------+ 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |        Hands        | 
 |####################################################| |      LongSword      | 
 |####################################################| |                     | 
 |####################################################| |         Hat         | 
 |####################################################| |     SteelHelmet     | 
 |####################################################| |                     | 
 |####################################################| |        Armor        | 
 |####################################################| |      Platemail      | 
 |####################################################| |                     | 
 |####################################################| |        Pants        | 
 |####################################################| |    ChainLeggings    | 
 |####################################################| |                     | 
 |####################################################| |        Boots        | 
 |####################################################| |   SandelesOfSpeed   | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 +----------------------------------------------------+ |                     | 
                                                        |                     | 
 +------------------------------------------------------+                     | 
 |                                                                            | 
 | HP:05                            a                                         | 
 |                                                                            | 
 | MoveRate: 5                      b                                         | 
 |                                                                            | 
 | DR Chance: %00                   c                                         | 
 |                                                                            | 
 | Block Chance: %00                d                                         | 
 |                                                                            | 
 | Dodge Chance: %00                e                                         | 
 |                                                                            | 
 +----------------------------------------------------------------------------+ 
                                                                                
                                                                                                                                                              
```

The field of walls is actually the size of the map. 
It makes for a compact and relatively lineir experaince when I must admit my map gen wallows in dead ends and confusion normally. 
Letters are where equipment will be listed as I want it to be descriptive since there are only five spots. 
Now I just have to figure out what to do with the side. 
This doesn't matter though and it could just end up blank so onwards. 

Start up and what does the screen you see look like? 

```
                                                                                
 +----------------------------------------------------------------------------+ 
 |                                                                            | 
 |                                                                            | 
 |                                                                            | 
 |   Welcome to a challenge. If you are                                       | 
 |   here it means you want to join the             ¦     ¦¦¦¦  ¦¦¦¦  ¦¦¦     | 
 |   Adventurers guild but not just                 ¦     ¦  ¦  ¦  ¦  ¦  ¦    | 
 |   anyone can do that. You will need              ¦     ¦  ¦  ¦¦¦¦  ¦  ¦    | 
 |   your wits about you for this. I                ¦     ¦  ¦  ¦  ¦  ¦  ¦    | 
 |   have crafted a dungeon to test                 ¦¦¦¦  ¦¦¦¦  ¦  ¦  ¦¦¦     | 
 |   your mind more than your brawn we                                        | 
 |   can make you stronger but the mind                                       | 
 |   is a bit harder to work with.                                            | 
 |   Anyway if your sure you want to                                          | 
 |   take the challenge sign here                   ¦   ¦  ¦¦¦¦  ¦       ¦    | 
 |   here and here. Okay proceed do                 ¦¦  ¦  ¦     ¦   ¦   ¦    | 
 |   the stairs and remember   Your                 ¦ ¦ ¦  ¦¦    ¦   ¦   ¦    | 
 |   death isn't our fault and be                   ¦  ¦¦  ¦      ¦ ¦ ¦ ¦     | 
 |   careful as there are rumors of                 ¦   ¦  ¦¦¦¦    ¦   ¦      | 
 |   some breaks in the magic and more                                        | 
 |   powerful monsters showing up.                                            | 
 |                                                                            | 
 |                                                                            | 
 |                                                   ¦¦¦    ¦  ¦  ¦¦¦  ¦¦¦    | 
 |                                                  ¦   ¦   ¦  ¦   ¦    ¦     | 
 |                                                  ¦   ¦   ¦  ¦   ¦    ¦     | 
 |                                                  ¦   ¦   ¦  ¦   ¦    ¦     | 
 |                                                   ¦¦¦ ¦   ¦¦   ¦¦¦   ¦     | 
 |                                                                            | 
 |                                                                            | 
 |                                                                            | 
 |                                                                            | 
 |                                                                            | 
 |                                                                            | 
 |                                                                            | 
 |                                                                            | 
 |                                                                            | 
 +----------------------------------------------------------------------------+ 
                                                                                
```