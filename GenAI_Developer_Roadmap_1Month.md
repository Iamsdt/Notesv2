# 🎯 Detailed One-Month Gen AI Developer Roadmap

**Duration:** 30 Days | **Daily Commitment:** 8 hours
**Goal:** Become a capable Generative AI Developer
**Prerequisites:** Python, Basic NumPy/Pandas (Completed)

---

## 🗓️ Week 1: The Foundation - Machine Learning & Deep Learning
*Goal: Understand the "Magic" behind the APIs.*

### Day 1: Machine Learning Core Concepts
**Focus:** What is learning? How do machines learn from data?
*   **Concepts to Master:**
    *   **Supervised vs. Unsupervised Learning:** Labeled vs. unlabeled data.
    *   **Regression vs. Classification:** Predicting values vs. categories.
    *   **Overfitting & Underfitting:** The bias-variance tradeoff.
    *   **Train/Validation/Test Splits:** Why we hide data from the model.
    *   **Loss Functions:** MSE (Mean Squared Error) for regression, Cross-Entropy for classification.
    *   **Gradient Descent:** The engine of learning (Learning Rate, Global vs. Local Minima).
*   **🎓 Resources:**
    *   **[Video] StatQuest with Josh Starmer:** "Machine Learning Illustrated" (Watch the basics playlist).
    *   **[Video] Google Cloud Tech:** "The 7 Steps of Machine Learning".
    *   **[Read] Google ML Crash Course:** Sections on "Framing", "Descending into ML", and "Generalization".

### Day 2: Neural Networks (The Brain)
**Focus:** Building the basic unit of Deep Learning.
*   **Concepts to Master:**
    *   **The Perceptron:** Weights, Biases, and Inputs.
    *   **Activation Functions:** Why we need non-linearity (Sigmoid, ReLU, Tanh).
    *   **Forward Propagation:** How data flows through the network.
    *   **Backpropagation:** The "Chain Rule" in calculus applied to error correction.
*   **🎓 Resources:**
    *   **[Video] 3Blue1Brown:** "But what is a Neural Network?" (Chapters 1-4 - **Must Watch**).
    *   **[Playground] TensorFlow Playground:** Tinker with neural nets in the browser to see them learn.

### Day 3: Deep Learning & Optimization
**Focus:** Making networks deep and efficient.
*   **Concepts to Master:**
    *   **Stochastic Gradient Descent (SGD) vs. Adam:** Optimizers.
    *   **Regularization:** Dropout, L1/L2 (Preventing overfitting).
    *   **Batch Normalization:** Stabilizing training.
    *   **Intro to PyTorch:** Tensors, Autograd.
*   **🎓 Resources:**
    *   **[Video] Andrej Karpathy:** "The spelled-out intro to neural networks and backpropagation: building micrograd".
    *   **[Read] PyTorch 60 Minute Blitz:** Official PyTorch Tutorial.

### Day 4: NLP Fundamentals (Pre-Transformers)
**Focus:** How computers understand text.
*   **Concepts to Master:**
    *   **Tokenization:** Breaking text into numbers (One-hot encoding, Bag of Words).
    *   **Word Embeddings:** Word2Vec, GloVe (King - Man + Woman = Queen).
    *   **RNNs & LSTMs:** Handling sequences and memory (High-level understanding only).
*   **🎓 Resources:**
    *   **[Video] Jay Alammar:** "The Illustrated Word2Vec".
    *   **[Video] MIT 6.S191:** "Recurrent Neural Networks".

### Day 5: The Transformer Revolution (CRITICAL)
**Focus:** The architecture that changed everything.
*   **Concepts to Master:**
    *   **The "Attention" Mechanism:** Why "Attention is All You Need".
    *   **Self-Attention:** How words look at each other for context.
    *   **Encoder-Decoder Architecture:** The original Transformer.
    *   **Positional Encodings:** Giving order to words.
*   **🎓 Resources:**
    *   **[Read] Jay Alammar:** "The Illustrated Transformer" (**The Bible of Transformers**).
    *   **[Video] StatQuest:** "Transformer Neural Networks, clearly explained".

### Day 6: Large Language Models (LLMs)
**Focus:** GPT, BERT, and T5.
*   **Concepts to Master:**
    *   **Decoder-Only Models (GPT):** Generative pre-training.
    *   **Encoder-Only Models (BERT):** Understanding and classification.
    *   **Pre-training vs. Fine-tuning:** The two-stage process.
    *   **RLHF (Reinforcement Learning from Human Feedback):** How ChatGPT became "chatty".
*   **🎓 Resources:**
    *   **[Video] Andrej Karpathy:** "State of GPT" (Microsoft Build talk).
    *   **[Read] Jay Alammar:** "The Illustrated GPT-2".

### Day 7: Hands-on Review & Practice
*   **Task:** Build a simple Neural Network in PyTorch to classify MNIST digits.
*   **Task:** Use Hugging Face `transformers` library to load a pre-trained model (e.g., GPT-2) and generate text.

