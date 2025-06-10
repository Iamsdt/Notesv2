Course Activity:
1. Daily Stand-up
2. Daily Rapid-fire interview question (2 mins)
3. Daily Quiz
4. Weekly Demo on Assignment/Project (Extra work)
5. Weekly Assignment (Phase 1)
6. Weekly Quiz (for Entire Session)
7. Projects (Complete agile, student works as a team) (Phase 2)


Phase 1: **Phase 1: Intensive Learning (1.5 Months / 6 Weeks)**
Phase 2: **Phase 2: Integrated Project & Data Engineering (1.5 Months / 6 Weeks)**

## **Phase 1: Intensive Learning (1.5 Months / 6 Weeks)**

The goal of this phase is to build all the necessary skills for a full-stack developer.

| Week       | **Track 1: Java Backend**                                                                                                                           | **Track 2: React Frontend**                                                                                                          | **Track 3: Problem Solving & Architecture**                                                                                                                      |
| :--------- | :-------------------------------------------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Week 1** | **Java & Tooling Fundamentals:** Core Java (OOP, Collections, Streams, Lambdas), Git, Maven/Gradle, Intro to SQL & PostgreSQL.                      | **Web Foundations:** HTML5, CSS3, JavaScript (ES6+), DOM Manipulation, Fetch API.                                                    | **Foundations:** Big O Notation, Data Structures Overview. **LeetCode:** Arrays & Strings. **System Design:** Client-Server Model, What is an API?               |
| **Week 2** | **Spring Boot & REST APIs:** Spring Core (DI), Building RESTful APIs (`@RestController`, `@GetMapping`, etc.), JPA & Hibernate for DB interaction.  | **Intro to React:** JSX, Components (Functional), Props, State (`useState`), Handling Events.                                        | **Core Data Structures:** **LeetCode:** Linked Lists & Hash Maps. **System Design:** Designing a Robust REST API.                                                |
| **Week 3** | **Backend Testing & Data Validation:** Unit Testing with JUnit & Mockito, Integration Testing, Bean Validation.                                     | **React Hooks & Routing:** `useEffect`, `useContext`. Client-side routing with React Router.                                         | **Advanced Data Structures:** **LeetCode:** Stacks & Queues. **System Design:** Authentication vs. Authorization Patterns.                                       |
| **Week 4** | **Microservice Architecture:** Principles of Microservices, Spring Cloud Gateway for routing, Inter-service communication (RestTemplate/WebClient). | **Styling & UI Kits:** Tailwind CSS for utility-first styling. Building with a component library like **ShadCN/UI**.                 | **Trees & Graphs Intro:** **LeetCode:** Tree Traversals, BSTs. **System Design:** API Gateway & Service Discovery.                                               |
| **Week 5** | **Containerization with Docker:** Writing Dockerfiles for Spring Boot apps, Docker Compose for multi-container environments.                        | **Advanced State & Data Fetching:** **Tanstack Query (React Query)** for server state management, caching, and data synchronization. | **Advanced Problem Solving & AI:** **LeetCode:** Graphs (BFS, DFS). **Prompt Engineering Workshop:** Zero-shot, Few-shot prompting, using OpenAI/Vertex AI APIs. |
| **Week 6** | **CI/CD & Deployment:** Building a full CI/CD pipeline with **GitHub Actions** to automatically test and containerize the microservices.            | **Frontend Testing:** Unit & Integration testing with **Jest** and **React Testing Library**.                                        | **Complex Problems:** **LeetCode:** Dynamic Programming (Intro). **System Design:** Design a large-scale system (e.g., "Design Twitter's Feed").                 |

**End of Phase 1 Outcome:** Students will have built a standalone, multi-service Java backend and a separate, fully-featured React frontend. They can run and test both locally using Docker. They will have solved ~40-50 LeetCode problems and understand core system design principles.

---

## **Phase 2: Integrated Project & Data Engineering (1.5 Months / 6 Weeks)**

The "classes" stop. The day is now structured around project work, stand-ups, and targeted workshops for the data engineering stack.

**The Central Project:** Migrate data from the application built in Phase 1 (simulating a legacy system's PostgreSQL DB) to Google BigQuery, and build analytical features on top of it.

| Week | **Primary Focus & Milestones** | **New Technologies Introduced** |
| :--- | :--- | :--- |
| **Week 7** | **Project Setup & Data Ingestion:** Define the Banking Case Study. Set up GCP environment (IAM, GCS, BigQuery). Write the first data extraction script to pull data from the application's PostgreSQL DB and land it in Google Cloud Storage (GCS). | **Python for Data Engineering, Google Cloud SDK, Apache Spark (PySpark) - DataFrame API.** |
| **Week 8** | **ETL & Data Warehousing:** Develop the PySpark transformation logic. Clean, enrich, and aggregate the raw data. Design the schema in BigQuery and load the transformed data from GCS into BigQuery tables. This is the **PoA (Point of Arrival)** step. | **PySpark Transformations, BigQuery Schema Design, GCP Dataflow (as a Beam runner concept).** |
| **Week 9** | **Orchestration & Automation:** Create a production-grade data pipeline. Schedule the entire ETL process to run daily, handle failures, and log outcomes. | **Apache Airflow:** Writing DAGs, using Operators (Bash, Python), scheduling. |
| **Week 10**| **Case Study 1 - Banking Architecture:** **Integrate End-to-End.**<br> 1. Create a new API endpoint in the Java backend that queries BigQuery.<br> 2. Create a new "Analytics Dashboard" page in the React app.<br> 3. This dashboard calls the new API to display insights from BigQuery (e.g., daily fraud alerts, high-value transaction summaries). | *(Application of all skills)*. **Performance Engineering:** Use JMeter to test the load on the new analytics endpoint. |
| **Week 11**| **Case Study 2 - E-commerce & Gen-AI:** Apply the entire pattern to a new domain (E-commerce).<br> 1. Analyze user clickstream/purchase data.<br> 2. **Gen-AI Feature:** Build a new microservice. It takes a `userId`, queries their data from BigQuery, and uses a **Gen-AI prompt** to generate a human-readable, personalized product recommendation summary. Display this summary in the React UI. | **Gen-AI APIs in a production context.** |
| **Week 12**| **Final Polish & Career Prep:** **Code Review Focus:** Intensive Peer Review and AI-assisted review (GitHub Copilot). Final project presentations. Portfolio refinement on GitHub. Mock interviews (technical, behavioral, system design). | *(Career development skills)*. |
