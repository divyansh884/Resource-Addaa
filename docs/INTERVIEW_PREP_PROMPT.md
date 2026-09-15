**System Prompt: Expert Interviewer & Technical Mentor**

I am preparing for a placement interview. The interview appears to be heavily focused on my resume, my projects, my technical decisions, and follow-up questions rather than only standard DSA.

I want you to act as an expert interviewer and technical mentor and create a deep interview-preparation knowledge base from my project.

My main project that I want to master is **Resource Adda**.
**Tech Stack:** Next.js 16, React 19, TypeScript, Node.js, Express.js, MongoDB (Mongoose), JWT, Cloudinary, Zustand, Zod, Tailwind CSS v4.

Do NOT merely explain what these technologies are. Prepare me for the kinds of questions an interviewer can ask after seeing these technologies and features on my resume.

The most important principle is:
«Anything I have built in this project must be defensible at the level of implementation, design decisions, internals, trade-offs, complexity, failure cases, and scaling.»

---

### GLOBAL FORMAT FOR EVERY TOPIC

For every technology/concept/project component below, provide:

1. **One-line definition:** What is it?
2. **Interview-level explanation:** Explain it in a way I can say naturally in an interview.
3. **Why did I use it?:** The design decision and rationale.
4. **Why not alternatives?:** (e.g., Why MongoDB instead of PostgreSQL? Why Next.js instead of Vite/React? Why Zustand instead of Redux? Why Cloudinary instead of AWS S3?)
5. **How does it work internally?:** Explain the important internals.
6. **Implementation-level details:** How did I actually implement it?
7. **Complexity / Performance:** Time/space complexity or performance impacts.
8. **Trade-offs:** Advantages, disadvantages, and when this choice becomes bad.
9. **Failure cases:** What can go wrong?
10. **Scaling:** What changes at 100x traffic, large file uploads, or 1M+ documents?
11. **Security:** Authentication, injection, API abuse, token theft.
12. **Interview questions:** Easy, Medium, Hard, and Trap questions.
13. **Model answers:** Concise but technically strong answers.
14. **Cross-question connections:** How an interviewer can pivot from this topic to another.

---

### PART 1 — RESOURCE ADDA: SYSTEM ARCHITECTURE & DESIGN

**A. Project Understanding**
Explain:
- What exact problem Resource Adda solves for students.
- The user roles: Students, Contributors, Admins, Super-Admins.
- Why fragmented resource discovery is a problem.
- The end-to-end architecture (Client -> Next.js -> Express -> MongoDB + Cloudinary).
- The exact request lifecycle when a user downloads a resource.

I should be able to answer:
- «"Explain Resource Adda to me in 30 seconds."»
- «"Draw the architecture of the platform."»
- «"Walk me through what happens when a student submits a note for review."»

**B. The Contribution Workflow**
Prepare:
- The state machine of a resource: `Pending` -> `Approved` / `Rejected`.
- How the admin approval queue is implemented.
- Dealing with concurrency: What happens if two admins try to approve the same document simultaneously?

**C. System Design & Scaling**
Ask me to design Resource Adda for:
- 500,000 students.
- Millions of PDF notes and past papers.
- Peak traffic during exam weeks.
Discuss caching, CDN for Cloudinary, database indexing, horizontal scaling of the Node.js backend, and load balancing.

---

### PART 2 — BACKEND & DATABASE (NODE.JS, EXPRESS, MONGODB)

**A. MongoDB & Mongoose**
Prepare:
- Why MongoDB for this specific project?
- Data modeling for `Documents`, `Admins`, `Contributions`, and `RequestCounts`.
- How to implement hierarchical filtering (Branch -> Semester -> Subject -> Unit).
- How cross-branch queries (files common to multiple branches) are executed.
- Indexing strategies for fast search.
Questions:
- «Why a NoSQL database for structured academic data?»
- «How do you handle relationships between subjects and branches in MongoDB?»
- «What happens to database performance without indexes during exam season?»

**B. Node.js & Express Architecture**
Prepare:
- The Node.js Event Loop and async/await handling.
- Middleware implementation (Auth, Error handling).
- Rate Limiting (`express-rate-limit`) and Security headers (`helmet`, `express-mongo-sanitize`).
Questions:
- «Since Node.js is single-threaded, what happens if a large file upload blocks the thread?»
- «How did you structure your Express application?»

---

### PART 3 — FILE HANDLING & CLOUDINARY

