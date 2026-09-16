## Most Likely Project Questions + Technical Follow-Ups

### Web Chat App
- Explain how WebRTC establishes a connection (SDP offer/answer, ICE candidates) — **HIGH**, they will ask this if it's on your resume.
- What's the difference between STUN and TURN? Did you use either?
- How does your signaling server work — what does it actually pass between peers?
- What happens if a peer's connection drops mid-call?
- How would you scale the signaling server across multiple instances?
- Is your data (chat/video) encrypted? (WebRTC media is encrypted by default via DTLS-SRTP — know this.)

### ISS Live Tracker
- How often do you poll the API, and why that interval?
- How do you calculate "distance from user" to the ISS's ground position?
- What happens if the API is down or rate-limits you?
- Why Three.js over a simpler 2D map?
- How do emails get triggered — client-side timer or server-side cron/check?

### DevStreaks
- How do you fetch LeetCode data — official API or workaround? What are the risks?
- How do you handle two different data shapes (GitHub vs LeetCode) in one dashboard?
- How did you actually publish it (Play Store/App Store process)?
- What does your update cycle look like — how do you decide what to ship monthly?
- How do you know 100+ people downloaded it — what are you tracking, and is that a vanity metric or does it tell you something about usage?

<!-- ### MANIT Internship / ADA-GMWL Research (expect deep, skeptical questions here — see Section 7)
- Explain a transformer architecture at a high level — what is self-attention actually doing?
- Why do you need domain adaptation here specifically — what changes between the source (Mendeley) and target (BRISC 2025) datasets?
- What does "custom loss function with five mathematical extensions" mean — pick ONE and explain the math and intuition in plain terms.
- 98.87% accuracy — accuracy on what split, what's the class balance, and why is accuracy alone not a great metric for imbalanced medical data (precision/recall/F1/AUC matter more)?
- What is Swin-Tiny, and why a Swin Transformer backbone instead of a CNN like ResNet?
- What does "manuscript in preparation" mean — is it under review anywhere, and is your name first author?
- Would you deploy this model in a real hospital as-is? Why or why not? (Good answer: no — needs external validation, regulatory clearance, clinician-in-the-loop, robustness testing across scanners.) -->

---

## Questions for Every Skill/Technology on Your Resume

**JavaScript / TypeScript**
- var vs let vs const, and closures — give an example.
- What does TypeScript actually add at compile time vs runtime (it's erased — no runtime type safety)?
- Explain the event loop and how async/await works under the hood.

**React.js**
- What is the virtual DOM and why does it help performance?
- useState vs useEffect — dependency array gotchas.
- Controlled vs uncontrolled components.
- What causes unnecessary re-renders, and how do you prevent them (memo, useCallback)?

**React Native**
- How is it different from a WebView-based hybrid app?
- What is the bridge/JSI, and why does it matter for performance?
- How do you handle platform-specific code (iOS vs Android)?

**Node.js / Express.js**
- Is Node single-threaded? Explain the event loop + libuv thread pool.
- How does Express middleware work — order of execution?
- How do you handle a CPU-heavy task without blocking the event loop?

**MongoDB**
- SQL vs NoSQL — when would you pick each?
- What is an index, and why does it speed up queries?
- Explain a document schema you designed — was it embedded or referenced, and why?

**MySQL / SQL** — ⚠️ *flagged gap: no listed project visibly uses SQL/MySQL. Expect this to be probed directly.*
- Write a query using a JOIN (be ready to literally write SQL on a whiteboard/doc).
- What's the difference between INNER JOIN, LEFT JOIN, and a subquery?
- What is normalization, and can you name 1NF/2NF/3NF in one sentence each?
- Primary key vs foreign key vs unique constraint.
- **Prep note:** if you can't point to where you used it, say so honestly and pivot to "I've studied it and used MongoDB in production-style projects, but I'd want to strengthen hands-on SQL — here's what I understand conceptually," then answer the fundamentals well. Don't claim project experience you don't have.

**Flask / Django** — ⚠️ *same flag: not clearly used in any listed project.*
- Flask vs Django — when would you pick one over the other (Flask = minimal/microframework, Django = batteries-included/ORM+admin+auth built in)?
- What is a Django model / Flask route decorator, at a basic level?
- Be ready to say plainly if these are coursework/self-study rather than project-proven.

**GraphQL** — ⚠️ *listed but no visible project usage.*
- GraphQL vs REST — over-fetching/under-fetching problem GraphQL solves.
- What is a resolver?
- Again — be honest about depth of hands-on experience here.

**REST APIs**
- What makes an API "RESTful" — statelessness, resource-based URLs, proper HTTP verbs.
- Idempotency — which HTTP methods are idempotent?
- How do you version an API?

**Firebase** — ⚠️ *listed but unclear which project used it.*
- Firestore vs Realtime Database — difference?
- What did you specifically use Firebase for? (Have a concrete, truthful answer ready.)

**Python / NumPy / Pandas / Matplotlib** (ML side)
- Why NumPy arrays over Python lists for numerical work (vectorization, memory layout)?
- How do you handle a missing/imbalanced dataset in Pandas?
- Explain one plot type in Matplotlib you used and why.

**Git & GitHub**
- git merge vs git rebase — when do you use each?
- What causes a merge conflict, and how do you resolve one?
- What's the difference between git fetch and git pull?
- How do you undo a commit that's already pushed?

---

## CS Fundamentals

### Java (you use this for DSA per your revision series — MEDIUM priority since it's not on your resume skills list, but be ready since interviewers may ask "what language do you code DSA in?")
- Why is Java "write once, run anywhere" — JVM/bytecode.
- Difference between JDK, JRE, JVM.
- What's the difference between an interface and an abstract class?
- Pass-by-value vs pass-by-reference in Java (Java is always pass-by-value, even for objects — this trips people up).

### DSA (HIGH — this is your strongest area, own it)
- Time/space complexity of your go-to approaches for arrays, strings, stacks, queues, trees.
- Explain your problem-solving process out loud for a new problem (brute force → optimize).
- Be ready to code live — this matters more than reciting theory given 950+ problems solved.

### OOP (HIGH)
- Four pillars: encapsulation, abstraction, inheritance, polymorphism — with real (not textbook) examples, ideally from your own code.
- Method overloading vs overriding.
- What is composition, and why is "favor composition over inheritance" a common principle?

### DBMS (MEDIUM-HIGH given the SQL resume gap)
- ACID properties.
- Normalization (1NF–3NF).
- Indexes — how do they work, and what's the tradeoff (faster reads, slower writes)?
- Primary key vs foreign key vs candidate key.

<!-- ### OS (MEDIUM)
- Process vs thread.
- Deadlock — four necessary conditions.
- What is a race condition, and how do you prevent one?
- Paging vs segmentation (high-level only, unless it's a systems-heavy role).

### CN (MEDIUM)
- OSI model — 7 layers, one line each.
- TCP vs UDP — when would you use each?
- What happens when you type a URL into a browser and hit enter? (Classic — DNS → TCP handshake → TLS → HTTP request → response → render.)
- HTTP vs HTTPS — what does TLS actually add? -->