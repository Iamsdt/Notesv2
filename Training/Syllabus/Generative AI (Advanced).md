---
Created by: Shudipto Trafder
Created time: 2024-11-12T17:50:00
Last edited by: Shudipto Trafder
Last edited time: 2024-11-12T17:54:00
tags:
  - syllabus
---


**Course Duration**: 12 weeks
**Total Class Time per Week:** 10 hours

**Target Audience:** Individuals with a strong foundation in machine learning, neural networks, and basic Generative AI concepts.

**Course Objectives:** Upon completion, students will be able to:

* Master advanced prompt engineering techniques and fine-tune LLMs for specific tasks.
* Implement complex RAG pipelines and build sophisticated applications with LangChain and LangGraph.
* Develop and deploy robust multi-agent systems.
* Understand the cutting edge of Generative AI research.

## Course Schedule

**Week 1: Advanced Prompt Engineering & LLM Architectures**
* Deep Dive into Transformer Architectures: Attention mechanisms, encoder-decoder models. (3 hours)
* Advanced Prompting:  Prompt engineering for complex reasoning, code generation, and creative writing. (5 hours)
* Hands-on: Exploring the limitations of LLMs and developing strategies for robust prompt engineering. (2 hours)

**Week 2: Fine-tuning LLMs - Theory and Practice**

* Fine-tuning Techniques: Parameter-Efficient Fine-Tuning (PEFT), LoRA, Adapter methods. (4 hours)
* Dataset Preparation and Augmentation for Fine-tuning. (3 hours)
* Hands-on: Fine-tuning a LLM for a specific downstream task using PEFT. (3 hours)


**Week 3: Retrieval Augmented Generation (RAG) - Advanced Architectures**

* Advanced RAG Architectures:  Multi-hop RAG, Knowledge Graph-augmented RAG. (4 hours)
* Implementing complex retrieval strategies: Vector databases, semantic search. (4 hours)
* Hands-on: Building a multi-hop RAG system using a vector database. (2 hours)


**Week 4: LangChain for Complex Applications**

* Advanced LangChain Features: Custom Chains, Callbacks, and Asynchronous operations. (4 hours)
* Building complex workflows: Integrating LLMs with external APIs and tools. (4 hours)
* Hands-on: Building a sophisticated chatbot with external API integrations. (2 hours)


**Week 5: LangGraph and Orchestrating LLM Workflows**

* Advanced LangGraph: Dynamic workflows, conditional execution, and error handling. (4 hours)
* Integrating LangChain with LangGraph for complex applications. (4 hours)
* Hands-on: Building a dynamic LangGraph workflow for a data processing pipeline. (2 hours)


**Week 6: Multi-Agent Systems and Reinforcement Learning**
* Advanced Multi-Agent Systems:  Reinforcement learning for agent coordination. (4 hours)
* Designing reward functions and training strategies for multi-agent systems. (4 hours)
* Hands-on: Implementing a simple multi-agent reinforcement learning scenario. (2 hours)


**Week 7: Generative AI for Code and Software Development**
* Code Generation and Completion with LLMs: Best practices and tools. (4 hours)
* Building coding assistants and automated documentation generation tools. (4 hours)
* Hands-on: Developing a code generation tool for a specific programming language. (2 hours)


**Week 8:  Generative AI for Creative Applications**
* Generative AI for Art, Music, and Storytelling: Exploring creative possibilities. (4 hours)
* Building creative applications: Generating images, music, and narratives. (4 hours)
* Hands-on: Developing a creative application using a generative model (e.g., Stable Diffusion). (2 hours)


**Week 9:  Evaluating and Deploying Generative AI Models**
* Evaluating LLM performance: Metrics and benchmarks. (3 hours)
* Deployment Strategies:  Cloud deployment, serverless functions, and edge deployment. (5 hours)
* Hands-on: Deploying a fine-tuned LLM to a cloud platform. (2 hours)

