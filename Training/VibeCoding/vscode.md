## Github Copilot


# Discussion Topics
1. Prompt Files
2. Project wide Instructions
3. Modes (Agents)
4. Settings and Configurations (Max Requests etc)
6. MCP server


### 1. Prompt Files

Prompt files are reusable Markdown files that define prompts for common, repeatable development tasks. They allow you to create standalone prompts that can be run directly in Copilot Chat, including task-specific context and guidelines. This ensures consistency and saves time on repetitive tasks.

**How to create and use:**
- Create a `.github/prompts/` directory in your workspace.
- Add Markdown files (e.g., `scaffold-component.md`) with your prompt content.
- Run them in chat by referencing the file or using `/prompt` command.
- Combine with custom instructions for enhanced consistency.

**Use cases:**
- Scaffolding new components, API routes, or tests.
- Performing code reviews (e.g., checking quality, security).
- Step-by-step guides for complex processes or project patterns.
- Generating implementation plans or migration strategies.

https://code.visualstudio.com/docs/copilot/customization/prompt-files


### 2. Project wide Instructions (Custom Instructions)

Custom instructions are Markdown files that define common guidelines or rules for tasks like code generation, reviews, or commit messages. They automatically apply to chat interactions or can be included manually, ensuring generated output follows your standards.

**How to set up:**
- Create `.github/copilot-instructions.md` in your repo.
- Define rules for coding practices, technologies, or requirements.
- Use glob patterns for language/framework-specific rules (e.g., `*.js` for JavaScript).

**Use cases:**
- Specifying coding standards, preferred tech stack, or project requirements.
- Specific libraries or frameworks to use/avoid.

Link: https://code.visualstudio.com/docs/copilot/customization/custom-instructions

### 3. Modes (Agents) (Chat Modes)

Chat modes create specialist assistants for specific roles or tasks, such as planning, front-end development, or research. Each mode is defined in a Markdown file describing its scope, capabilities, accessible tools, and preferred language model.

**How to create:**
- Define in `.github/chat-modes/` with Markdown files.
- Specify scope, tools, and model preferences.
- Activate in chat by selecting the mode.

**Use cases:**
- Planning mode: Read-only access for implementation plans.
- Research mode: Access to external resources for tech exploration.
- Front-end mode: Limited to UI-related code generation.

https://code.visualstudio.com/docs/copilot/customization/custom-chat-modes


## Upcoming Feature
1. sub agents
https://github.com/ShepAlderson/copilot-orchestra
2. HandOff https://code.visualstudio.com/docs/copilot/customization/custom-chat-modes#_handoffs

# MCP Server
MCP (Model Control Protocol) server allows organizations to manage and configure AI models used in Copilot Chat. It provides centralized control over model selection, usage policies, and monitoring.
https://github.com/mcp?utm_source=vscode-website&utm_campaign=mcp-registry-server-launch-2025

Helpful Tools:
- Playwright -> Testing New designed websites and web apps, Ai will figure out the best way to test based on the codebase and also based on the prompt provided
- Context 7: Fetch Relevant documentation for any library
- Chrome Dev Tools: lets your coding agent (such as Gemini, Claude, Cursor or Copilot) control and inspect a live Chrome browser.
- Serena is a powerful coding agent toolkit capable of turning an LLM into a fully-featured agent that works directly on your codebase. Unlike most other tools, it is not tied to an LLM, framework or an interface, making it easy to use it in a variety of ways

# Premium Models vs Free Models
Unlimited (OX) Models:
- GPT 4.1
- GPT 4.0
- GPT 5 Mini
- Grok Code Fast 1

Premium Models:
- Auto (Give 10% discount)
- Claude Haiku (0.33 means 900 requests per month)
- Claude Sonnet 4/4.5 (1x means 300 requests per month) (Best Model)
- Gemini 2.5 Pro (1x means 300 requests per month)
- GPT 5 Pro (1x means 300 requests per month)
- GPT 5 codex (1x means 300 requests per month) (Best Model)

