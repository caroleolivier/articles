# Fun with dice

This post is about a simple dice game without much excitement at first sight. However, as we dig deeper into several aspects of the game you will hopefully become as interested as I am about it.


## Problem

### Game

You roll a dice and win the amount shown by the dice. You can choose to keep this amount or roll a second time.

The dice is a normal 6 sided face dice with numbers 1, 2, 3, 4, 5, 6. Each number has equal probability of being rolled.

### Question

###### What is your rolling strategy?

Before you look at the solution, please take a minute (or more!) to think about what you are trying to achieve and what you would do to achieve it.

It is very interesting at this stage to think about the strategy you would adopt if you were to follow your intuition and later check if you were right or wrong and why.

Here are a couple of teasers as well (that may help or not!):

* What if the faces were different? For instance 0, 0, 0, 0, 0, 1.
* Or 1, 1, 1, 1000, 10000, 1000000
* What if you could throw an infinite amount of time?


### Solution

First of all, let's look at what we are trying to achieve: in this case, our goal is to **maximise the gain**. If you get confused come back to that statement. There are many facets to that game, it can help to come back to that statement.

Let's look at the mean gain of rolling a dice once:

	1/6 x 1 + 1/6 x 2 + 1/6 x 3 + 1/6 x 4 + 1/6 x 5 + 1/6 x 6 = 3.5

So in English: rolling the dice once wins us on average 3.5. Based on this, if the first roll is below the average then we roll again but if it is above then we stop, chances are we won't win more.

| Roll 	| 1st roll larger than mean ?	|	action |
| ---- 	| ------------------------- 	| -------- | 
| 1 	| 1 < 3.5 						| roll again|
| 2		| 2 < 3.5 						| roll again |
| 3		| 3 < 3.5						| roll again|
| 4		| 4 > 3.5 						| keep	| 
| 5		| 5 > 3.5 						| keep	| 
| 6		| 6 > 3.5						| keep	|



## Properties

Before looking at different variants, let's take a quick look at a couple of properties of the game.

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

How would calculate the probability of rolling a 6 (please read __at least__ a 6) with 2 rolls?

	P(6) = P(6 first roll) + P(6 second roll) = 1/6 + 5/6 x 1/6 = 11 / 36 ~ 30.6%


You can also look at the inverse property: the probability of rolling at least a 6 is the inverse of not rolling a 6 at all:

	P(at least one 6) = 1 - P(no 6) * P(no 6) = 1 - 5/6 x 5/6 = 11 / 36 ~ 30.6%



## Discussions

Now that we looked at the basics of the game, let's have `fun with dice`!


### 3rd roll

You can now roll a 3rd time.

###### Strategy

Let's look at what we know::

1. The mean gain of 1 roll is 3.5
2. The mean gain of 2 rolls is 4.25

Using 2. and the same reasoning we used for a 2 roll game: if the 1st roll isn't above the mean gain of 2 rolls, i.e. 5 or 6, then we should play again:

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

Using the same method as before, i.e. looking at the mean (~17.8) you should conclude that if your 1st roll isn't 100 you should roll a 2nd time.

Is that example intuitive? We are all different but it seems to make sense.


#### Dice 2 
0, 0, 0, 1,000,000, 1,000,000, 1,000,000,000,000.

###### What is your rolling strategy?

Using the method we have been using so far: if your 1st roll isn't 1,000,000,000,000 then you should roll a 2nd time.

Is that example intuitive? Again, we are all different but somehow I found it a lot harder to accept, especially if we assume we are talking about money. Here we are saying that if we roll £1 million we should roll again and, say the little voice in my head, take 50% risk of getting £0 (<= :O).

I find it really strange, especially since this example is actually quite similar to the previous one, the main difference being the scale of the numbers. So what happened?

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









