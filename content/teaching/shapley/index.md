---
title: Understanding Shapley Values and SHAP
summary: An introduction to Shapley values and their applications in explaining ML models.
date: 2025-01-10
type: docs
math: true
tags:
  - Shapley values
  - Machine learning
  - Explainability
  - Interpretability
  - Feature importance
  - Game theory
  - Cooperative games
  - Explainable AI
image:
  caption: 'Image credit: [**University of California**](https://www.universityofcalifornia.edu/news/how-two-matchmakers-won-nobel-prize)'
---

SHAP (SHapley Additive exPlanations) is a unified approach to explain the output of any machine learning model. In other words, it is a model-agnostic method that considers the model as a black box and only access the input and output of the model. It tries to explain the output of the model for a specific instance by computing the contribution of each component of the input to the output. The components can be features/columns in a tabular dataset, a set of pixels in an image, a word/token in a text document, etc. In this article, we first introduce the concept of Shapley values and then explain how SHAP uses Shapley values to explain the predictions of machine learning models. I will also provide some code examples and a list of resources to learn more about this topic.

## Intuition

To be honest, "Shapley Values" is a term that I have been hearing a lot in the literature, but I was afraid to dive into it because it sounded too complex and there wasn't a straightforward explanation of what it is and how it works. Recently, my supervisor shared me an article from [Towards Data Science](https://towardsdatascience.com/introduction-to-shap-values-and-their-application-in-machine-learning-8003718e6827) that explained Shapley values comprehensively and I thought it was time to understand what Shapley values are, once and for all! However, the article was too long (around 120 pages in a PDF format) and I think many people would be discouraged to read it. So, I decided to write a blog post to summarize the key concepts which I learned from until now and share a more straightforward explanation of Shapley values. My explanation may not be as comprehensive (or even accurate) as the original article, but I will try to make it as simple as possible to allow everyone to easily understand this great concept.

## Shapley Values

