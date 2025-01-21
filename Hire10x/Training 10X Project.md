
User Types: 
1. Student
2. Trainer
3. Vendor
4. Marketing
5. Admin

## Student
1. Dashboard (Performance, Marketing Efforts, How many applied, Mock Interview Date, How Many coding problems solved) + Coding Platform Link
2. Enrolled Courses (Course Overview, Recordings, Additional Resources, Performance, Interview Preparation (With AI)) + Payment Need to be added. (Two classes free)
3. Short Courses Page
4. Career Page (CV Page + Marketing Page)
5. Chat Option (with trainer)

## Trainer
1. Dashboard (student tracking)
2. Manage Courses (manage notes, interview notes, class topics)
3. Payment Management (How much he will be paid)
4. Chat Options

## Vendor
1. Dashboard (student performance)
2. Marketing Efforts
3. Payments
4. Student Management

## Marketing
1. Dashboard (jobs, candidaes)
2. Resume Preparation
3. Available Jobs
4. Available Candidate
5. Application Management

## Admin Panel (Internal)
Can control all the resources


# Details

## Student Portals

### Sidebar
1. **Dashboard:**
    * Personalized overview of student progress.
    * Key performance indicators (coding problems solved, mock interview scores, courses enrolled, Quiz and Assignments scores).
    * Marketing effort updates (applications submitted, responses received).
    * Upcoming deadlines and important announcements.

2. **Courses:**
    * **Live Courses:**  Traditional instructor-led courses with structured curriculum, live sessions, recordings, assignments, and resources.  Payment integration for premium access (with initial free trial). Progress tracking and performance metrics within each course.
    * **Short Courses:** Self-paced, focused courses on specific technologies or skills.  Can serve as prerequisites for live courses or provide targeted skill upgrades.

3. **Playground:**
    * **Live Coding Practice:** Integrated coding platform with personalized metrics tracking.  Performance data feeds into the student dashboard. We have a solution already. That can be reused or we can built our own solution
    * **Notebooks:** Cloud-based Jupyter Notebook environment for interactive learning in specific courses (e.g., AI, Data Analysis, Python).  Pre-configured environments and datasets relevant to the coursework.

4. **Career:**
    * **CV Page:**  Resume builder with role-specific templates and AI-powered suggestions.  Generates relevant interview questions based on the resume content.
    * **Available JD:**  Aggregated job descriptions from various sources. Students can browse and apply directly through the platform.  Integration with the marketing team for personalized job recommendations and application tracking.
    * **Marketing Dashboard:**  Transparency into marketing efforts on the student's behalf.  View application status, feedback, and upcoming opportunities.

5. **Interview:**
    * **Interview Module:**  AI-powered mock interview practice with personalized feedback on performance and areas for improvement.
    * **Mock Interview Scheduling:**  Platform for scheduling mock interviews with human interviewers.  Integrated calendar and communication tools.

6. **Support:**
    * **Chat with Instructor:**  Real-time chat functionality for direct communication with instructors and teaching assistants.  Similar to Slack, enabling quick questions and support.

## Page: Live Course
Same As UI
![[Pasted Image 20250119122117_250.png]]

Note: Note required: Rating, Bookmark, (Top Level List and Grid)

## Page: Course Details
#question Then same as udacity

https://www.udacity.com/course/ai-programming-python-nanodegree--nd089



## Page: Course Content Page
Note after enroll

### List of Tabs
1. Announcements (All course announcements)
2. Course Contents (Main Course content)
3. Quiz 
4. Assignments
5. Course Materials (Explore additional resources, such as supplementary readings and helpful documents, provided by the instructor to enhance your learning experience.)
6. Feedback (Student Feedback)
7. Chat with Instructor
### Tab: Announcements
List of Cards
- Title
- Details
- Date
- View (BTN) (By clicking this, it will open right panel with full details)

### Tab: Course Contents  
This is the landing page.  
At the top, it will display any live announcements (single announcement only).  

**Table:**  (columns)
- **Date**  
- **Class No**  
- **Topic**  
- **Meet Link / Recording**  
- **Trainer**  
- **Notes**  
- **Feedback**  

**Notes:**  
- **Meet Link:** If the class is scheduled, it will display the Meet link along with the scheduled time.  
- **Recording:** If the class is over, it will show the recording video link.  
- **Notes:** It will display the link to the class notes.


### Tab: Quiz
Table: 
1. Date
2. Quiz No
3. Title
4. Link
5. Deadline
6. Obtained Number
7. Remarks (From feedback)

### Tab: Assignment
**Table:**  
1. **Date**  
2. **Assignment No**  
3. **Title**  
4. **Submit**  
5. **Deadline**  
6. **Obtained Number**  
7. **Remarks (From Feedback)**  

**Notes:**  
- **Submit:**  
  - Allow users to upload their assignments.  
  - If submitted, display the submission date.  
  - Users are allowed to resubmit their assignments before the deadline. Only the latest submission will be retained.  
  - Notify users that previous submissions will be replaced and old records will be removed.


### Tab: Course Materials
Table:
1. Date
2. Title
3. Link

### Tab: Feedback
Table:
1. Date
2. Title
3. Descriptions

### Tab: Chat with Instructor  
**Note:**  
Chat with the instructor can be integrated via Slack, Mattermost (an open-source alternative to Slack, customizable with our platform), or a custom chat solution.  

If using a custom solution, the structure will include a table with detailed conversations:  

**Table:**  
1. **Date**  
2. **Title**  
3. **Instructor**  
4. **Chats** (Show Chat UI button)  
5. **Is Resolved**  

**Note:**  
- Clicking on a row will open a right-side panel with the chat interface for that specific conversation.