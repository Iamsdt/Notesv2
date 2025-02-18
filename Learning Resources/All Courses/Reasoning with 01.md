
## Introductions

- Models are like children: they always say the first thing that comes to the mind
- As they grow and mature, they need to be taught valuable lessons
- They should think before speak

O1 use COT, to do the reasoning

How its work?
1. Identifying problem and solution space
2. Development of hypotheses
3. Testing of hypotheses
4. Rejecting ideas and backtracking
5. Identifying most promising path


Completion Tokens: 
Completion Tokens can be now be broken down into two categories:
- Reasoning Tokens: These tokens are used to reason about the problem and solution space. They are used to develop hypotheses, test hypotheses, reject ideas, backtrack, and identify the most promising path.
- Output Tokens: These tokens are used to generate the final output. They are used to generate the final solution, explanation, or reasoning.

Note: Reasoning Tokens are not passed from one turn to next turn. They are only used in the current turn. Output Tokens are passed from one turn to the next turn. If you want that you need to prompt to use the reasoning tokens in the next turn.

Breakthroughs:
Ability to think longer time generate better results
Verification via Consensus Voting or Majority Voting

- **Consensus Voting:**  
  Multiple models (or multiple reasoning passes) produce outputs, and the final answer is selected only if there is sufficient agreement among them. This method seeks a general consensus to ensure that the output is robust.

- **Majority Voting:**  
  This is a straightforward approach where the answer that appears most frequently across several responses is chosen as the final output.

# How does it work in detail?
1. Use Large Scale RL to generate a chain of thoughts before answering
2. COT is longer and higher quality then what is attained via prompting
3. COT contains behavior like
- Error Correction
- Trying Multiple Strategies
- Breaking down problems into sub-problems

Link: https://openai.com/index/learning-to-reason-with-llms/


# Abstract Reasoning
- Abstract reasoning is the ability to think about things that are not physically present. It is the ability to understand concepts and ideas that are not concrete or tangible.
- Abstract reasoning is a key component of human intelligence. It is the ability to think about things that are not physically present. It is the ability to understand concepts and ideas that are not concrete or tangible.

# The Generator Verifier Gap
1. For Example, verifying a good solution is easier than generating one
- Many puzzles (sudoku)
- Math problems
- Logic problems
- Programming problems
here verification is important

But, Some case where verification not that important
- Information retrieval
- Image Recognition

When a generator-verifier gap is present, and we have a good verifier, we can spend more time on generating better solutions.

# Where we can use this Reasoning model?
1. Data Analysis
2. Mathematical Reasoning
3. Experimental Design
4. Scientific Reasoning
5. Biological and Chemical Reasoning (STEM subjects)
6. Algorithmic Reasoning
7. Literary Reasoning (combine multiple research papers)

IN general, lets not use reasoning token for everything, Use when you need
higher intelligence, creativity, and problem-solving skills, in cost of
latency and tokens.

# Prompting O1 Model
1. Simple and Direct Prompts: Write prompts that are straightforward and concise, Direct instructions yield better results.
2. No Explicit Cot Required: You can skip step by step (COT) reasoning prompts.
The o1 models can infer and execute these itself without details breakdowns.
3. Structure: Break complex prompts into sections using delimiters like markdown, xml, or quotes.
This structured format enhances model accuracy and simplifies your own troubleshooting.
4. Show Rather than tell: Rather than excessive explanation, give a contextual example to
give the model understanding of the broad domain of your task.


Examples:
2. Simple and COT
Bad Prompt
```
Generate a function that outputs the SMILES IDs for all the molecules involved in insulin."
"Think through this step by step, and don't skip any steps:"
"- Identify all the molecules involve in insulin"
"- Make the function"
"- Loop through each molecule, outputting each into the function and returning a SMILES ID"
"Molecules: 
```

Good Prompt
```
Generate a function that outputs the SMILES IDs for all the molecules involved in insulin.
```

