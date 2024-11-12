---
tags:
  - paper
  - ai
  - genai
Created time: 2024-05-20T19:00:00
Last edited time: 2024-05-20T20:14:00
---
# Summary:
The paper “Plan-and-Solve Prompting: Improving Zero-Shot Chain-of-Thought Reasoning by Large Language Model” presents a new approach to improve the reasoning capabilities of Large Language Models (LLMs) like GPT-3. The authors identify three main pitfalls in the existing Zero-shot-CoT method: **calculation errors, missing-step errors, and semantic misunderstanding errors**.

To address these issues, the authors propose two new prompting methods: Plan-and-Solve (PS) Prompting and PS+ Prompting.

**Plan-and-Solve (PS) Prompting** aims to address missing-step errors. It involves two components: devising a plan to divide the entire task into smaller subtasks, and then carrying out the subtasks according to the plan. The prompt for PS prompting replaces **“Let’s think step by step”** of Zero-shot-CoT with **“Let’s first understand the problem and devise a plan to solve the problem. Then, let’s carry out the plan and solve the problem step by step”.**

**PS+ Prompting** is an extension of PS Prompting designed to address calculation errors and improve the quality of generated reasoning steps. It extends the prompt with more detailed instructions such as **“extract relevant variables and their corresponding numerals”** and **“calculate intermediate results (pay attention to calculation and commonsense)”.**

Similar to Zero-shot-CoT, Zero-shot PS prompting consists of two steps. In the first step, the prompt makes an inference using the proposed prompting template to generate the reasoning process and the answer to a problem. In the second step, it extracts the answer for evaluation using the answer extraction prompting.

The authors also discuss the criteria for their prompting methods. They follow Zero-shot-CoT and first convert the input data example into a prompt with a simple template. The input slot contains the input problem statement and a hand-crafted instruction is specified in the input slot to trigger LLMs to generate a reasoning process that includes a plan and steps to complete the plan. To meet the second criterion, they extend the plan-based trigger sentence with more detailed instructions. Specifically, “pay attention to calculation” is added to the trigger sentence to request the LLMs to perform calculations as accurately as possible. To reduce errors resulting from missing necessary reasoning steps, they include “extract relevant variables and their corresponding numerals” to explicitly instruct the LLMs not to ignore relevant information in the input problem statement.

The paper provides an example to illustrate the application of these methods. Based on the example, the prompt used in Step 2 will include the problem statement, variables, and the answer. For this example, the final answer returned by LLM is “623”.


# Notes:
1. **To Improve reasoning**: “Let’s think step by step” of Zeroshot-CoT with “Let’s first understand the problem and devise a plan to solve the problem. Then, let’s carry out the plan and solve the problem step by step
2. **To fix calculate error**: “extract relevant variables and their corresponding numerals” and “calculate intermediate results (pay attention to calculation and commonsense)” instructions
3. **Prompt Design:**
	1. The templates should guide LLMs to pay more attention to calculations and intermediate results and to ensure that they are correctly performed as much as possible. 
	2. For complex Calculation: `Calculate intermediate Results` into the prompt. 

# Trigger Sentence
1. Lets think step by step
2. Extract variables and assign their corresponding numerals to these variables first and then solve the problem step by step
3. Firstly, extract variables and their corresponding numerals. Then, calculate intermediate variables. Finally, solve the problem step by step. 
4. Let’s first understand the problem and devise a plan to solve the problem. Then, let’s carry out the plan and solve the problem step by step. 
5. Let’s first understand the problem, extract relevant variables and their corresponding numerals, and make a plan. Then, let’s carry out the plan, calculate intermediate variables (pay attention to correct numerical calculation and commonsense), solve the problem step by step, and show the answer.


