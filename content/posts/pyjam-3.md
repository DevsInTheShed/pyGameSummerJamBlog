---
title: "PyGame Group collision"
date: 2021-07-25T5:02:38+10:00
draft: false
---

Here is a little bit of an update, while Aaron has been busy refactoring I tried to atleast get the "Block" Harry to shoot bullets ( again blocks ) into block enemies.

here is a little clip:

<iframe width="1280" height="1067" src="https://www.youtube.com/embed/Nc5zV3T-cCU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>


```python
collisions = pygame.sprite.spritecollide(self, bullet_group, False)
    for bullet in collisions:
        bullet_group.remove(bullet)
        player.update_score(10)

```
In the code I check for any collisions between the enemy and the bullets group.  For each collision I remove the bullet and inctrement the score by 10.  The score is currently help on the player class.

Paul.