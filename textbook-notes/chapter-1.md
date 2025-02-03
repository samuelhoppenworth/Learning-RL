### Chapter 1 - Introduction

To better process and retain this and future readings, I will be summarizing the sub-sections of  each chapter in my own words. The same goes for important equations, diagrams, pseudo-code, etc. If the formatting looks ChatGPT-ish, this is purely coincidence as I think LLM generated texts are nicely organized and convey information effectively. No LLMs were used in this process, as that would defeat the point.


#### 1.1 Reinforcement learning

**Definition:** Reinforcement learning is the process of learning when to take an action in order to maximize a numerical reward given a particular scenario. For example, an agent learning how to swing a baseball bat needs to decide when to swing in order to maximize the likelyhood of hitting a baseball given its path. The agent is the swinger, the action is swinging the bat, the enviornment is a baseball field, and the scenario is the current pitch.

**Process:** The process by which agents learn is essentially trial-and-error. By exploring the space of possible actions at the agent's disposal and receiving rewards based on these actions, the agent is better informed as to what actions are valuable going forward.

**Exploitation vs. exploration:** However, if the agent is always *exploring* the enviornment, i.e., always trying something new, then the agent is never *exploiting* the information its gained from exploring, i.e., maximizing the numerical reward signal. This balancing of exploration and exploitation is inherent to reinforcement learning and remains unresolved.

**Distinction between RL and other forms of learning:** supervised and unsupervised learning seem like exhaustive categories, but RL falls outside both of them. In superervised learning, a set of features and labels are given to a model, and the model attempts to learn how to label data it has never seen before. In unsupervised learning, a model is given an unlabeled dataset and attempts to find hidden structures within it. Neither of these categories encompasses the problem of trying to maximize a numerical reward signal, which is the ultimate goal of RL.

Additionally, RL and other forms of learning differ in scope. For problems involving an agent interacting with an enviornment to achieve a goal, RL can address in their entirety. However, supervised and unsupervised learning, by themselves, can only tackle sub-problems within these problem. As an example, a supervised learning model may be used to estimate the value of an action the agent can take (i.e., the expected reward given by taking said action), or predict the next enviornment state. In either case, it is ultimately the process of RL that trains the agent to incorporate this data into the agents decision making.

**Trends:** RL is part of a larger trend towards finding simpler, general principles to understand intelligence. It used to be thought that cramming as many facts into a machine as possible would create intelligence, but now, more elegant theories of learning, grounded in general principles, are being sought out. RL's process of trial-and-error is one such principle, evident in its similarity to how humans and animals learn, and serves as a potent paradigm of decision making.