> [!PDF|] [[2305.04091.pdf#page=1&selection=47,1,58,24|2305.04091, p.1]]
> > To eliminate the manual effort, Zeroshot-CoT concatenates the target problem statement with “Let’s think step by step” as an input prompt to LLMs. Despite the success of Zero-shot-CoT, it still suffers from three pitfalls: calculation errors, missing-step errors, and semantic misunderstanding errors. To address the missing-step errors, we propose Planand-Solve (PS) Prompting


> [!PDF|255, 208, 0] [[2305.04091.pdf#page=1&annotation=648R|2305.04091, p.1]]
> > To address the calculation errors and improve the quality of generated reasoning steps, we extend PS prompting with more detailed instructions and derive PS+ prompting


> [!PDF|] [[2305.04091.pdf#page=1|2305.04091, p.1]]
> > Zero-shot CoT eliminates the need for manually crafted examples in prompts by appending “Let’s think step by step” to the target problem fed to LLMs such arXiv:2305.04091v3 [cs.CL] 26 May 2023 as GPT-3. This simple prompting strategy surprisingly enables LLMs to yield performance similar to few-shot CoT prompting
> 
> 

> [!PDF|] [[2305.04091.pdf#page=2&selection=35,22,47,2|2305.04091, p.2]]
> > It consists of two components: first, devising a plan to divide the entire task into smaller subtasks, and then carrying out the subtasks according to the plan. In our experiments, we simply replace “Let’s think step by step” of Zeroshot-CoT with “Let’s first understand the problem and devise a plan to solve the problem. Then, let’s carry out the plan and solve the problem step by step” 

> [!PDF|] [[2305.04091.pdf#page=2&selection=51,11,58,14|2305.04091, p.2]]
> > Specifically, we extend it with “extract relevant variables and their corresponding numerals” and “calculate intermediate results (pay attention to calculation and commonsense)” instructions


> [!PDF|255, 208, 0] [[2305.04091.pdf#page=2&annotation=654R|2305.04091, p.2]]
> > Similar to Zero-shot-CoT, Zero-shot PS prompting consists of two steps. In step 1, the prompt first makes an inference using the proposed prompting template to generate the reasoning process and the answer to a problem. In step 2, it extracts the answer for evaluation by using the answer extraction prompting, such as “Therefore, the answer (arabic numerals) is”

> [!PDF|255, 208, 0] [[2305.04091.pdf#page=3&annotation=660R|2305.04091, p.3]]
> > To meet the first criterion, we follow Zero-shotCoT and first convert the input data example into a prompt with a simple template “Q: [X]. A: [T]”. Specifically, the input slot [X] contains the input problem statement and a hand-crafted instruction is specified in the input slot [T] to trigger LLMs to generate a reasoning process that includes a plan and steps to complete the plan. In Zero-shot-CoT, the instruction in the input slot [T] includes the trigger instruction ‘Let’s think step by step”. Our Zero-shot PS prompting method instead includes the instructions “devise a plan” and “carry out the plan” as shown in Figure 2(b). Thus, the prompt would be “Q: [X]. A: Let’s first understand the problem and devise a plan to solve the problem. Then, let’s carry out the plan and solve the problem step by step.”

> [!PDF|255, 208, 0] [[2305.04091.pdf#page=3&annotation=663R|2305.04091, p.3]]
> > To meet the second criterion, we extend the planbased trigger sentence with more detailed instructions. Specifically, “pay attention to calculation” is added to the trigger sentence to request the LLMs to perform calculations as accurately as possible. To reduce errors resulting from missing necessary reasoning steps, we include “extract relevant variables and their corresponding numerals” to explicitly instruct the LLMs not to ignore relevant information in the input problem statement
> 
> 

> [!PDF|255, 208, 0] [[2305.04091.pdf#page=4&annotation=669R|2305.04091, p.4]]
> > Based on the example in Figure 3(b), the prompt used in Step 2 will include “Q: Grace weighs 125 pounds · · · Variables: Grace: 125 pounds · · · Answer: Combined weight of Grace and Alex = 125 + 498 = 623 pounds. Therefore, the answer (arabic numerals) is”. For this example, the final answer returned by LLM is “623”
