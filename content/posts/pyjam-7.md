---
title: "Game Scaffold - Refactor 2"
date: 2021-07-26T20:15:50+10:00
draft: false
---

So I learned a bit about Python during setting up the game scaffoled, as I'm sure you seasoned Python devs would think something simple, but as a programmer used to other languages I found the Package structure in Python interesting. Not being able to import pacakges from folders higher in the tree was a little anoying, so was having to inject all the classes that I wanted from the package higher in the tree... this was becoming unruly, so ended up pulling the screens folder out of the game folder and put it parallel.

so went from:

![image info](https://pygamesummerjam.devsintheshed.com/images/Screenshot_oldtree.png) 

to everyting at the same level:

![image info](https://pygamesummerjam.devsintheshed.com/images/Screenshot_newtree.png) 

so after that change, finishing the game scaffold (all the screen modules and the stage screen calling the level modules) was easy to finish.

Then I refactored the player and enemy classes into a single Character class that player and enemy inherit from, to reduce the amound of doubled sprite animation and interaction code, and just gave the player and emeny their own sepcific properties.

for the Player class now all its doing is mananging the user interaction through the update_action call on player.draw(), handling the update() for weapon cooldown and shooting the specific weapon (at this stage only shotgun):  

![image info](https://pygamesummerjam.devsintheshed.com/images/code_player.png)


and just so you can see what a weapon class does, its pretty simple, it just handles if its active or not (meaning is it usable, so when the player picks it up its available to cycle through in the weapons list), ammo and cooldown:

![image info](https://pygamesummerjam.devsintheshed.com/images/code_weapon.png)

Thats it for me tonight!! basic refactor and scaffold is done!
Next I'll move onto the stage HUD, to see the player health, ammom current weapon etc.

- Aaron.
