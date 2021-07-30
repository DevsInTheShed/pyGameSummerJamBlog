---
title: "Level world builder"
date: 2021-07-29T20:01:42+10:00
draft: false
---

So today I added collision detection and level scroll, so we can extend the level beyond the edges of the view screen.

The collision detection I added to the World class, that you will recall from yesterdays post "Level world builder" which plots and draws each of the different tile types onto the view screen. As you can see, it is a very simple function to check if the Character rect (player and enemy both inherit character) colides with the rect from the block list:

```python
def collision(self, blocklist, character):
    for block in blocklist:
        feet = character.rect.bottom - TileSize

        #collide left
        if block.rect.collidepoint(character.rect.right - TileSize, feet):
            character.state[pygame.K_RIGHT] = False
            character.rect.x -= 1

        # collide right
        if block.rect.collidepoint(character.rect.left + TileSize, feet):
            character.state[pygame.K_LEFT] = False
            character.rect.x += 1

        # collide feet
        if block.rect.collidepoint(character.rect.centerx, character.rect.bottom):
            if character.velocity_y >= 0:
                character.velocity_y = 0
                character.in_air = False
                character.delta_y = block.rect.top

        # collide head
        if block.rect.collidepoint(character.rect.centerx, character.rect.top):
            if character.velocity_y < 0:
                character.velocity_y = 0
                character.delta_y = block.rect.bottom
```

And then to make sure this is applied to both Player and Enemy classes, we call the collid method  in the update method.
you will also see that when the player collides with water, the player health is reduced to 0... This is temporary, as curretly when the player respawns they start in the same place they died, so we will need to fix this. 

```python
def update(self):
    feet = self.player.rect.bottom - TileSize

    self.collision(self.obstacles, self.player)

    for enemy in self.enemies:
        self.collision(self.obstacles, enemy)

    for wet in self.water:
        if wet.rect.colliderect(self.player):
            self.player.health = 0
```

I'm not completely happy with how the collision is currenly working, as personaly I would prefer the collision for the character be handled on the character not in the world, so I may look at raising a custom pygame.event to signal the colission and move the collision logic to the character class.  

Aaron.
