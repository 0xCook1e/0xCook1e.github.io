---
title: TFC24 - Bad Invaders 
date : 2024-08-02 16:30:00 +0530
categories: [ctf, tfc24]
tags: [ctf, tfc24]
description: Bad Invaders
image: /assets/posts/TFC/banner.png
---

## Bad Invaders

Just a game. Win

### How to Play

We are given the game source code so we can see how it functions.

We are also given a python script to play the game.

### The Game

The game we are given is a simple game with 2 players 1 is a bot, 1 is a player (you). The task is simple. Kill the bot (invader) and get the flag... but there's a problem.

Initial analysis by playing the game we can see that the bot always goes to tile no 3 and to shoot it we need to be on tile 3. But there is a barrier between us and the bot. We can't shoot through the barrier.

So I checked the source code for more information on how to beat the game.

```go
hit := player.Position == otherPlayer.Position && player.Position != 3

if hit {
    FLAG := os.Getenv("FLAG")
    if FLAG == "" {
        FLAG = "The flag should be here. If you see this on remote, contact an admin"
    }
    player.Conn.Write([]byte(PayloadError(FLAG)))
}
```

So as we can see if the bot or the player is on tile 3 we can't get the flag. So, my next move was to see how to make the bot move.

### Making the Bot Move

Code on server side responsible for moving the bot

```go
func (g *Game) MovePlayer(id int, position int) error {
	player, ok := g.Players[id]

	if !ok {
		return errors.New("Player not found")
	}

	if position != 0 && position != 1 {
		return errors.New("Invalid move")
	}

	if position == 0 {
		position = -1
	}

	player.Position += position
	if player.Position < 0 {
		player.Position = 0
	}
	if player.Position >= 9 {
		player.Position = 8
	}
	g.Players[id] = player

	g.Broadcast(PayloadMovePlayer(player.Name, player.Position))

	return nil
}
```