**Week 10: Advanced Topics in Generative AI Research**
* Exploring cutting-edge research:  Model interpretability, bias mitigation, and safety. (5 hours)
* Emerging trends in Generative AI:  Personalized LLMs, multimodal generation. (5 hours)

**Week 11: Interview Preparation – Technical Deep Dive**
* Review of advanced concepts: Fine-tuning, RAG, LangChain, LangGraph, Multi-agent systems. (4 hours)
* Advanced interview questions and problem-solving strategies. (4 hours)
* Mock interviews:  Simulating challenging technical interviews with detailed feedback. (2 hours)

**Week 12: Project Presentations, Career Guidance, and Future Directions**
* Capstone Project Presentations:  Showcasing advanced projects and contributing to open-source. (5 hours)
* Career guidance and networking:  Connecting with industry experts and exploring career opportunities. (3 hours)
* Future directions in Generative AI:  Open discussion and brainstorming. (2 hours)

**Assessment:**
* Weekly quizzes on theoretical concepts.
* Practical assignments involving prompt engineering and LangChain development.
* Final project demonstrating proficiency in building and deploying a generative AI application.
* Participation in class discussions and mock interviews.

**Resources:**
* LangChain documentation
* Relevant research papers and articles
* Online forums and communities

**Software/Tools:**
* Python
* LangChain
* Preferred LLM provider API keys (OpenAI, Hugging Face, etc.)
* Development environment (e.g., VS Code, Google Colab)
* Deployment platforms (e.g., Streamlit, Gradio)


## Projects

**Project 1: Automated Interview Question Generator & Analysis**

* **Detailed Objective:**  This project aims to build a comprehensive system that assists recruiters throughout the interview process.  The system will have two main components:

    * **Automated Question Generation:** Given a job description and optionally a candidate's resume or profile, the system will generate a set of relevant and insightful interview questions. These questions should assess the candidate's technical skills, soft skills, experience, and cultural fit. The system should allow recruiters to specify the desired focus of the questions (e.g., technical skills, teamwork) and the difficulty level.  It should also avoid generating biased or discriminatory questions.
    * **Automated Response Analysis:**  After an interview, the recruiter can input the candidate's responses. The system will analyze these responses using NLP techniques, including sentiment analysis, keyword extraction, and similarity comparison with ideal answers (if provided). The system will provide a summarized analysis of the candidate's performance, highlighting strengths and weaknesses.  It may also generate a score or rating for each candidate based on the analysis, helping recruiters compare candidates objectively.

* **Implementation Guidance:**

    1. **Data Collection:** Gather a dataset of job descriptions, interview questions, and ideally, candidate responses. Publicly available datasets or synthetic data can be used.
    2. **Model Training:** Fine-tune a large language model (LLM) for both question generation and response analysis tasks. Consider using different models or fine-tuning strategies for each task.
    3. **Feature Engineering:**  For response analysis, extract relevant features from the candidate's responses, such as sentiment scores, keywords related to skills and experience, and similarity to ideal answers.
    4. **Score/Rating System:** Develop a method for scoring or rating candidates based on the analysis of their responses. This could involve a weighted combination of different features.
    5. **User Interface:** Create a user-friendly interface for recruiters to input job descriptions, candidate profiles, and interview responses, and to view the generated questions and analysis.


**Project 2: Bias Detection and Mitigation in Recruitment Processes**

* **Detailed Objective:**  This project focuses on building a tool to identify and mitigate bias in various stages of the recruitment process.  The tool will have two primary functions:

    * **Bias Detection:** Analyze recruitment data, including job descriptions, resumes, and interview feedback, for potential biases related to gender, ethnicity, age, or other protected characteristics. The system should be able to identify both explicit and implicit biases, such as gendered language in job descriptions or disparities in interview ratings based on demographic factors.  The output should provide specific examples of potential bias and quantify the level of bias detected.
    * **Bias Mitigation:** Suggest and implement strategies to mitigate identified biases.  This could include:
        * **Resume Anonymization:**  Removing identifying information like names and addresses from resumes to reduce unconscious bias during the screening process.
        * **Job Description Rewriting:**  Suggesting alternative wording for job descriptions to remove gendered or culturally biased language.
        * **Interview Bias Training:**  Providing recruiters with training materials and resources to raise awareness of unconscious bias and promote fair evaluation practices.
        * **Fairness Metric Tracking:**  Continuously monitor and evaluate the effectiveness of bias mitigation strategies using fairness metrics like demographic parity or equalized odds.


