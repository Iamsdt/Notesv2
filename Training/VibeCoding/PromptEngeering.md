# Prompt Engineering: Techniques, Best Practices, and Examples

## Introduction

Prompt engineering is the art of crafting effective instructions for AI language models to get accurate, relevant, and useful responses. It involves clear context, specific constraints, and examples to guide AI behavior.

## Core Techniques

### 1. Few-Shot Prompting
Provide 2-3 examples to demonstrate desired output format and style. This helps the AI understand patterns and reduces ambiguity.

**Best Practices:**
- Use exactly 2-3 examples (more can confuse, fewer may not provide enough guidance).
- Clearly label inputs and outputs (e.g., use arrows or separators).
- Ensure examples are consistent in structure.

**Example:**
```
Classify these support tickets by urgency (High/Medium/Low) and category (Billing/Technical/Account):

Ticket 1: "My account is locked and I need access now!" → High, Account
Ticket 2: "How do I change my payment method?" → Medium, Billing
Ticket 3: "The app keeps freezing." → High, Technical

Now classify: "I can't log in after password reset."
```

### 2. Chain-of-Thought (CoT)
Instruct the AI to show step-by-step reasoning before giving the final answer. This improves accuracy for logical, mathematical, or analytical tasks.

**Best Practices:**
- Explicitly ask for "step-by-step" or "reasoning process".
- Use numbered steps for clarity.
- Combine with few-shot for complex problems.

**Example:**
```
Solve this coding problem step by step:
Write a function to reverse a string in Python.

1. Understand the requirement: Take a string input and return it reversed.
2. Consider edge cases: Empty string, single character, palindromes.
3. Choose approach: Use slicing or loop.
4. Implement: def reverse_string(s): return s[::-1]
5. Test: reverse_string("hello") should return "olleh"
```

### 3. Decomposition
Break down complex tasks into smaller, manageable sub-steps. This prevents the AI from getting overwhelmed and ensures structured outputs.

**Best Practices:**
- Number the steps clearly.
- Define what each step should output.
- Use this for multi-part problems like debugging or planning.

**Example:**
```
Refactor this JavaScript function into smaller, testable parts:

Original function:
function processData(data) {
  // validate, transform, save
}

Steps:
1. Extract validation logic: Create validateData(data) function.
2. Extract transformation: Create transformData(data) function.
3. Extract saving: Create saveData(data) function.
4. Update main function to call these helpers.
5. Add error handling for each step.
```

### 4. Self-Criticism
Ask the AI to evaluate and improve its own initial response. This leads to more accurate, nuanced answers.

**Best Practices:**
- Request specific critique criteria (accuracy, completeness, assumptions).
- Ask for confidence ratings or alternative viewpoints.
- Use for factual or advisory responses.

**Example:**
```
Explain how to optimize a slow SQL query.

Initial Answer: [AI provides explanation]

Self-Critique:
- Accuracy: Does this cover indexing and query structure?
- Completeness: Are there other optimization techniques?
- Assumptions: What if the database is NoSQL?
- Confidence: Rate 1-10 and suggest improvements.
```

### 5. Role Assignment
Assign a specific role or persona to the AI to influence its response style and expertise level.

**Best Practices:**
- Choose roles relevant to the task (e.g., "senior developer", "code reviewer").
- Combine with other techniques for better results.
- Avoid over-relying on this alone, as modern models handle roles well.

**Example:**
```
You are a senior full-stack developer reviewing a junior's React component.

Review this code for best practices, performance, and maintainability:

```jsx
function UserList({ users }) {
  return (
    <ul>
      {users.map(user => <li key={user.id}>{user.name}</li>)}
    </ul>
  );
}
```

Provide specific feedback and suggested improvements.

## Do's and Don'ts

| Do | Don't |
|----|-------|
| Be specific and clear | Use vague instructions |
| Provide context and examples | Assume AI knows your intent |
| Specify format and constraints | Overload with multiple tasks |
| Iterate and refine prompts | Accept first response without validation |
| Use action verbs (analyze, explain) | Start with generic questions |
| Request sources for facts | Ignore potential biases |
| Test different phrasings | Stick to one prompt style |
| Set output length/tone | Leave format unspecified |

## Best Practices

1. **Clarity:** Define exactly what you want.
2. **Context:** Provide background information.
3. **Format:** Specify output structure (bullet points, code, etc.).
4. **Constraints:** Set limits (word count, tone).
5. **Iteration:** Refine based on responses.
6. **Validation:** Verify factual claims.
7. **Examples:** Include 2-3 samples for complex tasks.
8. **Perspective:** Ask for multiple viewpoints when needed.

## Practical Examples

### Code Generation
```
Write a Python function to calculate factorial using recursion.
Include docstring and error handling.
```

### Bug Analysis
```
Debug this JavaScript error: "TypeError: Cannot read property 'length' of undefined"
Provide step-by-step analysis and fix.
```

### Documentation
```
Explain REST API authentication in simple terms.
Use examples with curl commands.
Target: Beginner developers.
```

## Conclusion

Master prompt engineering by focusing on clarity, examples, and iteration. Use the techniques above to get better AI responses for coding, analysis, and problem-solving. Practice regularly and adapt to different models.
