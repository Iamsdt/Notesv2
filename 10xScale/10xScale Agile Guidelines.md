8.7
This document provides practical guidelines for Agile teams, covering daily standups, estimation techniques, workflow states, and issue labeling. It is designed to help teams collaborate efficiently, maintain transparency, and deliver high-quality results.

---
## 🕒 Daily Standup & Demo Times

- **Daily Standup:** Every weekday at 10:15 AM (15 minutes, all team members)
- **Sprint Demo:** Every week Monday at 11:00 AM

---
## **Effective Standup Guidelines for Agile Teams**

Daily standups (also known as daily scrums) are short, focused team meetings that help align everyone, surface blockers, and track progress. They’re a vital part of Agile and Scrum processes.

---

### 📖 Purpose of a Standup

- Share progress since the last meeting

- Identify roadblocks or issues early

- Align on today’s priorities

- Foster team accountability and transparency

  

---

  

### ⏰ Timing & Duration

  

- **Duration**: 15 minutes max

- **Frequency**: Daily, at the same time

- **Best time**: Beginning of the workday to align efforts

---

### ❓ Questions Every Member Should Answer

  

Each person answers these 3 core questions:

1. **What did I accomplish yesterday?**

- (Example: "Finished login API integration.")

2. **What will I work on today?**

- (Example: "Start implementing password reset feature.")

3. **Are there any blockers?**

- (Example: "Waiting on database access from DevOps.")

  

Optional (for distributed or async teams):

- Do I need help or input from anyone?

  

---

  

### 🔄 Best Practices

- Be **concise** – No deep-dive explanations

- Stay **on-topic** – Avoid side conversations

- Use a **parking lot** for extended discussions after standup

- Ensure **everyone participates** (no silent observers)

- Focus on **tasks and blockers**, not just activity

- Update task boards (e.g., Jira, Plane) either before or during the standup

  

---

### 🏢 Team Responsibilities

  

- **Scrum Master / Facilitator**: Keeps time, ensures structure

- **Team Members**: Actively share updates and identify blockers

- **Tech Lead / Manager**: Takes note of escalations and offers support where needed

---

### ❌ Common Pitfalls to Avoid

  

- Turning the standup into a status meeting for a manager

- Not calling out blockers due to fear or hesitation

- Letting a few team members dominate the discussion

- Losing focus and turning it into a planning meeting

  

---

  

### 🚀 Goal

A good standup should leave the team with:

- Clear visibility on what everyone is doing

- Awareness of blockers and who can help

- Confidence that progress is on track

  

Make it a habit. Keep it short. Keep it useful.

  
---


## **Agile Estimation Guide (Fibonacci System)**

  

This guide is intended to help your team estimate tasks using the Fibonacci system in an Agile workflow

  

---

### 📊 Fibonacci Points Meaning




| Points | Meaning                                                         | Examples                                                                                               |
| ------ | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **1**  | Very small task, very low complexity                            | Minor UI change, fix a typo, small CSS tweak                                                           |
| **2**  | Small task, little complexity                                   | Add validation to a form, small API change                                                             |
| **3**  | Moderate effort, some complexity                                | Create a reusable React component, write a new API endpoint                                            |
| **5**  | Larger task, multiple steps or dependencies                     | Create a full-page frontend + backend logic, integration with another module                           |
| **8**  | Big task, complex logic or cross-team dependency                | User authentication system, integrating external APIs like payment gateways                            |
| **13** | Very large task, high uncertainty, possibly needs breaking down | Full-feature module (e.g., messaging system), major refactoring, complex 3rd party service integration |


---

### 🔄 Guidelines for Using Fibonacci Points for Estimation
  
- Use points to express **relative complexity**, not exact hours.

- If a task seems too big to estimate, it's likely a **13 or more** → break it down.

- Ask: "Is this task twice as hard as another one rated 3 points?" → Then maybe it's a 5 or 8.

- Focus on **team consensus** during estimation sessions (e.g., planning poker).

- Track your team's **velocity** (total points completed per sprint) to help with planning.

  
---

## 🗂️ Workflow States in Agile

  
This section explains the typical workflow states used in Agile teams to track the progress of tasks, user stories, or issues. Understanding these states helps ensure clarity, transparency, and smooth handoffs throughout the development process.

  

**How Code Should Flow:**

- New tasks start in the **Backlog**.

- When ready for work, they move to **Todo** at the start of a sprint.

- As a team member begins work, the task moves to **In Progress**.

- Once development is complete, the task transitions to **Testing/Review** for validation and feedback.

- If the task passes all checks, it moves to **Done**. If not, it may return to **In Progress** for further work.

- If a task is no longer needed, it is moved to **Cancelled**.

  

---
#### States:

1. **Backlog**

- Tasks or user stories that have been identified but are not yet ready to be worked on. Items in the backlog are typically awaiting further clarification, prioritization, or grooming. The team reviews the backlog regularly to ensure items are well-defined and prioritized for future sprints.

  

2. **Todo**

- Tasks that are ready for development and have been selected for the current sprint or iteration. These items are clearly defined, estimated, and prioritized. The team can pick up these tasks as soon as they are ready to start new work.

  

3. **In Progress**

- Tasks that are actively being worked on by team members. This state indicates that development or implementation is underway. The team should limit the number of items in this state to avoid context switching and ensure focus.

  

4. **Testing/Review**

- Tasks that have been completed by the developer and are now undergoing testing, code review, or quality assurance. This state ensures that work meets the team's quality standards before being considered done. Feedback may result in tasks moving back to "In Progress."

  

5. **Done**

- Tasks that have passed all reviews and testing, meeting the team's definition of done. These items are considered complete and are ready for release or deployment. No further action is required unless issues are discovered later.

  

6. **Cancelled**

- Tasks that are no longer relevant or required. These items are removed from the active workflow, often due to changes in priorities, requirements, or business needs. Cancelled tasks are documented for historical reference but are not worked on further.

  

## 🏷️ Issue Labels in Agile

  

This section describes common labels used to categorize and prioritize work items in Agile teams. Labels help teams quickly identify the type, urgency, or area of a task, making it easier to organize and manage the workflow.

  

**How Labels Should Be Used:**

- Assign one or more labels to each task or issue to clarify its nature and requirements.

- Use labels to filter, search, and report on work items during standups, planning, and retrospectives.

- Consistent labeling improves transparency and helps the team focus on priorities.

  

**Label Descriptions:**

- **Bug**: Indicates a defect, error, or unexpected behavior that needs to be fixed.

- **Feature**: Represents a new functionality or capability to be added to the product.

- **Improvement**: Enhancements or optimizations to existing features or processes.

- **UI**: Tasks related to the user interface, design, or user experience.

- **API**: Work involving backend APIs, integrations, or data contracts.

- **To Discuss**: Items that require team discussion, clarification, or decision before proceeding.

- **Tech Debt**: Technical debt that should be addressed to maintain code quality and long-term agility.

- **Ready QA**: Tasks that are complete from a development perspective and are ready for quality assurance testing.