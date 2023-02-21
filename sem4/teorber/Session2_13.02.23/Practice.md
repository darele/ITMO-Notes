# Practice 2

# Table of Contents
1. [Computation of probability by complement and Inclusion-Exclusion principle](#computation-of-probability-by-complement-and-inclusion-exclusion-principle)
    - [1.1 Problem 1](#problem-1)
    - [1.2 Problem 2](#problem-2)
    - [1.3 Problem 3](#problem-3)
    - [1.4 Problem 4](#problem-4)
    - [1.5 Problem 5](#problem-5)
    - [1.6 Problem 6](#problem-6)
    - [1.7 Problem 7](#problem-7)
2. [Homework](#homework)


# Computation of probability by complement and Inclusion-Exclusion principle

## Problem 1

A coin is thrown 10 times, what is the probability of getting heads at least once?

- ### Solution

    Instead of computing all possible cases, let's compute the complement of the opposite outcome (that we get no heads, in other words, getting always tails)

    Probability:

    $$P(A)=1 - \left(\dfrac{1}{2}\right)^{10}$$

[Back to top](#practice-2)

## Problem 2

A coin is thrown twice, What is ithe probability of getting exactly once heads?

- ### Solution

    $$P(HT + TH) = \dfrac{1}{2} \cdot \dfrac{1}{2} + \dfrac{1}{2} \cdot \dfrac{1}{2} = \dfrac{1}{2}$$

[Back to top](#practice-2)

## Problem 3

Two guns fire to a target, the probability of the first one of hitting the target is $0.8$ for the second one is $0.6$, what is the probability that

- a) They both hit the target

- b) Only one hit the target

- c) at least one hit the target

- ### Solution

    $$ P(A_1) = 0.8 \rightarrow P(\overline{A}) = 0.2$$
    $$ P(A_2) = 0.6 \rightarrow P(\overline{A}) = 0.4$$

    - a) 
    $$A=A_1A_2$$
    $$P(A) = P(A_1)P(A_2) = 0.8*0.6=0.48$$

    - b)
    $$B = A_1\overline{A_2} + A_2\overline{A_1}$$
    $$P(B) = P(A_1)P(\overline{A_2}) + P(A_2)P(\overline{A_1}) = 0.8 \cdot 0.4 + 0.6\cdot 0.2 = 0.44$$

    - c)
    Let $C - $ outcome: At least one hit the target

    Let $\overline{C} - $ outcome: No gun hit the target

    $$\overline{C} = \overline{A_1}\cdot \overline{A_2}$$
    $$P(\overline{C}) = P(\overline{A_1})\cdot P(\overline{A_2}) = 0.08$$
    $$P(C) = 1 - P(\overline{C}) = 1 - 0.08 = 0.92$$

[Back to top](#practice-2)

## Problem 4

There are three witnesses, the first one can lie with a probability of $5\%$, the second with $10\%$, and the third with $20\%$, they all testified, what is the probability that.

- a) there were 3 truths (no one lied)

    ### Solution

    $$A = \overline{A_1} \cdot \overline{A_2} \cdot \overline{A_3}$$
    $$A = 0.95 \cdot 0.9 \cdot 0.8 = 0.684$$

- b) 2 of them said the truth

    ### Solution

    $$B = \overline{A_1} \cdot \overline{A_2} \cdot A_3 + \overline{A_1} \cdot A_2 \cdot \overline{A_3} + A_1 \cdot \overline{A_2} \cdot \overline{A_3}$$
    $$B = 0.95\cdot 0.9 \cdot 0.2 + 0.95\cdot 0.1 \cdot 0.8 + 0.05\cdot 0.9 \cdot 0.8$$

- c) At least one of them said the truth

    ### Solution

    $$C = 1 - (A_1 \cdot A_2 \cdot A_3)$$
    $$B = 0.95\cdot 0.1 \cdot 0.2$$

[Back to top](#practice-2)

## Problem 5

$n$ places are assigned to n passengers on an airplane, the first passeger sits on any place, all the next passengers sit on their place if it is free, or in a random place otherwise, what is the probability that the last passenger sits on their place.

- ### Solution

    The only two possible free seats for the last passenger are theirs, or the first passenger's seat, therefore the probability is $\dfrac{1}{2}$

[Back to top](#practice-2)

 ## Problem 6

What is the probability for electric current to flow on the following diagram.

![!Circuit scheme](img/electric%20scheme.png)

where the numbers in the components represent the probability of the given component to work.

- ### Solution

    Let $A_i$ event "Current flows through component $A_i$" for $i \in [1, 5]$ numbered from left to right and top to bottom

    Let $B_1$ - Current flow through the top line and $B_2$ - Curent flow through the bottom line

    Let C - Current flow in the diagram (no matter through which line it flows).

    $$P(A_1) = 0.5$$
    $$P(A_2) = 0.8$$
    $$P(A_3) = 0.5$$
    $$P(A_4) = 0.6$$
    $$P(A_5) = 0.8$$
    $$P(B_1) = P(A_1)\cdot P(A_2) = 0.9 \cdot 0.8 = 0.92$$
    $$P(B_2) = P(A_3)\cdot P(A_4) \cdot P(A_5) = 0.5 \cdot 0.6 \cdot 0.8 = 0.24$$

    $$C = B_1 + B_2$$
    $$P(C) = P(B_1) + P(B_2) - P(B_1B_2) = 0.72 + 0.24 - 0.72 \cdot 0.24 = 0.7872$$

[Back to top](#practice-2)

## Problem 7

2 Players threw a coin $n$ times, the first one threw it one more time, what is the probability that the first player got more points than the second one

- ### Solution

    Let $V_a$ - first player's points after $n$ tries

    Let $V_b$ - second player's points after $n$ tries

    Let's take a look at the probaility scheme.

    $$P(V_a \gt V_b) + P(V_a \lt V_b) + P(V_a = V_b) = 1$$

    Let $C$ - Player 1 gets more points, we are interested in the outcomes $V_a \gt V_b$, and $V_a = V_b$

    $$C = \lbrace V_a \gt V_b \rbrace + \lbrace V_a = V_b, H \rbrace$$

    Observe that $P(V_a \gt V_b)$ is equally probable as $P(V_b \lt V_b)$, then, let's denote $P(V_a = V_b)$ as $P_0$, we get.

    $$2P(V_a > V_b) = 1 - P_0 \Rightarrow P(V_a > V_b) = \dfrac{1 - P_0}{2}$$

    $$P(C) = P(V_a > V_b) + P(V_a = V_b)\cdot P(H)$$
    $$P(C) = \dfrac{1 - P_0}{2} + \dfrac{P_0}{2} = \dfrac{1}{2}$$

[Back to top](#practice-2)

## Homework

1) 3 орудия стреляют 2 раза по цели. Вероятность попадания 1 орудия 0,8, второго 0,7, третьего 0,5. Какова вероятность что

    - А) все попадут в цель
    - Б) Ровно две попадут в цель
    - В) хотя бы одна попадёт в цель

2) Какова вероятность того, что ток пройдёт через электрическую цепь

![electric scheme](img/homework%20task2.jpg)

3) n человек наугад надели n шляп. Вероятность потерять шляпу по дороге равна p. Какова вероятность того, что никто не придёт домой в своей шляпе и куда стремится эта вероятность?

[Back to top](#practice-2)