When you should use Unlimited Models:
1. When you need to do a lot of requests
2. When you need faster response time
2. Need to ask queries about the project codebase
3. Small tasks, simple tasks
4. When you need to do code generation, code explanation, code debugging
5. Easy to medium complexity tasks
6. Unit tests, integration tests

Summary: Use Unlimited models for most tasks, especially those involving code generation and analysis. Reserve Premium models for complex, high-stakes tasks that require advanced reasoning or specialized knowledge, You can go with fall back strategy, start with Unlimited models and if the response is not good enough, then switch to Premium models. Most of the time, Unlimited models will suffice, if you use
better agent modes and better prompt engineering techniques.

When you should use Premium Models:
1. Complex, high-stakes tasks requiring advanced reasoning (e.g., architectural design, algorithm optimization)
2. Specialized knowledge domains (e.g., security audits, performance tuning, niche frameworks)
3. When Unlimited models fail to provide satisfactory responses
4. Tasks needing deeper context understanding or multi-step problem-solving
5. High-accuracy requirements for production code or critical features
6. Advanced agent modes for autonomous coding, refactoring large codebases, or integrating multiple systems
7. When dealing with ambiguous or novel problems that need creative solutions
8. For enterprise-level features like custom integrations or compliance checks


Prompt Tips:
1. Keep prompts short and concise and to the point. Avoid unnecessary details
2. Clear Instructions, what you want and dont want, define clear boundaries (Make sure task are clear and concise and not too broad, or not too big) (Like dont ask to build entire app, but ask to build specific module or feature)
3. Dont forget to mention the tools needed to be used (#playwright -> for testing, #react -> for react code etc)


## Example prompts:
1. **Codebase Understanding**: "Explain how authentication works in #codebase"
2. **Code Generation**: "Add a login button and style it based on #styles.css"
3. **Debugging**: "Fix the issues in #problems"
4. **Testing**: "Add unit tests for the user service"
5. **Refactoring**: "Refactor this code to use async/await"
6. **Source Control**: "Summarize the #changes"
7. **External Resources**: "How do I use the 'useState' hook in React 18? #fetch https://react.dev/reference/react/useState"
8. **Terminal Tasks**: "How do I install npm packages?"
9. **Jupyter Notebooks**: "/newNotebook use pandas to analyze #data.csv"



# UI Design Tips
1. Attach context, files
2. If need to provide examples code snippets, ui snippets, provide them as files rather than pasting in prompt (Better for longer examples, and also keeps prompt short and concise)
2. Clear Instructions, what you want and dont want, define clear boundaries (Make sure task are clear and concise and not too broad, or not too big) (Like dont ask to build entire app, but ask to build specific module or feature)
3. You can add example ui (Only for vision based models). From unlimited models, except Gork, all of the models support vision based inputs.
4. Setup project wide instructions, so that every time you create a new prompt file, those instructions are automatically added to the prompt. This will help in maintaining consistency across different prompts and tasks

Prompt 1:

"Design a responsive login form for a React app. Use Material-UI components, include email and password fields with validation, and a submit button. Attach #login-styles.css for styling reference. Do not include backend logic, focus only on the UI component. When design complete, test it using #playwright for responsiveness across devices.
"

Prompt 2:
Now write unit tests for the login form component you just created using Jest and React Testing Library. Ensure to cover all validation scenarios and user interactions. Refer to #test-guidelines.md for best practices on writing tests. Do not modify the component code, focus solely on the test cases.


## Workflow Breakdown
Say you are starting a new feature. Then you can break down in this style.
1. First share your feature idea with the chats, and ask to generate a implementation plan with steps breakdown
2. Now Ask another AI model act as devil advocate, and review the plan for any potential issues, improvements and security concerns and update the main plan accordingly
3. Now start implementing the steps one by one, for each step, ask the AI to generate code, review code, test code and finally integrate the code, ask ai to mark the step as done.
4. After all steps are done, ask ai to do a final review of the entire feature


Prebuilt Agents and Prompts:
https://github.com/github/awesome-copilot?tab=readme-ov-file