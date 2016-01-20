title: Dice Game Probability
date: 2016-01-17 14:29:52
categories:
- Interview
tags:
- Technical Interview
comments: true
---

You are playing a game of dice with a friend. Your friend will roll one die, and you must pay the hunber of dollars for the number they roll. What should you charge you friend to play this game, if you want to break even in the long run? This value is the "fair value" of the game. It's easy to see that for a one roll game, the fair value is 3.5

Extend this to a game with up to 2 rolls of the die: you friend can either stop at the first roll, and keep that number, or choose to roll again, but then must take the 2nd number. Assume your friend will take the first roll if the number on the die is more than the fair value if they roll again. Otherwise, they'll choose to roll again (effectively playing a 1 roll game). What should you charge your friend to play this 2 roll game to break even in the long run.

Extend this to a game with up to N rolls of the die. They can roll again up to N times (each time playing the game with one less roll), but must take the last roll if they choose to roll the last time.

Write a function that computes the "fair value" for an N-roll game, where N is an integer larger than 0.

Here is an example of a 3-roll game, assuming you've decide the fair value is `$3`: Your friend gives you `$3`. Your friend rolls a 1, and decides to rll again (they know the fair value of a 2 roll game is more than 1). They roll again, this time is a 2; they decided to roll gain since they know that a one roll game's fair value is 3.5. On the last roll, your friend roll s a 1. So you pay `$1` and your net gain is `$2`.

```python
def die_game_fair_value(rolls):
	if (rolls ==1 ):
		return int(3.5)
	else:
		array = [3.5]
		i = 1
		while (i < rolls):
			res = int(array[i - 1])/6.0 * array[i-1] + 1/6.0 * (6+ int(array[i-1]) + 1) * (6 - int(array[i-1])) / 2.0
			array.append(res)
			i += 1
	
	return int(array[rolls - 1])
```