3. Structure
```
structured_prompt = ("<instructions>You are a customer service assistant for AnyCorp, a provider"
          "of fine storage solutions. Your role is to follow your policy to answer the user's question. "
          "Be kind and respectful at all times.</instructions>\n"
          "<policy>**AnyCorp Customer Service Assistant Policy**\n\n"
            "1. **Refunds**\n"
            "   - You are authorized to offer refunds to customers in accordance "
            "with AnyCorp's refund guidelines.\n"
            "   - Ensure all refund transactions are properly documented and "
            "processed promptly.\n\n"
            "2. **Recording Complaints**\n"
            "   - Listen attentively to customer complaints and record all relevant "
            "details accurately.\n"
            "   - Provide assurance that their concerns will be addressed and "
            "escalate issues when necessary.\n\n"
            "3. **Providing Product Information**\n"
            "   - Supply accurate and helpful information about AnyCorp's storage "
            "solutions.\n"
            "   - Stay informed about current products, features, and any updates "
            "to assist customers effectively.\n\n"
            "4. **Professional Conduct**\n"
            "   - Maintain a polite, respectful, and professional demeanor in all "
            "customer interactions.\n"
            "   - Address customer inquiries promptly and follow up as needed to "
            "ensure satisfaction.\n\n"
            "5. **Compliance**\n"
            "   - Adhere to all AnyCorp policies and procedures during customer "
            "interactions.\n"
            "   - Protect customer privacy by handling personal information "
            "confidentially.\n\n6. **Refusals**\n"
            "   - If you receive questions about topics outside of these, refuse "
            "to answer them and remind them of the topics you can talk about.</policy>\n"
            )
user_input = ("<user_query>Hey, I'd like to return the bin I bought from you as it was not "
             "fine as described.</user_query>")
```

4. Show Rather than tell
```
base_prompt = ("<prompt>You are a lawyer specializing in competition law, "
               "assisting business owners with their questions.</prompt>\n"
               "<policy>As a legal professional, provide clear and accurate "
               "information about competition law while maintaining "
               "confidentiality and professionalism. Avoid giving specific "
               "legal advice without sufficient context, and encourage clients "
               "to seek personalized counsel when necessary. Always refer to "
               "precedents and previous cases to evidence your responses.</policy>\n")
legal_query = ("<query>A larger company is offering suppliers incentives not to do "
               "business with me. Is this legal?</query>")
```
Now and example
```
example_prompt = ("<prompt>You are a lawyer specializing in competition law, "
               "assisting business owners with their questions.</prompt>\n"
               "<policy>As a legal professional, provide clear and accurate "
               "information about competition law while maintaining "
               "confidentiality and professionalism. Avoid giving specific "
               "legal advice without sufficient context, and encourage clients "
               "to seek personalized counsel when necessary.</policy>\n"
               """<example>
<question>
I'm considering collaborating with a competitor on a joint marketing campaign. Are there any antitrust issues I should be aware of?
</question>
<response>
Collaborating with a competitor on a joint marketing campaign can raise antitrust concerns under U.S. antitrust laws, particularly the Sherman Antitrust Act of 1890 (15 U.S.C. §§ 1–7). Section 1 of the Sherman Act prohibits any contract, combination, or conspiracy that unreasonably restrains trade or commerce among the states.

**Key Considerations:**

1. **Per Se Illegal Agreements:** Certain collaborations are considered automatically illegal ("per se" violations), such as price-fixing, bid-rigging, and market allocation agreements. For example, in *United States v. Topco Associates, Inc.*, 405 U.S. 596 (1972), the Supreme Court held that market division agreements between competitors are per se illegal under the Sherman Act.

2. **Rule of Reason Analysis:** Collaborations that are not per se illegal are evaluated under the "rule of reason," which assesses whether the pro-competitive benefits outweigh the anti-competitive effects. In *Broadcast Music, Inc. v. Columbia Broadcasting System, Inc.*, 441 U.S. 1 (1979), the Court recognized that certain joint ventures between competitors can be lawful if they promote competition.

3. **Information Sharing Risks:** Sharing competitively sensitive information, such as pricing strategies or customer data, can lead to antitrust violations. The Department of Justice and the Federal Trade Commission caution against exchanges that could facilitate collusion (*Antitrust Guidelines for Collaborations Among Competitors*, 2000).

**Recommendations:**

- **Define the Scope:** Clearly delineate the parameters of the collaboration to focus on the marketing campaign without involving competitive aspects like pricing or market division.
- **Implement Safeguards:** Establish protocols to prevent the exchange of sensitive information that is not essential to the marketing effort.
- **Legal Consultation:** Given the complexities of antitrust laws, consult with a legal professional to ensure the collaboration complies with all legal requirements.

**Conclusion:**

While joint marketing campaigns between competitors are not inherently illegal, they must be structured carefully to avoid antitrust pitfalls. Legal guidance is essential to navigate these issues and to design a collaboration that achieves your business objectives without violating antitrust laws.
</response>
</example>""")
```