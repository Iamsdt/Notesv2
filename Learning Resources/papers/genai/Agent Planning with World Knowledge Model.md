---
Author: Shuofei Qiao
Link: https://arxiv.org/pdf/2405.14205
Status: In progress
Type: Paper
Completed: 2024-11-19T07:34
Last edited time: 
tags:
  - genai
---
Summary:
The paper introduces a World Knowledge Model (WKM) to improve the planning abilities of Large Language Model (LLM) agents in interactive tasks.  LLMs, while powerful, often exhibit shortcomings in these tasks like blind trial-and-error and generating hallucinatory actions due to their lack of real-world understanding.  The WKM addresses this by mimicking the human mental model, providing both global prior knowledge about the task and maintaining dynamic local knowledge during task execution.

The WKM is built by leveraging both expert and agent-explored trajectories.  The agent model is first used to synthesize task knowledge by comparing successful and unsuccessful trajectories.  It then summarizes state knowledge for each planning step from expert trajectories and combines these with previous and next actions to form a state knowledge base.  This knowledge is integrated into expert trajectories and used to train the WKM. The agent model is also retrained to incorporate the learned task knowledge.

During planning, the WKM provides global task knowledge to guide the agent and prevent excessive trial-and-error.  At each step, local state knowledge is retrieved from the state knowledge base using the current state as a query.  This retrieved knowledge, combined with the agent's own predictions and constraints from the previous action, is used to determine the next action.

>[!info]
>In contrast to LLMs, humans possess a mental knowledge model about the physical world [1, 18, 17, 30]. When facing a specific task, they will first briefly rehearse the entire process in mind using their rich prior knowledge before performing mindless actions.

We call this kind of knowledge global task knowledge (a.k.a. environment/task commonsense). In addition, during the task procedure, the mental world knowledge model will constantly maintain a kind of local state knowledge, representing humans’ cognition of the current world state. For example, imagine you are in a room and your task is to *put a clean egg in microwave*. The task knowledge may refer to The egg is most likely in the fridge ... The workflows are: **1) locate and take the egg;** **2) clean the egg using sinkbasin ... The state knowledge possibly refers to My task is to** ... I have found and taked the egg ... Next I should ... The absence of world knowledge can lead to blind trial-and-error in the early planning stages when environmental information is limited. Conversely, in later stages when information is redundant, it can easily result in a confused cognition of the current world state and generate hallucinatory actions.

>[!Markov Decision Process (MDP)]
>A **Markov Decision Process (MDP)** is a way to model decision-making in situations where outcomes are partly random and partly under the control of a decision-maker. It's used in areas like reinforcement learning, robotics, and economics

