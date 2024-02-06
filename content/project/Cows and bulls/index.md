---
title: Game of Cows and Bulls
summary: I wrote this python program as a solver for a game of cows and bulls which broke out between friends during a particularly boring train ride. The Wrapper GUI is written in PyQt and designed using QT designer. All processing is done in python.

tags:
- Python
- PyQt
- Graph
- Algorithm
- Data Processing
date: "2018-10-26T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: Photo by Juliana Amorim on Unsplash
  focal_point: Smart

links:
- icon: twitter
  icon_pack: fab
  name: Follow
  url: https://twitter.com/itsmekhallu
url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: example
---

[Cows and Bulls](https://en.wikipedia.org/wiki/Bulls_and_Cows) is a code breaker game where the player has to guess a 4 digit code. In this case I have 4 letter words, this makes playing for humans much more than random guessing and some strategy is required. I have switched cows and bulls compared to wiki definition, but concept remains same.

GUI
===

Solver
------

In this tab the human is the game host, he holds the secret 4 letter word while the computer guesses. User has to provide how many cows and bulls the guess has.

{{< figure src="images/cnb_solver.png" title="Cows and Bulls Solver" >}}

Ofcourse, a computer crunching numbers is rather uninteresting, so I have a Data page to track how the program is pruning number of availabe guesses. The guesser had two algorithms, Simple and Advanced:

* Simple - The next guess is naively selected without any preprocessing. This is fast in processing each step but might take longer.

* Advanced - The next guess here is selected such that it reduces the remaining choices. Each current valid guess is evaluated and scored according to the number of choices it can eliminate. Best scoring guess if put forward to the user.

{{< figure src="images/cnb_graph.png" title="Cows and Bulls Graph" >}}

English language has around 2000 valid 4 letter words, each guess more than halves the avalanle choices. I notices the program take at max 7 tries regardless of the complexity.


Game
----

In this mode the system is the host and user has to guess the code. The programs provides number of cows and bulls for each guess. All previous guess and corresponding scores are printed for reference.

{{< figure src="images/cnb_game.png" title="Cows and Bulls Game" >}}

{{< figure src="images/cnb_succes.png" title="Game Solved!" >}}

Code
====

Core of the processor is this calcuator. This takes a guess and a chosen code and generates number of cows and bulls.

```python
def score_calc(self, guess, chosen):
	bulls = cows = 0
	for g, c in zip(guess, chosen):
		if g == c:
			cows += 1
		elif g in chosen:
			bulls += 1
	return cows, bulls
```

Thus any code that does not match either cows or bulls is eliminated from the dictionary of choices. Now the question is selecting the chosen code, this depends on the strategy we want to employ.

```python
self.choices = [c for c in self.choices if self.score_calc(c, self.ans) == score]
```

Simple Strategy
---------------
In the simple strategy the chosen code is simply the top most item after elimination. Then repeat till a score of 4 cows is generated and voila! that is the correct guess.

```python
if self.strategyComboBox.currentIndex() == 0 :
	return self.choices[0]
```

Advanced Strategy
-----------------
In advanced strategy instead of selecting the top item, each item is assumed to be the chosen code and evaluated by eliminating the non matchnig codes. This is similar to simple strategy, however this is repeated for all item and the item which produces the smallest eliminated list is chosen for next guess.

```python
if self.strategyComboBox.currentIndex() == 1 :
	max_unique = 0
	max_g = ""
	for g in self.choices:
		results_list = []
		for c in self.choices:
			(cows,bulls) = self.score_calc(g,c)
			results_list.append(str(cows) + str(bulls))
			if len(set(results_list)) < len(results_list):
				break
		if len(set(results_list)) == len(results_list):
			return  g
		elif len(set(results_list)) > max_unique:
			max_unique  = len(set(results_list))
			max_g = g
	return max_g
```
