---
title: "Level world builder"
date: 2021-07-28T22:05:50+10:00
draft: false
---

Just a quick update for today, Matt and Paul are at a work event tonight, so I'm taking a small break too. But just so that we have some progress, tonight I implemented the level world builder.

All its doing at the moment is drawing tiles onto the view screen (and placing enemies into the world)

![image info](https://pygamesummerjam.devsintheshed.com/images/levelWorld.png) 

I just wanted to implement the world builder to at least process the level data.
As you can see here its not really doing much yet, accept reading in the data and placing the obstacles (ground and wall tiles) and enemies, and drawing them (when called on the level class)

```python
class World():
    def __init__(self, player):
        self.player = player
        self.enemies = []
        self.obstacles = []
    
    def processData(self, data):
        # iterate through level data
        for y, row in enumerate(data):
            for x, tile in enumerate(row):
                if tile >= 0:
                    tileImg = TileList[tile]
                    tileRect = tileImg.get_rect()
                    tileRect.x = x * TileSize
                    tileRect.y = y * TileSize
                    tileData = (tileImg, tileRect)

                    #obstacles
                    if tile >= 0 and tile <= 8:
                        self.obstacles.append(tileData)

                    #water
                    elif tile >=9 and tile <= 10:
                        pass 
                    
                    #decorators
                    elif tile >=11 and tile <= 14:
                        pass 
                    
                    #enemies
                    elif tile == 15:
                        self.enemies.append(Enemy(EnemyTypes["alien1"], tileRect.x, tileRect.y, 2, self.player))

                    #ammo
                    elif tile == 16:
                        pass

                    #weapon
                    elif tile == 17:
                        pass
                    
                    #health
                    elif tile == 18:
                        pass

                    #exit
                    elif tile == 19:
                        pass

        return self.enemies
                
    
    def draw(self):
        for tile in self.obstacles:
            ViewScreen.blit(tile[0], tile[1])
        
        for enemy in self.enemies:
            enemy.draw()
```

Thats it for tonight. tomorrow I will implement window scrolling so that when the player moves to the edge of the view screen the platform will scroll.

then we need to implement power up classes like ammo, health and weapons so that we can build them to interact  with their corresponding tiles when the player runs over them.

Aaron.
