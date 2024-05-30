## Summary


> [!PDF|] [[2402.03620v1.pdf#page=1&selection=58,0,63,22|2402.03620v1, p.1]]
> > Core to the framework is a self discovery process where LLMs select multiple atomic reasoning modules such as critical thinking and step-by-step thinking, and compose them into an explicit reasoning structure for LLMs to follow during decoding
> 
> 

> [!PDF|] [[2402.03620v1.pdf#page=2&selection=182,0,201,7|2402.03620v1, p.2]]
> > Given a task and a set of reasoning module descriptions representing high-level problem-solving heuristics such as “Use critical thinking” and “Let’s think step by step”, Stage 1 of SELF-DISCOVER aims to uncover the intrinsic reasoning structure for solving this task via meta-reasoning. Specifically, we uses three meta-prompts to guide LLMs to select, adapt, and implement an actionable reasoning structure with no labels or training required. We format the structure in key-value pairs similar to JSON due to interpretability and findings on following JSON boosts reasoning and generation quality

### Steps
> [!PDF|] [[2402.03620v1.pdf#page=3&selection=126,43,133,34|2402.03620v1, p.3]]
> > 1) SELECT, where relevant reasoning modules for task-solving are chosen from the set of reasoning module descriptions; 2) ADAPT, where descriptions of selected reasoning modules are rephrased to be more specific to the task at hand; and 3) IMPLEMENT, where the adapted reasoning descriptions are implemented into a structured actionable plan so that the task can be solved by following the structure.

> [!PDF|] [[2402.03620v1.pdf#page=3&selection=135,0,161,2|2402.03620v1, p.3]]
> > SELECT First, not every reasoning module is helpful for every task, so the first stage of SELF-DISCOVER guides model to select modules that are useful based on task examples. For example, “reflective thinking” might help search for first-principle theories on science problems, while “creative thinking” helps on generating a novel continuation to a story. Given raw set of reasoning module descriptions D such as “critical thinking”, and “break the problem into sub-problems” 
> 

> [!PDF|] [[2402.03620v1.pdf#page=3&selection=217,0,230,27|2402.03620v1, p.3]]
> > ADAPT Since each reasoning module provides a general description of how to solve problems, the next step of SELFDISCOVER aims at tailoring each selected module to the task at hand. For example, from “break the problem into subproblems” to “calculate each arithmetic operation in order” for arithmetic problems. Given selected reasoning module subset DS from the previous step, ADAPT rephrases each of the selected module to be more specific to the task. Similarly to SELECT, this stage uses a meta-prompt pA and a generative model M to generate the adapted reasoning module descriptions
> 
> 

> [!PDF|] [[2402.03620v1.pdf#page=3&selection=289,0,324,46|2402.03620v1, p.3]]
> > IMPLEMENT Finally, given the adapted reasoning module descriptions DA, SELF-DISCOVER operationalizes the reasoning modules into an implemented reasoning structure DI with specified instruction on what to generate for each step. In addition to a meta prompt pI , IMPLEMENT also provides a demonstration of a human-written reasoning structure Shuman on another task to better convert the natural language descriptions into a reasoning

> [!PDF|] [[2402.03620v1.pdf#page=3&selection=357,0,369,31|2402.03620v1, p.3]]
> > After the three stages, we have an implemented reasoning structure DI uniquely adapted for the task we need to solve T . Then we can simply append the reasoning structure to all instances of the task and prompt models to follow the reasoning structure to generate
> 
>


