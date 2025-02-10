### Chapter 2: Multi-armed Bandits

#### 2.0 Evaluative vs. Instructive feedback

A key distrinction between RL and other forms of learning is the use of evaluative feedback instead of instructive feedback during training. Evaluative feedback tells an agent how good or bad their decision was, whereas instructive feedback tells the agent what to do. The former is dependent on the action taken, the latter is not.

#### 2.1 A *k*-armed Bandit Problem

The *k*-armed Bandit Problem is a *nonassociative* learning problem, meaning their is only a single state the agent can interact with. In other words, the agent does not learn to associate states with actions when changing its policy. Instead, it has to learn by other means.

The problem itself involves choosing between *k* options, where each option has its own random distribution of rewards and the expected value of each distribution is unknown. The goal of the agent is to maximize its aggregate rewards by repeatedly choosing the option with the the highest expected reward.

The problem might be better understood by the anaology from which it derives its name. "One-armed bandits" are another name for slot-machines, so a *k*-armed bandit is a slow machine with *k* levers, each with its own variable payout. The objective, then, is to predict the odds of each lever and repeatedly pull the one you think yields the most profit (or, more likely in this case, yields the least loss).

#### 2.2 Action-value Methods

*Sample-average*: If the agent's goal is to estimate the expected reward of an action, then an intuitive way of doing so is by averaging the rewards actually received when taking that action. This is called the sample-average method.

*Epsilon-greedy*: Regardless of how the agent estimates the value of each action, it has to balance choosing between the action with the highest predicted reward (the greedy action) and all other actions (the exploratory actions). A simple balancing schema defines some *epsilon* such that the agent chooses the greedy option *(1-epsilon)* percent of the time and exploratory actions *epsilon* percent of the time.

#### 2.3 The 10-armed Testbed

Comparing the performance of different *epsilon values* shows each has its own advantages over the others. Consider the *epsilon* values of 0, 0.1, and 0.01. With an *epsilon* of 0 (a greedy action selection method), the agent does not explore and is therefore less likely to find the optimal policy. For an *epsilon* of 0.1, the agent explores and converges on the optimal policy quickly, but will never choose the greedy option more than 90% of the time. For *epsilon* of 0.01, the agent converges on the optimal policy slower than the agent with an *epsilon* of 0.1, but in the long run, will accumulate more reward than said agent due to choosing the greedy option 99% of the time.

In special cases where the reward variance of each action is 0, the greedy method only needs to try each action once to know its true value, which allows it to outperform *epsilon*-greedy methods that needlessly make sub-optimal exploratory actions. The inverse is true, where the actions with higher reward variance require more exploration to accurately estimate their true expected payout. In these cases, *epsilon*-greedy methods substantially outperform greedy methods.