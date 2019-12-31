---
layout: post
title: Markov Decision Process
next: Dynamic Programming
next-url: /reinforcementLearning/dynamicProgramming.html
---
A Markov Decision Process is represented as a tuple $$ (\mathcal{S}, \mathcal{A}, \mathcal{P}, \mathcal{R}, \gamma, \pi) $$. 
* $$\mathcal{S}$$ is the state space of the agent
* $$\mathcal{A}$$ is the action space of the agent
* $$\mathcal{P}$$ is the state transition probability
* $$\mathcal{R}$$ is the reward function
* $$\gamma$$ is the discount factor
* $$\pi$$ is the policy

At each time step $$t$$, an agent at state $$\mathcal{S}_t$$ performs an action $$\mathcal{A}_t$$ and moves to state $$\mathcal{S}_{t+1}$$. As a consequence of its action, it receives a reward $$\mathcal{R}_{t+1}$$. Therefore the Markov Decision Process generates a sequence 

$$
\mathcal{S}_0,\mathcal{A}_0,\mathcal{R}_1,\mathcal{S}_1,\mathcal{A}_1,\mathcal{R}_2,\mathcal{S}_2,\dots
$$

## State Transition Probability
An agent the executes action $$a$$ in state $$s$$ at time $$t$$ has the probability $$\mathcal{P}^{s'}_{sa}$$ ending up in state $$s'$$ at time $$t+1$$.

$$
P^{s'}_{sa} = P\left[S_{t+1}=s' \;|\; S_t=s,A_t=a\right]
$$

## Reward Function
An agent the executes action $$a$$ in state $$s$$ and ends up in state $$s'$$ receives the reward $$\mathcal{R}^{s'}_{sa}$$.
## Return 
The goal of the agent is to maximise the return, $$\mathcal{G}$$, which is the cumulative reward it receives in the long run. The return at time $$t$$ is given by

$$
\mathcal{G}_t = \mathcal{R}_{t+1} + \gamma \mathcal{R}_{t+2} + \gamma^2 \mathcal{R}_{t+3} + \dots 
$$

## Policy
An agent that follows policy $$\pi$$ has the probability $$\pi_t(s,a)$$ of selecting action $$a$$ in state $$s$$ at time $$t$$.

$$
\pi_t(s,a) = P\left[\mathcal{A}_t=a\;|\;\mathcal{S}_t=s\right]
$$

### Optimal Policy
A policy $$\pi$$ is better than policy $$\pi'$$ if the expected return under policy $$\pi$$ is greater or equal to expected return under policy $$\pi'$$ for all states. The opimal policy is one that maximises the optimal value function.

$$
v_*(s) =\max_\pi v_\pi(s)
$$

The optimal policy must satisfy the Bellman Optimality Equations.

$$
v_*(s) = \max_a \sum_{s'}\mathcal{P}^{s'}_{sa}\left(\mathcal{R}^{s'}_{sa} + \gamma v_*(s')\right)\\
$$

## Value Functions
### State Value Function
The state value function returns the expected return of a state under policy $$\pi$$.

$$
v_\pi(s) = \sum_a \pi_t\left(s,a\right) q_\pi\left(s,a\right)
$$

### State Action Value Function
The state action value function returns the expected return of a state-action under policy $$\pi$$.

$$
q_\pi(s,a) = \sum_{s'} \mathcal{P}^{s'}_{sa}\left(\mathcal{R}^{s'}_{sa} + \gamma v_\pi(s')\right)
$$


