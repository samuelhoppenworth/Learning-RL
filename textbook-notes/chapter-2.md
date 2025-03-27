### Chapter 2: Multi-armed Bandits

#### 2.0 Evaluative vs. Instructive feedback

A key distrinction between RL and other forms of learning is the use of evaluative feedback instead of instructive feedback during training. Evaluative feedback tells an agent how good or bad their decision was, whereas instructive feedback tells the agent what to do. The former is dependent on the action taken, the latter is not.

#### 2.1 A *k*-armed Bandit Problem

The *k*-armed Bandit Problem is a *nonassociative* learning problem, meaning there is only a single state the agent can interact with. In other words, the agent does not learn to associate states with actions when changing its policy. Instead, it has to learn by other means.

The problem itself involves choosing between *k* options, where each option has its own random distribution of rewards, and the expected value of each distribution is unknown. The goal of the agent is to maximize its aggregate reward by repeatedly choosing the option with the the highest expected value.

The problem might be better understood by the anaology from which it derives its name. "One-armed bandits" are another name for slot-machines, so a *k*-armed bandit is a slot machine with *k* levers, each with its own variable payout. The objective, then, is to predict the odds of each lever and repeatedly pull the one you think yields the most profit (or, more realistically, the least loss).

#### 2.2 Action-value Methods

*Sample-average*: If the agent's goal is to estimate the expected reward of an action, then an intuitive way of doing so is by averaging the rewards actually received when taking that action. This is called the sample-average method.

*Epsilon-greedy*: Regardless of how the agent estimates the value of each action, it has to balance choosing between the action with the highest predicted reward (the greedy action) and all other actions (the exploratory actions). A simple balancing schema defines some *epsilon* such that the agent chooses the greedy option *(1-epsilon)* percent of the time and exploratory actions *epsilon* percent of the time.

#### 2.3 The 10-armed Testbed

*Epsilon value camparison*: Comparing the performance of different *epsilon values* shows each has its own advantages over the others. Consider the *epsilon* values of 0, 0.1, and 0.01. With an *epsilon* of 0 (a greedy action selection method), the agent does not explore and is therefore less likely to find the optimal policy. For an *epsilon* of 0.1, the agent explores and converges on the optimal policy quickly, but will never choose the greedy option more than 90% of the time. For *epsilon* of 0.01, the agent converges on the optimal policy slower than the agent with an *epsilon* of 0.1, but in the long run, will accumulate more reward than said agent due to choosing the greedy option 99% of the time.

*Epsilon value use-cases*: In special cases where the reward variance of each action is 0, the greedy method only needs to try each action once to know its true value, which allows it to outperform *epsilon*-greedy methods that needlessly make sub-optimal exploratory actions. The inverse is true, where the actions with higher reward variance require more exploration to accurately estimate their true expected payout. In these cases, *epsilon*-greedy methods substantially outperform greedy methods.

#### 2.4 Incremental Implementation

*Naive sample-averaging*: One naive approach to implementing sample-averaging for a particular action by tracking all rewards received by taking said action and 
taking the average. But the time and space complexcity of this approach is O(n), 
where n is the number of times the action has been taken. 

*Incremental implementation*: a better method is incrementally updating this value prediction using the following general formula:

        NewEstimate = OldEstimate + StepSize[Target - OldEstimate]

 *StepSize* is a parameter which influences how much the prediction changes.
  *Target* is the actual reward received the last time this action was taken, so *[Target - OldEstimate]* can be thought of
as the error between the prediction and real value of the reward the last time the agent took this action.
So, the greater the error, the more *NewEstimate* moves in the direction of the *Target*, and vice versa.

#### 2.5 Tracking a Nonstationary Problem

*Intuition:* It is often the case that the functions which describe the amount of reward a particular action illicits are nonstationary, i.e., the reward given for taking an action may change over time. It then makes sense to place more weight on recent rewards when predicting the value of a given action going forward.

*Exponential recency-weighted average*: This running average estimates the reward of a given function after it has been selected *n* times, but exponentially diminishes the weights placed on early rewards recevied as *n* increases. Let $Q_n$ denote the estimated reward of an action after *n* selections, let $R_n$ be the actual reward received on the *n*th selection of an action, and let $\alpha$ be a constant stepsize between 0 and 1. 

$$
Q_{n + 1} = (1 - \alpha)^n Q_1 + \sum_{i = 1}^n \alpha(1 - \alpha)^{n - i} R_i
$$

Because $\alpha$ is always less than 1, the $\alpha(1 - \alpha)^{n - i}$ term effectively diminishes the weight that $R_i$ has on the average at an exponential rate, thus placing more weight on recent values of $R_i$, which may better predict $R_{n + 1}$.



