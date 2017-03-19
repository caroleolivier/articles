# Fun with dice

This post is about a simple dice game without much excitement at first sight. However, as we dig deeper into several aspects of the game you will hopefully become as interested as I am about it.


## Problem

### Game

You roll a dice and win the amount shown by the dice. You can choose to keep this amount or roll a second time.

The dice is a normal 6 sided face dice with numbers 1, 2, 3, 4, 5, 6. Each number has equal probability of being rolled.

### Question

###### What is your rolling strategy?

Before you look at the solution, please take a minute (or more!) to think about what you would do. It is interesting at this stage to think about your strategy based on your intuition and/or mathematic tools you know of.

It may help (**or not!**) to think about what you would do if the faces of the dice were different. For instance 0, 0, 0, 0, 0, 1 or 1, 10, 100, 1000, 10000, 1000000.

### Solution

First of all, let's look at what we are trying to achieve: in this case, our goal is to **maximise the gain**. If you get confused come back to that statement. There are many facets to that game, it always helps to come back to where we started.

Let's look at the mean gain:

	1/6 x 1 + 1/6 x 2 + 1/6 x 3 + 1/6 x 4 + 1/6 x 5 + 1/6 x 6 = 3.5

So one roll gives us on average 3.5. Since the roll are independent:

* 1st roll: the player can hope to get 3.5 on average.
* 2nd roll: the player can hope to get 3.5 on average.

Let's go back to the original question "What is your rolling strategy?", i.e. when do you decide to roll twice? 

| Roll 	| 1st roll larger than mean ?	|	action |
| ---- 	| ------------------------- 	| -------- | 
| 1 	| 1 < 3.5 						| roll again|
| 2		| 2 < 3.5 						| roll again |
| 3		| 3 < 3.5						| roll again|
| 4		| 4 > 3.5 						| keep	| 
| 5		| 5 > 3.5 						| keep	| 
| 6		| 6 > 3.5						| keep	|

## Properties

### Mean gain

How much can you hope to gain?

| Roll 	| 1st roll 	| 2nd roll 	| Gain 	|
| ---- 	| -------- 	| ---------	| -----	|
| 1 	| -        	| 3.5		| 3.5	|
| 2		| -			| 3.5		| 3.5	|
| 3		| -			| 3.5		| 3.5	|
| 4		| 4			| -			| 4		|
| 5		| 5			| -			| 5		|
| 6		| 6			| -			| 6		|

So the mean gain of the game is:

	3.5 + 3.5 + 3.5 + 4 + 5 + 6 = 4.25


### Probability of rolling a 6

You may wonder what is the probability of rolling a 6 (please read __at least__ a 6) with 2 rolls.

The probability or rolling at least a 6 is equivalent to 1 - the probability of rolling 1, 2, 3, 4 or 5 with 2 rolls:

	P(at least one 6) = 1 - 5/6 x 5/6 ~ 30.6%




## Discussions

Let's explore the game further by playing with different dice or changing the rules.



### 3rd roll

You can now roll a 3rd time.

###### Strategy

Let's look at the gain again. What do we know:

* if I can roll once the mean gain is 3.5
* if I can roll twice the mean gain is 4.25.
* if I can roll three times the mean gain is ???.

With the first roll if I don't win more than the mean gain with 2 rolls I should play again. So 5 and 6 I stop but 1, 2, 3 and 4 I play again and it is then equivalent to playing a 2 roll game.

| Roll 	| 1st roll	| 2 next rolls	| Gain 	|
| ---- 	| -------- 	| ---------		|------	|
| 1 	| -        	| 4.25 			| 4.25 	|
| 2		| -			| 4.25			| 4.25	|
| 3		| -			| 4.25			| 4.25	|
| 4		| -			| 4.25			| 4.25	|
| 5		| 5			| -				| 5		|
| 6		| 6			| -				| 6		|

###### Mean gain

	4.25 + 4.25 + 4.25 + 4.25 + 5 + 6 = 4.67

###### Probability of rolling a 6

	P(at least one 6) = 1 - 5/6 x 5/6 x 5/6 = 57.9%


### Many rolls

###### Strategy

You may have detected a recurrence pattern.

Let's call G(n) the gain with n rolls.

* G(n) >= G(n-1): stop rolling (if you were to roll, i.e. play a n-1 roll game, you will gain on average G(n-1))
* G(n) < G(n-1): play a n-1 roll game.




### Different dices

Let's play with a different dice. The probability of each face is still the same however the numbers are different.

#### Dice 1
1, 1, 1, 2, 2, 100.

###### What is your rolling strategy?

Using the same method as before, i.e. looking at the mean (~17.8) you should conclude that if your fist roll isn't 100 you should always roll a 2nd time.

Is that example intuitive? We are all different but it seems to make sense.


#### Dice 2 
0, 0, 0, 1,000,000, 1,000,000, 1,000,000,000,000.

###### What is your rolling strategy?

The numbers are different but this example is actually very similar to the one before so if your 1st roll isn't 1,000,000,000,000 then you should roll a 2nd time.

Is that example intuitive? Again, we are all different but I found it a lot harder to guess, especially if we assume we are talking about money: if we roll £1 million we should roll again and, say the little voice in my head, take the 50% risk of getting £0.

The problem that is getting in the way here is the one of minimising the risk of not winning anything.

Let's take a sample of 72 people playing the game and compare 2 strategies:

###### Strategy 1
If the 1st roll is below the mean then roll a second time.

| Roll 	| 1st roll (72 players)	|	2nd roll (60 players remaining) | Total
| ---- 	| ---------------------	| ------------------------| -----
| 0 	| play again			| 	10	| 10
| 0		| play again			| 	10 	| 10
| 0		| play again			| 	10	| 10
| 1 m	| play again			| 	10	| 10
| 1 m	| play again			| 	10	| 10
| 1 b	| 12 keep				| 	10	| **22**

###### Strategy 2
If the 1st roll is 0 then play again.

| Roll 	| 1st roll (72 players)	|	2nd roll (36 players remaining) | Total
| ---- 	| ---------------------	| ------------------------| -----
| 0 	| play again			| 	6	| 6
| 0		| play again			| 	6 	| 6
| 0		| play again			| 	6	| 6
| 1 m	| 12 keep				| 	6	| 18
| 1 m	| 12 keep				| 	6	| 18
| 1 b	| 12 keep				| 	6	| **18**

###### Analysis

Gain	| Strategy 1	| Strategy 2
-----	| -------------	| ----------
0		| 30			| 18
1 m		| 20			| 36
1 b		| 22			| 18

So on average to **maximise the gain** you want to follow strategy 1. However, to **minimise the risk of not gaining anything** you want to follow strategy 2.

In the next section we look at how to minimise the risk of not gaining anything.



### Different problems

#### Minimising the risk

Let's go back to the normal dice.

This time you want to minimise the risk of not gaining anything but obviously you still want to maximise the gain as well.

###### Strategy

Using the median.

	1	2	3	|| 	4	5	6
		50%				50%

Depending on the risk you are ready to take, you may want to play again if it is a 3.









