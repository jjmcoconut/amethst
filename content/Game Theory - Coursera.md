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

Prisioner's Dilemma