---
layout: post
title: "How to estimate the number of tournament competitors?"
category: Math
tags: ["clash royale", "tournament", "julia"]
date: 2019-02-16
comments: true

---

>**Summary**:
- I have achieved 13 wins in the world tournament of Clash Royale recently.
  I am curious about how is my skill level among all competitors.
  So, I write some code to simulate win/lose in a game's tournament.

- There are 1v1 tournament/challenge modes in games like Clash Royale:
  - :mag: Player can enter a Challenge and battle in this Challenge.
  - :mag: The player will be matched with another player who has the same number of wins.
  - :mag: Once the player gets the certain number of wins or certain number losses, the Challenge will end.
  - :mag: If the two players are tied, then there is no win or lose cumulation.

- In classic challenge or grand challenge, ending condition is 12 wins and 3 losses.
  In the latest world tournament, ending condition is 5 losses(no wins limit).
  The following is my Julia code of estimating the number of players in the world tournament.
  ```julia
  using Printf

  max_wins = 38
  max_losses = 5
  num_player = 65000000

  mutable struct 𝐒
    wins:: Int
    losses:: Int
    count_player:: Int
  end

  T = [𝐒(i, j, 0) for i = 0:max_wins for j = 0:max_losses if !(i == max_wins && j == max_losses)]

  add(A, w, l, c) = (A[w * (max_losses + 1) + l + 1].count_player += c)

  add(T, 0, 0, num_player)
  for t in T
    if t.wins != max_wins && t.losses != max_losses
      (w, rem) = divrem(t.count_player, 2)
      t.count_player = rem

      add(T, t.wins+1, t.losses, w)
      add(T, t.wins, t.losses+1, w)
    end
  end

  Counts = Dict(i => 0 for i = 0:max_wins)
  for t in T
    Counts[t.wins] += t.count_player
  end
  sum = 0
  for i in sort(collect(keys(Counts)))
    global sum
    @printf("%3d wins, %8d players. ", i , Counts[i])
    @printf("[top %10.6f%%]\n", (1-sum/num_player)*100)
    sum+=Counts[i]
  end
  ```
  The best player got 37 wins, so I set ``max_wins`` to 38 and set ``max_losses`` to 5.
  Then adjust ``num_player`` to approach the actual ranking situation.
  The player is matched who has same wins as well as losses in my algorithm.
  Thus some player who has same wins but different losses won't be matched finally.
  These numbers will be very small. So we can just ignore it.
  Here is my output:
  ```text
   0 wins,  2031250 players. [top 100.000000%]
   1 wins,  5078125 players. [top  96.875000%]
   2 wins,  7617188 players. [top  89.062500%]
   3 wins,  8886719 players. [top  77.343749%]
   4 wins,  8886720 players. [top  63.671874%]
   5 wins,  7998047 players. [top  49.999997%]
   6 wins,  6665041 players. [top  37.695309%]
   7 wins,  5236818 players. [top  27.441400%]
   8 wins,  3927614 players. [top  19.384757%]
   9 wins,  2836610 players. [top  13.342274%]
  10 wins,  1985626 players. [top   8.978258%]
  11 wins,  1353835 players. [top   5.923449%]
  12 wins,   902557 players. [top   3.840626%]
  13 wins,   590134 players. [top   2.452077%]
  14 wins,   379372 players. [top   1.544178%]
  15 wins,   240270 players. [top   0.960529%]
  16 wins,   150168 players. [top   0.590883%]
  17 wins,    92752 players. [top   0.359855%]
  18 wins,    56681 players. [top   0.217160%]
  19 wins,    34308 players. [top   0.129958%]
  20 wins,    20583 players. [top   0.077177%]
  21 wins,    12253 players. [top   0.045511%]
  22 wins,     7239 players. [top   0.026660%]
  23 wins,     4249 players. [top   0.015523%]
  24 wins,     2479 players. [top   0.008986%]
  25 wins,     1439 players. [top   0.005172%]
  26 wins,      828 players. [top   0.002958%]
  27 wins,      475 players. [top   0.001685%]
  28 wins,      271 players. [top   0.000954%]
  29 wins,      154 players. [top   0.000537%]
  30 wins,       87 players. [top   0.000300%]
  31 wins,       49 players. [top   0.000166%]
  32 wins,       28 players. [top   0.000091%]
  33 wins,       15 players. [top   0.000048%]
  34 wins,        8 players. [top   0.000025%]
  35 wins,        5 players. [top   0.000012%]
  36 wins,        2 players. [top   0.000005%]
  37 wins,        1 players. [top   0.000002%]
  38 wins,        0 players. [top   0.000000%]
  ```
  Actual total number of players will be more than the results above.
  For example, many players might not use all of the chances.
  If we want classic challenge simulation, we can just modify ``max_wins`` and ``max_losses``.
  Here is my output with ``max_wins = 12``, ``max_losses=3``, ``num_player = 10000000``:
  ```text
   0 wins,  1250000 players. [top 100.000000%]
   1 wins,  1875000 players. [top  87.500000%]
   2 wins,  1875000 players. [top  68.750000%]
   3 wins,  1562500 players. [top  50.000000%]
   4 wins,  1171875 players. [top  34.375000%]
   5 wins,   820313 players. [top  22.656250%]
   6 wins,   546876 players. [top  14.453120%]
   7 wins,   351564 players. [top   8.984360%]
   8 wins,   219726 players. [top   5.468720%]
   9 wins,   134278 players. [top   3.271460%]
  10 wins,    80567 players. [top   1.928680%]
  11 wins,    47607 players. [top   1.123010%]
  12 wins,    64694 players. [top   0.646940%]
  ```
