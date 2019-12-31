---
layout: post
title: Dynamic Programming
prev: Markov Decision Process
prev-url: /reinforcementLearning/markovDecisionProcess.html
next: Monte Carlo Methods
next-url: /reinforcementLearning/monteCarloMethods.html
---
Dynamic Programming is one of the methods to find the optimal policy. Dynamic Programming
* uses bootstrapping, which means it updates estimated values using other estimated values
* requires complete knownledge of the environment including transition probabilities $$\mathcal{P}$$

## Policy Evaluation
Policy evaluation finds the state value function of a policy $$\pi$$ by applying the Bellman Equation iteratively until the largest change in value function between two iteration steps is below a predetermined threshold $\epsilon$.
```
$\boldsymbol{Policy\;Evaluation}$

Repeat:
	$\Delta \leftarrow 0$
	For $s \in \mathcal{S}$:
		$v \leftarrow v(s)$
		$v(s) \leftarrow \sum_a \pi(s,a)q_\pi(s,a)$
		$\Delta \leftarrow max(\Delta,|v-v(s)|)$
Until $\Delta \lt \epsilon$
```
## Policy Improvement
Following the same policy $\pi$ will always return the same value function. We want to consider the value of selecting a different action $a$ at state $s$ and there after follow the existing policy $\pi$. If the value is greater, then it is better to select $a$ once in state $s$ than to follow the $\pi$ all the time. 
```
$\boldsymbol{Policy\;Improvement}$

$policyStable \leftarrow True$
For $s \in \mathcal{S}$:
	$a \leftarrow \pi(s)$
	$\pi(s) \leftarrow \arg\max_a q_\pi(s,a)$
	If $a \neq \pi(s)$:
		$policyStable \leftarrow False$
```
## Policy Control
Policy control finds the best policy to maximise the value function.
### Policy Iteration Algorithm
Policy Iteration Algorithm alternates between Policy Evaluation and Policy Improvement until we obtain the optimal policy.
```
$\boldsymbol{Policy\;Iteration}$

$\forall s\in \mathcal{S}: v(s) \leftarrow 0$
$\forall s \in \mathcal{S}: \pi(s) \leftarrow$ random $\mathcal{A}(s)$
Repeat:
	$\boldsymbol{Policy\;Evaluation}$
	$\boldsymbol{Policy\;Improvement}$
Until $policyStable$
```
### Value Iteration Algorithm
Value Iteration Algorithm combines Policy Evaluation and Policy Improvement into one step.
```
$\boldsymbol{Value\;Iteration}$

$\forall s\in \mathcal{S}: v(s) \leftarrow 0$
Repeat:
	$\Delta \leftarrow 0$
	For $s \in \mathcal{S}$:
		$v \leftarrow v(s)$
		$v(s) \leftarrow \max_a q_\pi(s,a)$
		$\Delta \leftarrow max(\Delta,|v-v(s)|)$
Until $\Delta \lt \epsilon$
For $s \in \mathcal{S}$:
	$\pi(s) \leftarrow \arg\max_a q_\pi(s,a)$
```