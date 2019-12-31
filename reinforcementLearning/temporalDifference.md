---
layout: post
title: Temporal Difference
prev: Monte Carlo Method
prev-url: /reinforcementLearning/monteCarloMethods.html
---
Temporal Difference is one of the methods to find the optimal policy. Temporal Difference
* uses sampling so does not require prior knowledge of the environment $\mathcal{P}$
* uses bootstrapping so can learn from incomplete episodes

## Policy Evaluation
[Monte Carlo Methods](./monteCarloMethods.html) updates q-values based on the actual observed return.

$$
q_\pi(s,a) \leftarrow q_\pi(s,a) + \alpha(\mathcal{G} - q_\pi(s,a))
$$

Temporal Difference updates q-values based on the estimated return.

$$
q_\pi(s,a) \leftarrow q_\pi(s,a) + \alpha\left(\mathcal{R} + \gamma q_\pi(s',a') - q_\pi(s,a)\right)
$$

```
$\boldsymbol{TD\;Policy\;Evaluation}$

$\forall s\in \mathcal{S},a\in\mathcal{A}: q_\pi(s,a) \leftarrow 0$
Repeat $1\dots n$:
	$s \leftarrow$ starting state
	$a \leftarrow \pi(s)$
	Repeat:
		$r,s' \leftarrow$ execute($a$)
		$a' \leftarrow \pi(s')$
		$q_\pi(s,a) \leftarrow q_\pi(s,a) + \alpha\left(r + \gamma q_\pi(s',a') - q_\pi(s,a)\right)$
		$s,a \leftarrow s',a'$
	Until $s$ is terminal state
```

## Policy Improvement
Policy Improvement is done by making the policy greedy with respect to the current value function.

## Policy Control
Monte Carlo control finds the optimal policy by alternating between Policy Evaluation and Policy Improvement. We can give up trying to complete Policy Evaluation before returning to Policy Improvement, instead we can update the policy after every step.

As with [Monte Carlo Methods](./monteCarloMethods.html), Temporal Difference uses $\epsilon$-greedy policy to balance between exploration and exploitation.

### SARSA
SARSA updates a $\epsilon$-greedy policy $\pi$ from experiences sampled from $\pi$. 
```
$\boldsymbol{SARSA}$

$\forall s\in \mathcal{S},a\in\mathcal{A}: q_\pi(s,a) \leftarrow 0$
$\pi \leftarrow \epsilon$-greedy($q_\pi$)
Repeat $1\dots n$:
	$s \leftarrow$ starting state
	$a \leftarrow \pi(s)$
	Repeat:
		$r,s' \leftarrow$ execute($a$)
		$a' \leftarrow \pi(s')$
		$q_\pi(s,a) \leftarrow q_\pi(s,a) + \alpha\left(r + \gamma q_\pi(s',a') - q_\pi(s,a)\right)$
		$s,a \leftarrow s',a'$
		$\pi \leftarrow \epsilon$-greedy($q_\pi$)
	Until $s$ is terminal state
For $s \in \mathcal{S}$:
	$\pi(s) \leftarrow \arg\max_a q_\pi(s,a)$
```

### Q-Learning
Q-Learning updates a greedy policy $\pi$ from experiences sampled from a $\epsilon$-greedy policy $\pi'$.
```
$\boldsymbol{Q\mbox{-}Learning}$

$\forall s\in \mathcal{S},a\in\mathcal{A}: q_\pi(s,a) \leftarrow 0$
$\pi \leftarrow \epsilon$-greedy($q_\pi$)
Repeat $1\dots n$:
	$s \leftarrow$ starting state
	Repeat:
		$a \leftarrow \pi(s')$
		$r,s' \leftarrow$ execute($a$)
		$q_\pi(s,a) \leftarrow q_\pi(s,a) + \alpha\left(r + \gamma \max_{a'}q_\pi(s',a') - q_\pi(s,a)\right)$
		$s \leftarrow s'$
		$\pi \leftarrow \epsilon$-greedy($q_\pi$)
	Until $s$ is terminal state
For $s \in \mathcal{S}$:
	$\pi(s) \leftarrow \arg\max_a q_\pi(s,a)$
```