* **Implementation Guidance:**

    1. **Data Collection and Preprocessing:** Collect recruitment data and clean it for analysis. Anonymize sensitive data appropriately.
    2. **Bias Detection Model:**  Train a model to identify biased language and patterns in the data. This might involve fine-tuning an LLM or using specialized bias detection tools.
    3. **Mitigation Strategies:**  Implement algorithms for resume anonymization, job description rewriting, and other mitigation techniques.
    4. **Fairness Metrics:**  Integrate fairness metrics into the system to measure the impact of mitigation strategies.
    5. **User Interface and Reporting:**  Develop a user interface that presents bias detection results clearly and provides recommendations for mitigation. Generate reports to track progress over time.

**Project 3: GitHub PR Agent (Automated Pull Request Reviewer)**

* **Detailed Objective:** This project aims to develop an AI-powered agent that streamlines and enhances the code review process on GitHub. The agent will automate several aspects of reviewing pull requests (PRs), providing valuable feedback to developers and reducing the workload on human reviewers. The project will focus on the following key functionalities:

    * **PR Integration:** Seamlessly integrate with the GitHub API to access all relevant information about a pull request, including code changes, commit messages, existing comments, and relevant repository context.  This integration should be robust and handle various PR scenarios.
    * **Code Analysis:** Perform comprehensive analysis of the code changes within the PR. Utilize techniques like static analysis, code similarity checks, and potentially dynamic analysis to identify potential bugs, style violations, security vulnerabilities, and deviations from established best practices.
    * **Automated Feedback:** Generate clear, concise, and actionable comments directly on the GitHub PR based on the code analysis.  These comments should highlight specific issues, suggest improvements, and ask clarifying questions to the developers. The feedback style and content should be customizable based on project-specific coding standards and guidelines.
    * **Test Generation and Execution (Optional Advanced Feature):** Explore the possibility of automatically generating unit tests based on the code changes introduced in the PR.  Execute these tests and report the results back on the PR, further assisting in the quality assurance process.
    * **Summarization:** Provide a concise summary of the key changes and potential issues identified in the PR. This summary should make it easier for human reviewers to quickly grasp the overall quality and focus their attention on critical areas.
    * **Learning and Adaptation (Advanced Feature):**  Investigate methods for the agent to learn from past reviews and feedback.  This learning could involve incorporating human feedback on the agent's suggestions to improve the accuracy, relevance, and helpfulness of future automated reviews.

* **Implementation Guidance:**
    1. **GitHub API Integration:**  Thoroughly familiarize yourself with the GitHub API and implement robust methods for accessing and interacting with PR data.
    2. **Code Analysis Tools:** Research and select appropriate code analysis tools and libraries. Integrate these tools into the agent's workflow.
    3. **Feedback Generation:** Develop clear templates and strategies for generating helpful and actionable feedback comments.  Consider using LLMs to improve the natural language generation aspect of the feedback.
    4. **Testing Framework Integration (Optional):**  If pursuing the test generation feature, integrate with a suitable testing framework for the target programming language.
    5. **Machine Learning for Adaptation (Optional):**  If implementing learning and adaptation, explore techniques like reinforcement learning or supervised learning to train the agent on historical review data.
    6. **User Interface/Configuration:**  Provide a user interface or configuration mechanism for users to customize the agent's behavior, such as setting coding standards or specifying the types of feedback to prioritize.
