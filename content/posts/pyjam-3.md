---
title: "PyGame Group collision"
date: 2021-07-25T17:02:38+10:00
draft: false
---

Here is a little bit of an update, while Aaron has been busy refactoring I tried to at least get the "block" Western Harry to shoot bullets ( again blocks ) into block enemies.

Here is a little clip ( click to play ):

[![IMAGE ALT TEXT HERE](https://img.youtube.com/vi/Nc5zV3T-cCU/0.jpg)](https://www.youtube.com/watch?v=Nc5zV3T-cCU)


```python
collisions = pygame.sprite.spritecollide(self, bullet_group, False)
    for bullet in collisions:
        bullet_group.remove(bullet)
        player.update_score(10)

```
In the code I check for any collisions between the enemy and the bullets group.  For each collision I remove the bullet and increment the score by 10.  The score is currently held on the player class.

Paul.