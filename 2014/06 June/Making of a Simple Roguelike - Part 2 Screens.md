###Wherein I Admit to My Failure

&nbsp;&nbsp;&nbsp;First of my failures is not getting another post up. 
Sorry about that as I just started my internship and it is a bit of a sharp turn about for my mind. 
Anyway my lack of posting is only partly having to learn another language in only a couple days. 
Honestly at this point I have the basics so its only learning the specific keywords for it. 

&nbsp;&nbsp;&nbsp;The big problem and failure on my part is not being able to pick something and stick with it. 
I have in my spare time coded and recoded my method of storing the three default screens. 
There is no way to get around the fact that it is just a few giant blobs of characters. 
So yeah, at the point where I am typing this I am going to stick with just hardcoding them in. 

###Now for the Screens Themselves

&nbsp;&nbsp;&nbsp;The game screen where you will spend most of your time is important and thus I will begin with it.
It was the easiest and probably hardest screen to design. 
Even now the design isn't complete. 
I was doing some tests on my map gen and figured out that a short map made with it feels best for this. 
This means that I actually ended up with too much room. 

```
                                                                                
 +----------------------------------------------------+ +---------------------+ 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
 |####################################################| |                     | 
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

&nbsp;&nbsp;&nbsp;The field of walls is actually the size of the map. 
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
 |   here it means you want to join the             �     ����  ����  ���     | 
 |   Adventurers guild but not just                 �     �  �  �  �  �  �    | 
 |   anyone can do that. You will need              �     �  �  ����  �  �    | 
 |   your wits about you for this. I                �     �  �  �  �  �  �    | 
 |   have crafted a dungeon to test                 ����  ����  �  �  ���     | 
 |   your mind more than your brawn we                                        | 
 |   can make you stronger but the mind                                       | 
 |   is a bit harder to work with.                                            | 
 |   Anyway if your sure you want to                                          | 
 |   take the challenge sign here                   �   �  ����  �       �    | 
 |   here and here. Okay proceed do                 ��  �  �     �   �   �    | 
 |   the stairs and remember   Your                 � � �  ��    �   �   �    | 
 |   death isn't our fault and be                   �  ��  �      � � � �     | 
 |   careful as there are rumors of                 �   �  ����    �   �      | 
 |   some breaks in the magic and more                                        | 
 |   powerful monsters showing up.                                            | 
 |                                                                            | 
 |                                                                            | 
 |                                                   ���    �  �  ���  ���    | 
 |                                                  �   �   �  �   �    �     | 
 |                                                  �   �   �  �   �    �     | 
 |                                                  �   �   �  �   �    �     | 
 |                                                   ��� �   ��   ���   �     | 
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

&nbsp;&nbsp;&nbsp;Once again I am dealing with too much space. 
Anyway it doesn't look too bad. 
In game there will be a frame around whichever option is selected at the moment. 
But all that aside we now have all the screens we need. 
Yes there is a pause screen but I am going to take a shortcut with that. 
Libtcod can make a frame which overwrites what it is drawn over so I will simply be drawing that and then the options. 

&nbsp;&nbsp;&nbsp;With that out of the way though I now have to put it into the code. 
I am thinking a simple class that just has getStartScreen and getGameScreen which takes the argument of a char**.
It will actually be somewhat easier then it could be because of something I learned recently. 
Techincally it is something I should have known already but sometimes you just need stuff pointed out to you. 
The important thing I learned was that in notepad++ you can search and replace with regular expressions. 
I knew this but it took someone else pointing out that it means I can search for (.) and replace \1',' which will put that between each character. 

&nbsp;&nbsp;&nbsp;The problem that remains is caused by how I store the map I would have to rotate it because I go map[width][height]. 
I do this because it means when I am doing stuff in the code any array dealing with the map can be accessed with x,y. 
The problem in the past that I had was I would do it the other way and then get it all mixed up. 
So now I could just do the work, on the other hand I think just making a couple of private arrays going the other way will work fine. 
Once I put that down in code it seemed to work so I should be done with this. 