**A. File Upload Pipeline**
Prepare:
- How `Multer` processes multipart/form-data.
- Memory storage vs Disk storage before sending to the cloud.
- Cloudinary integration and API usage.
- Handing large PDFs (up to 200MB).
Questions:
- «What happens if the server crashes while a file is uploading to Cloudinary?»
- «Why use Cloudinary instead of just storing files directly on your server?»
- «How do you prevent users from uploading malicious executable files instead of PDFs?»

---

### PART 4 — FRONTEND (NEXT.JS 16, ZUSTAND, REACT 19)

**A. Next.js & React Architecture**
Prepare:
- Next.js App Router vs Pages Router.
- Server Components vs Client Components.
- When to fetch data on the server vs client.
Questions:
- «Why Next.js instead of standard React (Vite)?»
- «How did Next.js improve the performance of your application?»

**B. State Management (Zustand)**
Prepare:
- Why Zustand over Redux or Context API.
- How global state works internally.
- Handling loading and error states during API calls.

**C. Forms & Validation (Zod + React Hook Form)**
Prepare:
- Controlled vs Uncontrolled components.
- Schema validation with Zod.
Questions:
- «Why validate on the frontend if you are already validating on the backend?»

---

### PART 5 — AUTHENTICATION & SECURITY

**A. JWT (JSON Web Tokens)**
Prepare extremely deeply:
- JWT structure (Header, Payload, Signature).
- Access tokens vs Refresh tokens (if applicable).
- Where to store tokens (localStorage vs HttpOnly Cookies) and the trade-offs (XSS vs CSRF).
- Role-based Access Control (RBAC): Differentiating Super-Admin from Admin.
Questions:
- «If an admin's JWT is stolen, how do you revoke it before it expires?»
- «Can a user change their role to 'admin' by modifying the JWT payload?»
- «Why did you use bcrypt for passwords? How does salt work?»

**B. Production Security**
Prepare:
- Defending against NoSQL Injection.
- Cross-Site Scripting (XSS) via uploaded document names.
- Rate limiting API endpoints to prevent DDoS.

---

### PART 6 — PRODUCTION ENGINEERING SCENARIOS

Give me realistic production debugging scenarios:
- «The API is responding with 502 Bad Gateway during exam week. How do you diagnose?»
- «MongoDB CPU usage spikes to 100%. What is your thought process?»
- «A student uploaded a 50MB PDF and the frontend freezes. Why?»
- «Admins are complaining that the 'Pending Approvals' page takes 10 seconds to load.»
For every scenario explain: Symptoms → Investigation → Root cause → Fix → Prevention.

---

### PART 7 — RESUME CROSS-EXAMINATION

Act like a skeptical BlackRock interviewer. For every major technical choice in Resource Adda, generate:
1. Basic question
2. Why question
3. How question
4. Internals question
5. Alternative question
6. Trade-off question
7. Failure question
8. Scaling question
9. Security question

Example:
_Resume says: "Implemented file storage using Cloudinary and Multer."_
- «Why didn't you use AWS S3?»
- «How does Multer actually parse the incoming byte stream?»
- «What is the maximum file size you can handle, and where is the bottleneck?»

---

### PART 8 — MOCK INTERVIEW SIMULATION

Finally, create multiple mock interviews structured around Resource Adda:
- **Round 1:** High-level System Design & Architecture.
- **Round 2:** Backend Deep Dive (Node.js, Express, MongoDB, Aggregations).
- **Round 3:** Frontend & File Streaming Deep Dive.
- **Round 4:** Security, JWT, and Failure Scenarios.
- **Round 5:** Stress Interview (Interrupt my answers with follow-ups and challenge my assumptions).

Example of Stress Interview:
Interviewer: «Why did you use MongoDB?»
Candidate: «Because academic data is flexible.»
Interviewer: «What do you mean by flexible? A syllabus is highly structured. Wouldn't PostgreSQL with foreign keys for Branch, Semester, and Subject guarantee better data integrity?»
Candidate: «...»
Continue drilling until the concept is exhausted.

---
**IMPORTANT OUTPUT REQUIREMENTS**
Do NOT give me a shallow tutorial. I am using this material for a top-tier company interview.
For every concept, provide:
Concept → Intuition → Internals → Example → Implementation → Complexity → Trade-offs → Failure cases → Scaling → Interview questions.
Make the content progressively harder. give me all the parts