---

## 🗓️ Week 2: Prompt Engineering & API Engineering
*Goal: Controlling the beast.*

### Day 8: Prompt Engineering Science
*   **Topics:** Zero-shot, Few-shot, Chain of Thought (CoT), ReAct prompting.
*   **Resources:**
    *   **[Read] PromptingGuide.ai:** Read through the "Techniques" section.
    *   **[Video] Andrew Ng (DeepLearning.AI):** "ChatGPT Prompt Engineering for Developers".

### Day 9: Google Gen AI SDK (Gemini) Deep Dive
*   **Topics:** `google-generativeai` library, ChatSession, Streaming responses, Safety settings.
*   **Task:** Build a CLI Chatbot that remembers context.
*   **Resources:** Google AI Studio Quickstarts.

### Day 10: Structured Outputs & Function Calling
*   **Topics:** Forcing JSON output, connecting LLMs to external tools (Calculator, Calendar).
*   **Task:** Build a script that extracts data from emails into a JSON format using Gemini.

### Day 11: OpenAI API & Comparison
*   **Topics:** `openai` python library, System messages vs. User messages.
*   **Task:** Port your Gemini chatbot to use GPT-4o-mini. Compare results.

### Day 12: Multimodality (Vision & Audio)
*   **Topics:** Sending images to Gemini Pro Vision / GPT-4o.
*   **Task:** Build a "Fridge Chef" app: Upload a photo of ingredients, get a recipe.

### Day 13-14: Week 2 Mini-Project
*   **Project:** **"Personal Study Assistant"**
    *   Upload a text note.
    *   Ask the AI to generate a quiz based on it.
    *   Grade the user's answers.

---

## 🗓️ Week 3: RAG (Retrieval Augmented Generation)
*Goal: Chatting with your own data (The most employable skill).*

### Day 15: Embeddings & Vector Spaces
*   **Topics:** What is a vector? Cosine Similarity.
*   **Resources:**
    *   **[Video] Cohere AI:** "What are Text Embeddings?"
    *   **Task:** Write a script to find the most similar sentence in a list using `scikit-learn` cosine similarity.

### Day 16: Vector Databases
*   **Topics:** ChromaDB (Local), Pinecone (Cloud).
*   **Task:** Store 100 text chunks in ChromaDB and query them.

### Day 17: RAG Architecture
*   **Topics:** Ingestion -> Chunking -> Embedding -> Storage -> Retrieval -> Generation.
*   **Resources:**
    *   **[Video] LangChain:** "RAG from Scratch" playlist.

### Day 18: LangChain / LlamaIndex Basics
*   **Topics:** Chains, Retrievers, Document Loaders.
*   **Task:** Build a "Chat with PDF" script using LangChain.

### Day 19: Advanced RAG
*   **Topics:** Hybrid Search (Keyword + Semantic), Reranking results.
*   **Task:** Improve your PDF chatter to handle specific keyword queries better.

### Day 20-21: Week 3 Project
*   **Project:** **"HR Policy Bot"**
    *   Ingest a dummy HR PDF.
    *   Answer questions like "How many leave days do I have?".
    *   Cite the page number where the answer was found.

---

## �️ Week 4: Agents & Production
*Goal: Building autonomous systems.*

### Day 22: Agents & Tools
*   **Topics:** ReAct Pattern (Reason + Act). Giving the LLM "hands".
*   **Resources:**
    *   **[Read] LangChain Docs:** Agents section.

### Day 23: Building Custom Tools
*   **Task:** Create a Python function (e.g., `get_stock_price`) and let the Agent call it.

### Day 24: Streamlit / Gradio UI
*   **Topics:** Building rapid frontends for AI apps.
*   **Task:** Put a UI on your HR Policy Bot.

### Day 25: Deployment
*   **Topics:** Hugging Face Spaces, Streamlit Cloud.
*   **Task:** Deploy your best app so others can use it.

### Day 26-30: Capstone Project
*   **Idea:** **"Market Research Analyst Agent"**
    *   **Input:** A company name.
    *   **Action:** Agent searches the web for recent news, summarizes stock performance, and looks for competitors.
    *   **Output:** Generates a Markdown report.
    *   **Tech Stack:** Python, LangChain, Tavily (Search API), Gemini/OpenAI, Streamlit.

---

## � Essential Bookmarks

1.  **Hugging Face:** The GitHub of AI models.
2.  **Papers with Code:** To see the latest research.
3.  **LangChain Documentation:** For building apps.
4.  **DeepLearning.AI:** For short, high-quality courses.

## 💡 Daily Routine (8 Hours)
*   **09:00 - 11:00:** 🧠 Concept Learning (Videos/Reading)
*   **11:00 - 13:00:** 💻 Code Implementation (Tutorials)
*   **14:00 - 17:00:** 🛠️ Project Building (Apply what you learned)
*   **17:00 - 18:00:** 📝 Review & Blog (Write down what you learned - "Feynman Technique")
