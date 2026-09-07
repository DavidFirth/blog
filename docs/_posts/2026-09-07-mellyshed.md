---
slug: mellyshed
title: Schedules for 'perfectly social' pétanque club mêlée competitions
categories:
- Pétanque
---

I play pétanque, the French boules game. This year I have enjoyed playing in a few 'mêlée' competitions, where players enter as individuals and are assigned playing partners and opponents at random in each round of the competition.  Typically there are between 3 and 6 rounds in a mêlée, and it is fun to meet and compete with a lot of different people during the course of the competition. At the end, individuals are ranked according to their own aggregated results across the games they have played, and usually there is a prize for the highest-ranked player.

In the competitions where I have played, I found that I was sometimes meeting the same person twice (either as partner or opponent or both).  It struck me that this could be avoided by using a suitably designed schedule for the competition, while still keeping things nicely random.  The purpose of this post is to provide such schedules.

The mêlée competitions I have entered had mainly doubles games (random pair versus random pair), with an occasional hybrid game (random pair versus random triple) when the total number of players entered is not a multiple of 4.  I will focus here on competitions of that kind.  (There will be just one exception below, which is the schedule for a 3-round mêlée with just 6 players.)

# 1. Randomization

I will use the letter _n_ to denote the total number of players entering the competition.

For each of the competition schedules discussed below, randomization comes from the initial assignment of a random competitor-number to each player who enters. If players are pre-registered, then a transparent method for this is to ask each player to draw a random number (on a folded piece of paper or whatever) from a hat. That method might be inconvenient when _n_ is unknown until the very last moment (as often seems to happen), in which case the assignment of pseudo-random numbers by a computer is likely to be more convenient.


# 2. 'Perfectly social' schedules (_n_=16, or _n_ at least 20).

I will call a schedule 'perfectly social' if no player meets any other more than once (either as partner or opponent) across all rounds played.  It turns out that such a schedule, with at least 3 rounds, is possible only when _n_ is either 16 or at least 20.  No such schedule is possible when $n$ is less than 16, nor when _n_ is 17, 18 or 19.

The starting-point for the schedules that I provide here is recent work by Prof. Alice Miller's research group at the University of Glasgow, on the 'social golfer problem':

> Miller, A, Valkov, I and Abel, RJR (2026). Combinatorial solutions to the social golfer problem and the social golfer problem with adjacent group sizes. _Symmetry_, **18**(2), 269. [doi: 10.3390/sym18020269](https://doi.org/10.3390/sym18020269)

That work is accompanied by an online tool, [BoRAT](https://alicemiller2.github.io/borat_git_pages), and it is the output from that tool that I adapt here for pétanque mêlée competitions with 'mainly pairs' games.  The adaptations needed are all connected with the inclusion of one or more triples teams when _n_ is not a multiple of 4 --- in particular, to adjust each schedule so that individual players do not appear in a triple more often than is necessary. My schedules allow for a maximum of 6 rounds of play.

I will tabulate here some properties of each schedule, up to _n_=67 players.  (My club has 16 pistes, so 67 is the largest number of players that can be accommodated there without including some triple-versus-triple games.)  The properties tabulated are: 

- the number of pistes required 
- the number _Rmax_ of 'perfectly social' rounds possible (up to 6)
- the largest number of times _Tmax_ that any player appears in a triple. 

Where _Tmax_ is "2*" in the table it means that _Tmax_ is reduced to 1 if five rounds or fewer are used.


| _n_ | _pistes_| _Rmax_ | _Tmax_ |
|-----:|---------:|--------:|-------:|
| 16  |   4| 5 | 0 |
| 20  |   5| 5 | 0 |
| 21  |   5| 5 | 1 |
| 22  |   5| 5 | 2 |
| 23  |   5| 5 | 2 |
| 24  |   6| 6 | 0 |
| 25  |   6| 5 | 1 |
| 26  |   6| 5 | 1 |
| 27  |   6| 5 | 2 |
| 28  |   7| 6 | 0 |
| 29  |   7| " | 1 |
| 30  |   7| " | 2 |
| 31  |   7| " | 2 |
| 32  |   8| " | 0 |
| 33  |   8| " | 1 |
| 34  |   8| " | 2 |
| 35  |   8| " | 2 |
| 36  |   9| " | 0 |
| 37  |   9| " | 1 |
| 38  |   9| " | 2* |
| 39  |   9| " | 2 |
| 40  |  10| " | 0 |
| 41  |  10| " | 1 |
| 42  |  10| " | 1 |
| 43  |  10| " | 2 |
| 44  |  11| " | 0 |
| 45  |  11| " | 1 |
| 46  |  11| " | 2* |
| 47  |  11| " | 2 |
| 48  |  12| " | 0 |
| 49  |  12| " | 1 |
| 50  |  12| " | 1 |
| 51  |  12| " | 2 |
| 52  |  13| " | 0 |
| 53  |  13| " | 1 |
| 54  |  13| " | 2* |
| 55  |  13| " | 2 |
| 56  |  14| " | 0 |
| 57  |  14| " | 1 |
| 58  |  14| " | 1 |
| 59  |  14| " | 2 |
| 60  |  15| " | 0 |
| 61  |  15| " | 1 |
| 62  |  15| " | 1 |
| 63  |  15| " | 2 |
| 64  |  16| " | 0 |
| 65  |  16| " | 1 |
| 66  |  16| " | 1 |
| 67  |  16| " | 2 |

# 3. _Almost_ perfectly social (_n_ = 8, 12, 13, 14, 15, 17, 18, 19)

In these schedules, no player partners any other more than once, and no player opposes any other more than once.

| _n_ | _pistes_| _Rmax_ | _Tmax_ |
|-----:|---------:|--------:|-------:|
|  8  |  2| 3 | 0 |
| 12  |  3| 3 | 0 |
| 13  |  3| 3 | 3 |
| 14  |  3| 3 | 3 |
| 15  |  3| 3 | 3 |
| 17  |  4| 4 | 2 |
| 18  |  4| 4 | 3* |
| 19  |  4| 4 | 4 |

Where _Tmax_ is "3*" in the table it means that _Tmax_ is reduced to 2 if only three rounds are played.

# 4. When there are just 6 players

When only 6 players turn up, a mêlée can still be played but obviously the games are triple-versus-triple.

The 4-round schedule that is provided for a 6-player mêlée has the property that each player partners 4 of the other players twice, and does not partner the remaining player at all. (Potentially useful when the 6 players arrive as 3 couples?  It can then be arranged that players in a couple are never in the same team.)

# 5. Downloading the schedules

The full set of schedules described above can be downloaded as a single zip file at [mellyshed.zip](/blog/assets/mellyshed.zip).  The files are human-readable Python code (with player numbers starting always at zero.)  I can easily export the schedules to other formats: if you have a need for a different format, then please specify exactly what format and I will try to make that available.


**To cite this entry:**
Firth, D (2026).  Schedules for 'perfectly social' pétanque club mêlée competitions.  Weblog entry at URL
[https://DavidFirth.github.io/blog/2026/09/07/mellyshed/](/blog/2026/09/07/mellyshed/)

