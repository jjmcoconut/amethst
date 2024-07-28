# 1. Introduction

## 1-1 TCP Backoff

__Game Theory__
Way of thinking about strategic interactions btw self-interested people.

__TCP Behavior__
1. TCP drops packets if the queue is full.
2. The sender does not get the ACK
3. Sender resends the message at a lower rate until it does not drop packets

__SO should we__
- Send packets using correctly implemented TCP(using backoff)
- Implement a defective algorithm for sending(Most likely to burst)

Suppose there are only 2 people using the line -> Two-player game
- Both use correct implementation: both 1ms delay
- One correct, one defective: 4ms for correct, 0ms for defective
- Both defective: both 3ms delay

## 1-2 Self-Interested Agents and Utility Theory

__Self-Interested Agents?__
- Agents has its own description of states of the world that it likes, acts based on this description
- Each such agent has a utility function
	- Quantifies degree of preference across alternatives
	- Explains the impact of uncertainty
	- Decision-theoretic rationality: act to maximize expected utility.

## 1-3 Game Theory Definition

__Key Ingredients__
- Players: Decision Makers
- Actions: Players' behavior
- Payoffs: Players' motivation

__2 standard Representations__
- Normal form: List payoffs as a function of their actions
- Extensive form: Includes timing of moves(e.g. Chess)
	- Timing, Information

__Normal form__
- $<N,A,\mu>$: Finite n-person normal game
	- Players: $N$
	- Action set for player $i$: $A_i$
	- Utility function for player $i$: $u_i: A_i \rightarrow \mathbb{R}$ 
- TCP backoff game matrix

|       | C      | D      |
| ----- | ------ | ------ |
| __C__ | -1, -1 | -4, 0  |
| __D__ | 0, -4  | -3, -3 |
- Large collective action game
	- Players: $N=\{1,\cdots,10000\}$
	- Action set for player $i$: $A_i = \{Revolt,Not\}$
	- Utility function for player $i$:
		- $$\begin{aligned}
		  u_i(a)=1 &\text{ if } \#\{ j:a_j=Revolt \}\geq 20000 \\
		  u_i(a)=-1 &\text{ if } \#\{ j:a_j=Revolt \}< 20000 \text{ and } a_i=Revolt\\
		  u_i(a)=0 &\text{ if } \#\{ j:a_j=Revolt \}< 20000 \text{ and } a_i=Not
		  \end{aligned}$$

## 1-4 Game Example

__Prisioner's Dilemma__

|     | C    | D    |
| --- | ---- | ---- |
| C   | a, a | b, c |
| D   | c, b | d,d  |
Is any game with $c>a>d>b$

__Games of pure competition__
- Players have exactly opposed interests
- Must be 2 players
- For all action $a \in A, u_1(a)+u_2(a)=c$  for some constant $c$

__Games of cooperation__
- Players have exactly same interests
- no conflict: all players want the same things
	- $\forall a \in A, \forall i,j,u_i(a)=u_j(a)$

## 1-5 Nash Equilibrium

__Keynes Beauty Contest Game__
- Each player names an integer btw 1 and 100
- The player who names the integer closest to two thirds of the average integer wins.

## 1-6 Strategic Reasoning

__Keynes Beauty Contest Game__
- What will other players do?
- What should I do in response?
- Each player takes the best response to others: _Nash equilibrium_

__Flow__
- Suppose the average will be _X_
- _X_ is no less than 100, the optimal strategy to announce less than 67
- If _X_ is less than 67 then the optimal strategy of any player is to write less than 45.
- Continues ...
- Everyone should pick 1 and get a $1/N$ chance to win

__Actually...__
- Mean 34, mode 50, Median 33, Winner 23
- Because people do not understand the problem well...

Why should we expect equilibria to be played?
- We expect the non-equilibria not to be stable. The players should move away from that state.