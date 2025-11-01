# 🚀 10xScale Agentflow: The Practical, LLM-Agnostic Orchestration Framework

10xScale Agentflow is a lightweight, high-performance framework for building and orchestrating multi-agent AI systems. Designed for production environments, it offers unparalleled flexibility, speed, and control without locking you into any specific LLM or tool ecosystem.

- **📜 Documentation:** [10xhub.github.io/Agentflow/](https://10xhub.github.io/Agentflow/)
    
- **💻 Code:** [github.com/10xhub/agentflow](https://github.com/10xhub/agentflow)
    

---

## Key Features that Set Agentflow Apart

### 🎯 **True LLM-Agnostic Orchestration**

Agentflow is built with an orchestration-first philosophy. You are never tied to a specific LLM vendor.

- **Bring Your Own LLM:** Seamlessly use models from **OpenAI, Gemini, Claude, LiteLLM**, or any other provider.
    
- **No Vendor Lock-in:** Unlike frameworks like CrewAI (OpenAI-focused) or Google's ADK (Gemini-centric), we don't dictate your model choice.
    

### 🧠 **Advanced 3-Layer Memory Architecture**

Go beyond simple conversation history with a sophisticated memory system designed for complex interactions.

- **Working Memory (AgentState):** Manages immediate context for the current task.
    
- **Session Memory (Checkpointers):** Stores conversation history using a dual-storage system (**Redis** for speed, **PostgreSQL** for durability).
    
- **Knowledge Memory (Stores):** Enables long-term learning of patterns and preferences with semantic search via **Qdrant** or **Mem0**.
    

### ⚡ **Automatic Parallel Tool Execution**

Dramatically boost performance for I/O-heavy tasks with zero extra configuration.

- **Built-in Concurrency:** Agentflow automatically executes multiple tool calls in parallel, a feature that requires manual implementation in LangGraph, AutoGen, or CrewAI.
    
- **3x+ Performance Gains:** Achieve significant speed improvements right out of the box.
    

### 🔧 **Advanced & Flexible Tool Integration**

Integrate tools cleanly and efficiently.

- **First-Class Support:** Native support for **MCP (Model Context Protocol)** and remote tool execution.
    
- **Seamless Integration:** Includes adapters for both **Composio** and **LangChain**.
    
- **Clean Definitions:** Use dependency injection for cleaner, more testable tool definitions.
    

### 🎨 **Clean Dependency Injection (InjectQ)**

Eliminate boilerplate code and improve testability with our built-in, type-safe dependency injection system.

- **No Manual Passing:** Automatically inject `state`, `tool_call_id`, configurations, and custom dependencies into your tools and nodes.
    
- **Effortless Testing:** Easily mock dependencies for robust unit tests.
    

### 💾 **Production-Grade Persistence**

Agentflow is built for reliability and scale.

- **Dual-Storage Checkpointer:** An intelligent caching strategy uses **Redis** for active conversations and **PostgreSQL** for durable, long-term storage.
    
- **Comprehensive State Management:** Persist agent states, messages, and thread metadata with ease.
    

### 🔀 **Simplified Graph Orchestration**

Inspired by LangGraph but simplified for ease of use, our graph system allows you to define complex workflows that work with any LLM.

- **Flexible Routing:** Define nodes, edges, and conditional logic to create powerful agent behaviors.
    
- **Pre-built Patterns:** Get started quickly with templates for ReAct, RAG, SupervisorTeam, MapReduce, and more.
    

### 📊 **Granular Real-Time Streaming**

Maintain complete control over data flow and observability.

- **Multiple Streaming Modes:** Stream raw tokens, completed messages, node outputs, or system events.
    
- **Event Publishing:** Integrate with **Redis, Kafka, or RabbitMQ** to monitor agent activity in real-time.
    

### 🔄 **Integrated Human-in-the-Loop (HITL)**

Easily build workflows that require human oversight or intervention.

- **Pause & Resume:** Built-in support for interrupting execution to allow for human input.
    
- **Approval & Debugging:** Inspect and modify agent state mid-execution for debugging or approval steps.
    

---

## How Agentflow Compares to Other Frameworks

|Framework|Key Weaknesses|Why Agentflow is a Better Choice|
|---|---|---|
|**CrewAI**|OpenAI-focused, rigid role-based structure, executes tasks sequentially.|**LLM-agnostic**, flexible graph orchestration, and automatic parallel execution.|
|**AutoGen**|Steep learning curve, resource-intensive with its conversation-heavy model.|**Lightweight and practical**, offering a balance of flexibility and control.|
|**LangGraph**|Complex abstractions, promotes lock-in with the LangChain/OpenAI ecosystem.|**Simple and framework-agnostic**, allowing you to use any library or LLM you prefer.|
|**Pydantic AI**|Excellent for data validation but lacks focus on multi-agent orchestration.|**Purpose-built for multi-agent systems** with production-ready features.|
|**Google ADK**|Heavily integrated with the Gemini and Google ecosystem, limiting flexibility.|**Truly vendor-neutral**, giving you the freedom to choose the best tools for the job.|