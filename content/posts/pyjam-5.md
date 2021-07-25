---
title: "Game Scaffold - Refactor 1"
date: 2021-07-25T19:09:45+10:00
draft: false
---

So while Matt was working on the main character art and Paul was working on the player and enemy interactions, I was refactoring what Paul had done earlier and building out a basic game scaffold, to handle different game screens.

Before I started coding, I put together a very simple storyboard to understnd what screens we will need:

![image info](https://pygamesummerjam.devsintheshed.com/images/01_main.PNG) 
![image info](https://pygamesummerjam.devsintheshed.com/images/02_intro.PNG) 
![image info](https://pygamesummerjam.devsintheshed.com/images/03_stage.PNG) 
![image info](https://pygamesummerjam.devsintheshed.com/images/04_end.PNG) 
![image info](https://pygamesummerjam.devsintheshed.com/images/05_credits.PNG) 


Based on the storybaord, I created a module for each screen, which will handle the draw() (updateing the view screen) for itself. 

Then I started codign it all together into a State Management class:
```python
class GameState:
    def __init__(self, globals):
        self.screens = enums.Screen
        self.currentScreen = self.screens.menu

        player = Character('player', 200, 200, 3, 5, globals.GRAVITY)
        player.actions = enums.Action

        scrMenu = menu.Menu(globals, self)
        scrIntro = intro.Intro(globals, self)
        scrStage = stage.Stage(globals, self, player)
        scrEnd = end.End(globals, self)
        scrCredits = credits.Credits(globals, self)

        self.view = {
            enums.Screen.menu: lambda : scrMenu.draw(),
            enums.Screen.intro: lambda : scrIntro.draw(),
            enums.Screen.stage: lambda : scrStage.draw(),
            enums.Screen.end: lambda : scrEnd.draw(),
            enums.Screen.credits: lambda : scrCredits.draw(),
        }

    def gotoScreen(self, screen):
        self.currentScreen = screen

    def render(self):
        return self.view[self.currentScreen]()

```
This code is what I put together to manage all the screens, in a single Game State to handle the current screen and navigating between.

Aaron.