To understand how Shapley values can explain the predictions of a machine learning model, we first need to understand the concept of [Shapley values](https://en.wikipedia.org/wiki/Shapley_value) which come from [*cooperative game theory*](https://en.wikipedia.org/wiki/Cooperative_game_theory). This mathematical concept introduced by [*Lloyd Shapley*](https://en.wikipedia.org/wiki/Lloyd_Shapley) in 1953 (and he was awarded the *Nobel Prize* in *Economic Sciences* in 2012 for this work) is used to fairly distribute the total gains of a coalition of players in a cooperative game among the players. What do we mean by "coalition of players" and "cooperative game"? Let's break it down with an example.

### Example

Imagine that you gathered some of your friends to record an album together. Some of them are good at playing an instrument, some in singing, some in mixing, some may be helpful in providing recording equipment, marketing, etc. Each of them has a different role in the process of recording and releasing the album. When the album is released, it will generate some revenue. Let's say that the album is a hit and it generates €100,000 in revenue. Now, the question is: how should we distribute this revenue among the friends who contributed to the album? Yes, you can distribute it equally among all friends, but is it fair? Should the friend who played the drums get the same share as the friend who provided the recording equipment? Each friend had an impact on the success of the album, but their contributions are different. This is where Shapley values come into play.

## Definitions

Imagine we have $M$ playes (numbered from 1 to $M$) and let $F$ be the set of all players ($F = \{1, 2, \ldots, M\}$). A **coalition** is a subset of players $S \subseteq F$ which can be any combination of players. The set $F$ itself is also a coalition, which commonly referred to as the **grand coalition**. We can have $2^M$ possible coalitions in total (the empty set $\emptyset$ is also a coalition that has no players).

The **worth** of a coalition is a real number that represents the total gains that the coalition can achieve and it is denoted by $v(S)$ for a coalition $S$. Note that $v$ is a function that takes a coalition as input and returns a real number as output, and commonly referred to as the **characteristic function** of the game. The worth of the grand coalition is the total gains that all players can achieve together, i.e., $v(F)$. The worth of the empty set is zero, i.e., $v(\emptyset) = 0$. The worth of a coalition can be calculated in different ways depending on the game. For example, in our album example, the worth of a coalition can be the revenue generated by the album when the friends in the coalition work together. 

### Marginal Contribution of a Player

Now the question is how we can compute the contribution of a player to the total gains of a coalition. Suppose that we have the following table and we assigned a number to each player.

| Player Name | Player Number | 
| :---: | :---: | 
| $Thom$ | $1$ |  
| $Colin$ | $2$ |
| $Jonny$ | $3$ |
| $Ed$ | $4$ |
| $Phil$ | $5$ |
| $Nigel$ | $6$ | 

Let's say we start with the empty set and add players one by one to form a coalition until we reach the grand coalition. For example, we can start with the empty set $\emptyset$ and add $Thom$ to form the coalition $\{1\}$, then add $Colin$ to form the coalition $\{1, 2\}$, and we continue this process until we reach the grand coalition $\{1, 2, 3, 4, 5, 6\}$. The total gain increases as we add more players to the coalition. Suppose the current coalition is ${1, 2, 3}$ and we want to add player $4$ to the coalition. Now, what is the marginal contribution of player $4$ to the total gains of the coalition $\{1, 2, 3, 4\}$? We can simply calculate the total gains of the coalition $\{1, 2, 3, 4\}$ and subtract the total gains of the coalition $\{1, 2, 3\}$ from it. This difference is the contribution of player $4$.

$$ \text{Marginal Contribution of Player 4} = v(\{1, 2, 3, 4\}) - v(\{1, 2, 3\}) $$

{{% callout note %}}

Order of adding players to the coalition is important! Suppose $Thom$ ($1$) have started the band and recorded some songs. However, when $Colin$ ($2$) joined the band, they re-recorded some songs and their revenue increased by €10,000 (which is the contribution of $Colin$). Now, when $Jonny$ ($3$) joined the band, they re-recorded some songs again and their revenue increased by just €2,000. However, $Jonny$ feels unfair when comparing his contribution to $Colin$'s contribution. He believes that if he had joined the band before $Colin$, the revenue would have also increased by €10,000. So, we need to consider all possible orders of adding players to the coalition to calculate the contribution of a player fairly.

{{% /callout %}}



### Expected Marginal Contribution / Shapley Value

We've seen how we can calculate the contribution of a player to the total gains of a specific coalition. However, as we mentioned earlier, the contribution of a player depends on the order of adding players to the coalition and we need to consider all possible orders. To do this, we compute the marginal contribution of a player for all possible permutations of players ($F$) and take the average of these contributions. This **Expected Marginal Contribution** is called the **Shapley value** of the player. As we will have $|F|!$ permutations in total, the Shapley value of player $i$, denoted by $\phi_i$, can be calculated as follows:

$$ \phi_i = \frac{1}{|F|!} \sum_{p \in P} \left( v(S \cup \{i\}) - v(S) \right) $$

In this formula, $P$ is the set of all permutations of players, and $S$ is the coalition related to the permutation $p \in P$. The following table shows how we can calculate the Shapley value of player $4$ for each permutation of players.

| Permutation | Marginal Contribution of Player 4 |
| :---: | :---: |
| $[1, 2, 3, 4, 5, 6]$ |  $v(\{1, 2, 3, 4\}) - v(\{1, 2, 3\})$ |
| $[2, 1, 3, 4, 5, 6]$ |  $v(\{1, 2, 3, 4\}) - v(\{1, 2, 3\})$ |
| $[3, 2, 1, 4, 5, 6]$ |  $v(\{1, 2, 3, 4\}) - v(\{1, 2, 3\})$ |
| $\vdots$ | $\vdots$ |
| $[4, 1, 2, 3, 5, 6]$ | $v(\{4\}) - v(\emptyset)$ |
| $\vdots$ | $\vdots$ |
| $[6, 5, 4, 3, 2, 1]$ | $v(\{4, 5, 6\}) - v(\{5, 6\})$ |


{{% callout note %}}

The characteristic function $v$ takes a coalition/set as input, not a permutation. This is because the worth of a coalition is independent of the order of players in the coalition. The worth of the coalition of $Thom$ and $Colin$ is the same as the coalition of $Colin$ and $Thom$. 

{{% /callout %}}

Now, we take the average of these contributions to calculate the Shapley value of player $4$. As we can see, some permutations have the same marginal contribution since their coalitions are the same. So, why don't we make it simpler and only calculate the distinct values of contributions and multiply them by the number of times they have been repeated in the permutations?

To do this, we need to find how many permutations can be formed from each coalition. If you look at the table above, you can see that the term $v(\{1, 2, 3, 4\}) - v(\{1, 2, 3\})$ is repeated for all permutations that the player $4$ is added after the players $1$, $2$, and $3$. So, if $S=\{1, 2, 3\}$, the player $4$ can be added after theses players in $|S|! = 3! = 6$ different ways. Furthermore, the remaining players can be added to the coalition in $(|F|-|S|-1)! = (6-3-1)! = 2!$ different ways. So, the Shapley value of player $4$ can be calculated as follows:

$$ \phi_i = \sum_{S \subseteq F \setminus \{i\}} \frac{|S|! \cdot (|F|-|S|-1)!}{|F|!} \left( v(S \cup \{i\}) - v(S) \right) $$

## Axioms of Shapley Values

Shapley values have some provable properties that make them unique and fair. This is because of these *axioms* that Shapley values are mathematically strong and widely accepted. The axioms of Shapley values are as follows:

### 🎯 Efficiency

The sum of Shapley values of all players should be equal to the total gains of the grand coalition. In other words, if we sum the Shapley values of all players, it should be equal to the worth of the case where all players work together.

$$ \sum_{i=1}^{|F|} \phi_i = v(F) $$

### ⚖️ Symmetry

If two players have the same contribution to every possible coalition, their Shapley values should be the same. 

$$ \text{If } v(S \cup \{i\}) = v(S \cup \{j\}) \text{ for all } S \subseteq F \setminus \{i, j\}, \text{ then } \phi_i = \phi_j $$

### ⭕ Dummy/Null Player

If a player has no contribution to any coalition, its Shapley value should be zero.

$$ \text{If } v(S \cup \{i\}) = v(S) \text{ for all } S \subseteq F \setminus \{i\}, \text{ then } \phi_i = 0 $$

### ➕ Additivity

If we have two games (or two characteristic functions) and we calculate the Shapley values of players for each game separately, the Shapley value of a player in the combined game should be the sum of the Shapley values of the player in each game. This axiom is based on the assumption that any game played are independent of each other.

$$ \phi_i(u+v) = \phi_i(u) + \phi_i(v) $$

## SHAP

To be continued...

## 🗂️ Resources

### 📰 Blog Posts

* [Introduction to SHAP Values and their Application in Machine Learning](https://towardsdatascience.com/introduction-to-shap-values-and-their-application-in-machine-learning-8003718e6827) by *Reza Bagheri* on *Towards Data Science*

* [Understanding Shapley value explanation algorithms for trees](https://hughchen.github.io/its_blog/index.html) by *Hugh Chen*, "Scott Lundberg", and "Su-In Lee" on *GitHub*

### 🎞️ Videos

* [SHAP playlist](https://youtube.com/playlist?list=PLqDyyww9y-1SJgMw92x90qPYpHgahDLIK&si=2VsAcTTC7GoZc-YC) by *A Data Odyssey* on *YouTube*