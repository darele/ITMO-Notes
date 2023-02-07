# Practice 1

# Table of Contents
1. [Part I Classic Probability](#classic-probability)
    - [1.1 Problem 1](#problem-1)
    - [1.2 Problem 2](#problem-2)
    - [1.3 Problem 3](#problem-3)
    - [1.4 Problem 4](#problem-4)
    - [1.5 Problem 5](#problem-5)
    - [1.6 Problem 6](#problem-6)
    - [1.7 Problem 7](#problem-7)
    - [1.8 Problem 8](#problem-8)
    - [1.9 Problem 9](#problem-9)
    - [1.10 Problem 10](#problem-10)
    - [1.2 Problem 6](#problem-6)
2. [PartII Geometrical Probability](#geometrical-probability)
    - [2.1 Problem 12](#problem-12)
    - [2.2 Problem 13](#problem-13)
3. [Homework](#homework)


# Classic Probability

## Problem 1

There are 4 red pencils and 3 blue pencils in a box, whte is the probability of randomly take out 2 red pencils and 2 blue pencils

- ### Solution

    Favorable cases:
    
    $$ m = {4 \choose 2} {3 \choose 2} = \dfrac{4!}{2!2!} \dfrac{3}{2} = 3\times2\times3=18$$

    Total cases:

    $$n = {7 \choose 4} = \dfrac{7!}{3!4!} = 35$$

    Probability:

    $$P(A)=\dfrac{18}{35}$$

## Problem 2

There are 2 white, 3 black and 4 red balls in a box, 5 are taken out, what's the probability that 2 of them are black and 2 red.

- ### Solution

    || White | Black | Red |
    |:---:| :---: | :---: | :---:|
    |There are| 2 | 3 | 4 |
    |Taken out| 1 | 2 | 2 |

    Favorable cases:

    $$m = {3 \choose 2} {4 \choose 2} {2 \choose 1} = 6!\dfrac{4!}{2!2!} = 6\times6 = 36$$

    Total cases:

    $$n = {9 \choose 5} = \dfrac{9\times8\times7\times6}{4!} = 126$$

    Probability:

    $$P(A)=\dfrac{36}{126} = \dfrac{2}{7}$$


## Problem 3

5 Students, 2 architects and 3 robots went on a trip, half of them came back, what is the probability that 3 students, 1 architect and 1 robot came back.

- ### Solution

    Favorable cases:

    $$m = {5 \choose 3} {3 \choose 1} {2 \choose 1} = \dfrac{5!}{3!2!}\dfrac{3!}{2!1!} \times 2 = 6\times6 = 60$$

    Total cases:

    $$n = {10 \choose 5} = \dfrac{10!}{5!5!} = 63\times4=252$$

    Probability:

    $$P(A)=\dfrac{60}{252} = \dfrac{5}{21}$$

    This is true only if all given characters may come back with the same probability, but not all of them may come back with the same probability (limitations of reality :,( )

## Problem 4

Letters 'И' 'П' 'Л' 'А' are given, whta is the probability off getting a correct russian word.

- ### Solution

    Favorable cases:

    $$m = 2$$

    Total cases:

    $$n = 4! = 24$$

    Probability:

    $$P(A)=\dfrac{2}{24} = \dfrac{1}{12}$$

## Problem 5

There are 8 books on a shelf, what's the probability that 3 specific books are arranged consecutively.

- ### Solution

    Favorable cases:

    $$m = 6\times3!\times5!$$

    Here we have 6 possible positions for this three books to be arranged consecutively, 3! possible arrangements of these three books, and 5! possible arrangements for the other 5 books in the shelf.

    Total cases:

    $$n = 8!$$

    Probability:

    $$P(A)=\dfrac{3}{28}$$

 ## Problem 6

There are 5 people in a circular table, What is the probability that 2 specific people sit next to each other

- ### Solution 1

    Favorable cases:

    We have 5 possible seats in which the first person can be seated, and next to them (because the table is circular) there are 2 possible seats for the second person to occupy, and the remaining 3 people can be seated in any place.

    $$m = 5\times2\times3!$$

    Total cases:

    $$n = 5!$$

    Probability:

    $$P(A)=\dfrac{1}{2}$$

- ### Solution 2

    We assume that one of these two people is already seated, then the second person can occupy 4 places, from which 2 of them are favorable, then

    $$P(A) = \dfrac{2}{4}=\dfrac{1}{2}$$

## Problem 7

On the first floor of a 6-stories building 3 people get on the elevator/lift, What is the probability that all of them get out of the elevator/lift on different floors.

- ### Solution

    Favorable cases:

    $$m = A_{5}^{3} = 3 \times 4 \times 5 = 60$$

    Where $A$ is *Placement formula*, which counts all possible accomodation of $k$ objects from a set of $n$ elements and it is equal to.

    $$A_{n}^{k} = \dfrac{n!}{(n - k)!}$$

    Total cases:

    $$n = 5^3 = 125$$

    Probability:

    $$P(A)=\dfrac{60}{125} = \dfrac{12}{25}$$

## Problem 8

There are 8 teams, and they are arranged in 2 groups of 4 teams, What is the probability that the 2 strongest teams will be in different groups

- ### Solution

    Favorable cases:

    $$m = {2 \choose 1}{6 \choose 3} = 2 \times 20 = 40$$

    Total cases:

    $$n = {8\choose 4} = 70$$

    Probability:

    $$P(A)=\dfrac{40}{70}$$

## Problem 9

For a heart game, 2 players have 4 heart cards, what is the probability that the cards are spread in:

a. 2 : 2

b. 1 : 3

c. 0 : 4

- ### Solution

    $$n = 2^4 = 16$$

    c.

    $$m = 2\\ P(A) = \dfrac{2}{16} = \dfrac{1}{8}$$

    In this case, all 4 four cards are given to one player, and there are two of them, then $m = 2$

    b.

    $$m=2\times4 = 8, P(A) = \dfrac{8}{16} = \dfrac{1}{2}$$

    1 out of 4 cards can be given to the first player, and there are 2 players.

    a.

    $$m = {4 \choose 2} = 6, P(A) = \dfrac{3}{8}$$

    2 cards have to be selected to be given to any of the players (the spreadings are symmetric, then by counting the arrangement, say 1,3  for the first player, the second can only be assigned 2,4; and when counting 2,4 for the first player, for the second 1,3 is automatically counted)

## Problem 10

On a chess board, a white and a black rook are placed, What is the probability that they don't kill each other

- ### Solution

    $$n = 64 \times 63
    $$

    One rook is white and the other black, then the order is important

    $$m = 64\times49$$

    We place one rook and consequently, for the second, one row and one column is not available, which leads to a $7\times7$ board.

    $$P(A) = \dfrac{49}{64\times63} = \dfrac{7}{9}$$

## Problem 11

2 dices are thrown, What is the probability that the sum of points at least 9

- ### Solution

    || 1 | 2 | 3 | 4 | 5 | 6 |
    |:---:| :---: | :---: | :---:| :---: | :---: | :---: |
    | **1** | 2 | 3 | 4 | 5 | 6 | 7 |
    | **2** | 3 | 4 | 5 | 6 | 7 | 8 |
    | **3** | 4 | 5 | 6 | 7 | 8 | _**9**_ |
    | **4** | 5 | 6 | 7 | 8 | _**9**_ | **10** |
    | **5** | 6 | 7 | 8 | _**9**_ | _**10**_ | _**11**_ |
    | **6** | 7 | 8 | _**9**_ | _**10**_ | _**11**_ | _**12**_ |

    $$n = 6^2 = 36$$

    Table's size

    $$m = 4 + 3 + 2 + 1 = 10$$

    Look at the italic bold numbers in table

    $$P(A) = \dfrac{5}{18}$$

# Geometrical Probability

## Problem 12

Some trambai has a wating interval of 15 minutes, What is the probability that it is necessary to wait more than 10 minutes.

- ### Solution

    In this case, the set of possible outcomes is uncountable

    $$P(A) = \dfrac{l(A)}{l(\Omega)} = \dfrac{5}{15} = \dfrac{1}{3}$$

    Where $l(x)$ represents the measure (Мера) of the given variable.

## Problem 13

Two people agreed to meet between 12:00 and 13:00, What is the probability that the waiting time will be at most 15 minutes.

- ### Solution

    ![Graph of waiting time correspondence](img/graph%20problem%2012.jpg)

    It is clear that $B_1$ and $B_2$ have the same area, so we just have to substract from the total area of the graph to get the marked area.

    We can see the possible outcome space as the cross product of the both times,

    let $x$ be first person's arriving time in minutes after 12:00, and $y$ for second person.

    <!-- To view in VSCode -->
    <!-- $$\begin{align}
        x &\in [0, 60] \\
        y &\in [0, 60] \\
        \Omega &= [0, 60]\times[0,60]
    \end{align}$$ -->
    
    <!-- To view on Github -->

    $x \in [0, 60]$

    $y \in [0, 60]$

    $\Omega = [0, 60]\times[0,60]$


    Recall from Math analysis semester 3, that integral returns the measure of what's inside it

    $$\int{(\Omega)} = 60 \times 60 = 3600$$

    $$\int{A} = \int {(\Omega)} - 2\int{B} = 60^2 - 45^2  = (60 + 45)(60-45) = 15\times15\times7 = 1575$$

    Everything was computed with basic formulas for area.


## Homework

1. Стержень случайно ломается на 3 части, какова вероятность того, что из них можно будет составить треугольник?

2. В урне 5 белых, 4 черных, 3 красных шара. Вынули половину из них, какова вероятность того, что среди них будет каждого цвета поровну?

3. В коробке 5 красных и 3 синих карандаша. Вынули 5 карандашей, какова вероятность того, что среди них будет не менее 3х красных?

Thanks Andrey
