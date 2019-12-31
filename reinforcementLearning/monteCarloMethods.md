---
layout: post
title: Monte Carlo Method
prev: Dynamic Programming
prev-url: /reinforcementLearning/dynamicProgramming.html
next: Temporal Difference
next-url: /reinforcementLearning/temporalDifference.html
---
Monte Carlo method is one of the methods to find the optimal policy. Monte Carlo method
* uses sampling so does not require prior knowledge of the environment $\mathcal{P}$
* only works on complete episodes

## Policy Evaluation
One way to estimate the value of the state-action value function is to average the returns observed after visits to that state-action. Since a state-action pair $(s,a)$ can be visited multiple times in an episode, there are two different methods to estimating the value.
* First visit Monte Carlo averages the returns from first visits to $(s,a)$
* Every visit Monte Carlo averages the returns from every visits to $(s,a)$

### Batch Averaing
Batch averaging stores all observed returns for each $(s,a)$ in a list then calculates the average.
```
$\boldsymbol{First\;Visit\;Monte\;Carlo\;(Batch\;Averaging)}$

$\forall s\in \mathcal{S}, a\in \mathcal{A}: q_\pi(s,a)\leftarrow 0$
$\forall s\in \mathcal{S}, a\in \mathcal{A}: Returns(s,a) \leftarrow [\;]$
Repeat $1 \dots n$:
	Generate episode $\tau$ using policy $\pi$
	For each first occurence $(s,a) \in \tau$:
		$\mathcal{G} \leftarrow $ return of $(s,a)$
		$Returns(s,a)$.append($\mathcal{G}$)
		$q_\pi(s,a) \leftarrow $ average($Returns(s,a)$)
```

### Online Averaging
Online averaging updates the average when a new return is collected.
```
$\boldsymbol{First\;Visit\;Monte\;Carlo\;(Online\;Averaging)}$

$\forall s\in \mathcal{S}, a\in \mathcal{A}: q_\pi(s,a)\leftarrow 0$
Repeat $1\dots n$:
	Generate episode $\tau$ using policy $\pi$
	For each first occurence $(s,a) \in \tau$:
		$\mathcal{G} \leftarrow $ return of $(s,a)$
		$q_\pi(s,a) \leftarrow q_\pi(s,a) + \alpha\left(\mathcal{G} - q_\pi(s,a)\right)$ 
```

## Policy Improvement
Policy Improvement is done by making the policy greedy with respect to the current value function.

## Policy Control
Monte Carlo control finds the optimal policy by alternating between Policy Evaluation and Policy Improvement. We can give up trying to complete Policy Evaluation before returning to Policy Improvement, instead we can update the policy after each epsiode.

### $\epsilon$-greedy Policy
One problem with estimating $q_\pi(s,a)$ is that many state-action pairs might not be visited, this can be solved by replacing the greedy algorithm with an $\epsilon$-greedy algorithm.

 In $\epsilon$-greedy policy we define an exploration probability $\epsilon$. At each time step, there is a probability $\epsilon$ for selecting a random action and a probability $1-\epsilon$ for exploiting the greedy action.
```
$\boldsymbol{First\;Visit\;Monte\;Carlo\;Control\;(Online\;Averaging)}$

$\forall s\in \mathcal{S}, a\in \mathcal{A}: q_\pi(s,a)\leftarrow 0$
$\pi \leftarrow \epsilon$-greedy($q_\pi$)
Repeat $1\dots n$:
	Generate episode $\tau$ using policy $\pi$
	For each first occurence $(s,a) \in \tau$:
		$\mathcal{G} \leftarrow $ return of $(s,a)$
		$q_\pi(s,a) \leftarrow q_\pi(s,a) + \alpha\left(\mathcal{G} - q_\pi(s,a)\right)$ 
	$\pi \leftarrow \epsilon$-greedy($q_\pi$)
For $s \in \mathcal{S}$:
	$\pi(s) \leftarrow \arg\max_a q_\pi(s,a)$
```
