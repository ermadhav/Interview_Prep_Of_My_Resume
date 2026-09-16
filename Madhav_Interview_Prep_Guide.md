# Madhav Tiwari — SDE Internship Interview Prep Guide

---

## 1. Self-Introduction (60–90 sec)

> "Hi, I'm Madhav Tiwari, a final-year B.Tech CSE student at Arya College of Engineering, Jaipur, graduating in 2027 with a CGPA of 8. My core strength is full-stack development on the MERN stack and React Native — I've built and shipped 10+ projects, including DevStreaks, a React Native app live at devstreaks.site with 100+ downloads that helps developers track their coding consistency across GitHub and LeetCode. Alongside that, I've solved 950+ DSA problems on LeetCode, sitting in the top 85K globally with a 159-day solving streak.

> More recently, I did a Machine & Deep Learning internship at MANIT Bhopal, where I built a transformer-based model to classify brain tumor types from MRI scans, designed a custom loss function to handle class imbalance, and hit 98.87% test accuracy across 20 optimizer-classifier configurations. I'm now extending that work into an original research paper on domain adaptation for medical imaging.

> I've also won Spark Hack 2026, and my team placed 4th out of 1500+ teams at Hackmol 7.0 at NIT Jalandhar. Right now, I'm looking for a software engineering internship where I can apply my full-stack and problem-solving skills to real production systems and keep growing as an engineer."

**Delivery tips:**
- Practice out loud with a timer — this should land at 70–80 seconds, not rushed.
- Lead with full-stack/SDE identity first (that's the role you're interviewing for), ML second — don't let the ML story dominate and make them doubt you want an SDE role.
- Cut "CGPA: 8" if the interviewer already has your resume in front of them — only say it if asked or if it's genuinely strong for their bar.

---

## 2. Project Deep-Dives (1–2 min each)

For each project below: use the structure, but **you must personalize the "Challenges" and "What I Learned" sections with your real, specific memories** — generic answers here are the #1 way candidates get caught. I've given you a strong scaffold; swap in the actual bug you hit, the actual late night, the actual "aha."

### A. Web Chat App (WebRTC, Node.js, React.js, Express.js, Tailwind)

**What it does:** A full-stack real-time chat and video calling platform — two people can either connect via a personal code (like a private room) or get randomly matched with a stranger, similar to Omegle but with more controls.

**Problem it solves:** Most peer-to-peer video chat demos are either too basic (no screen sharing/recording) or require a paid signaling service. This builds the full pipeline yourself — signaling, peer connection, media negotiation — end to end.

**My contribution:** Built the entire stack — the Express/Node signaling server, the React frontend, and the WebRTC peer-connection logic (offer/answer/ICE candidate exchange).

**Tech & why:**
- **WebRTC** — for direct peer-to-peer audio/video/data without routing media through your server (lower latency, lower server cost).
- **Node.js + Express** — lightweight signaling server (WebRTC needs *some* server to exchange session metadata before peers can connect directly).
- **React.js** — component-driven UI for chat + call screens.
- **Tailwind** — fast, consistent styling without hand-rolled CSS.

**Key features:** Personal-code-based private rooms, random stranger matching, screen sharing, screen recording, camera/mic toggle.

**Challenges (personalize this):** The hardest part of any WebRTC project is almost always **NAT traversal** — two peers behind different home routers can't just "find" each other; you need STUN (and sometimes TURN) servers to discover public-facing IP/port pairs, and the ICE candidate exchange has to happen reliably through your signaling server before the media connection succeeds. A common real challenge: connections working on the same network but failing across networks — that's a TURN-server gap. Be ready to explain this even if your specific fix was simpler (e.g., using a public STUN server).

**What I learned:** How real-time peer-to-peer systems are negotiated at a protocol level — signaling vs. media planes are separate concerns, and most of the "hard part" of WebRTC is session setup, not the media itself.

---

### B. ISS Live Tracker (React.js, Node.js, Express.js, Three.js, Open Notify API)

**What it does:** A 3D globe that shows the International Space Station's live position in real time, with coordinates, altitude, velocity, NASA's live video feed, and email alerts when the ISS passes near the user's location.

**Problem it solves:** Turns a plain lat/long API feed into an intuitive, visual, "you can see it moving" experience instead of raw numbers.

**My contribution:** Built the 3D globe visualization, integrated three external APIs (Open Notify, OpenCage, NASA feed), and built the location-based email alert system.

**Tech & why:**
- **Three.js / react-globe.gl** — WebGL-based 3D rendering in the browser for the globe visualization.
- **Open Notify API** — free, no-auth ISS position API (good for a side project, but be honest that it's a simple polling API, not a data-engineering feat).
- **OpenCage API** — reverse geocoding (lat/long → human-readable location).
- **Nodemailer** — server-side email sending for proximity alerts.

**Key features:** Live 3D tracking, real-time coordinates/altitude/velocity, proximity email alerts, embedded NASA live feed, Stellarium SkyView integration.

**Challenges (personalize this):** Likely candidates: keeping the globe animation smooth while polling the API on an interval (avoiding jank/memory leaks from repeated re-renders), calculating "distance from user" correctly (haversine formula on a sphere, not flat-earth math), and deciding a sensible polling interval that keeps data fresh without hammering the free API.

**What I learned:** How to compose multiple third-party APIs into one coherent product experience, and the basics of 3D rendering in the browser (camera, lighting, geo-to-3D-coordinate mapping).

---

### C. DevStreaks (React Native, TypeScript) — your strongest ownership story

**What it does:** A cross-platform mobile app (shipped, live at devstreaks.site) that unifies a developer's coding consistency — pulling GitHub contribution data and LeetCode stats into one dark-themed dashboard.

**Problem it solves:** Developers track their consistency across multiple platforms (GitHub, LeetCode) with no single view. This centralizes it.

**My contribution:** Designed and shipped the entire app solo — from data integration to UI to release — and have kept it live with monthly updates, growing to 100+ downloads.

**Tech & why:**
- **React Native + TypeScript** — one codebase for cross-platform (iOS/Android), with TypeScript for type safety across data models coming from two different external APIs (GitHub, LeetCode) that don't share a schema.

**Key features:** Unified dashboard, GitHub contribution graph, LeetCode stats, dark theme, live production deployment, ongoing monthly updates.

**Challenges (personalize this):** LeetCode has no official public API — most solutions to this scrape or use unofficial GraphQL endpoints, which can break without notice. If that's what you did, be ready to explain the tradeoff (unofficial endpoint = fast to build, but fragile — breaks if LeetCode changes their schema). Also: shipping to app stores involves real-world friction (build signing, store review, versioning) that tutorials skip.

**What I learned:** What "shipping" actually means beyond writing code — release cycles, real user feedback (100+ downloads means real people used it), and maintaining an app over months rather than abandoning it after a hackathon.

**⭐ This is your best answer to "tell me about a project you're most proud of" or "tell me about something you built end-to-end and maintained."** Lead with this when given the choice.

---

## 3. Most Likely Project Questions + Technical Follow-Ups

### General (any project)
- Walk me through your architecture — draw it if you can.
- What would you do differently if you rebuilt this today?
- What's the biggest bug you hit, and how did you debug it?
- If this had 10,000 concurrent users tomorrow, what breaks first?
- Why did you choose [X] over [alternative]?

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

### MANIT Internship / ADA-GMWL Research (expect deep, skeptical questions here — see Section 7)
- Explain a transformer architecture at a high level — what is self-attention actually doing?
- Why do you need domain adaptation here specifically — what changes between the source (Mendeley) and target (BRISC 2025) datasets?
- What does "custom loss function with five mathematical extensions" mean — pick ONE and explain the math and intuition in plain terms.
- 98.87% accuracy — accuracy on what split, what's the class balance, and why is accuracy alone not a great metric for imbalanced medical data (precision/recall/F1/AUC matter more)?
- What is Swin-Tiny, and why a Swin Transformer backbone instead of a CNN like ResNet?
- What does "manuscript in preparation" mean — is it under review anywhere, and is your name first author?
- Would you deploy this model in a real hospital as-is? Why or why not? (Good answer: no — needs external validation, regulatory clearance, clinician-in-the-loop, robustness testing across scanners.)

---

## 4. Questions for Every Skill/Technology on Your Resume

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

## 5. CS Fundamentals

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

### OS (MEDIUM)
- Process vs thread.
- Deadlock — four necessary conditions.
- What is a race condition, and how do you prevent one?
- Paging vs segmentation (high-level only, unless it's a systems-heavy role).

### CN (MEDIUM)
- OSI model — 7 layers, one line each.
- TCP vs UDP — when would you use each?
- What happens when you type a URL into a browser and hit enter? (Classic — DNS → TCP handshake → TLS → HTTP request → response → render.)
- HTTP vs HTTPS — what does TLS actually add?

### Git/GitHub (see Section 4 — already covered)

---

## 6. HR / Behavioral Questions

**"Tell me about yourself"** → Use Section 1.

**"Why do you want this internship / why us?"**
> "I want hands-on experience building and shipping production software at scale, with engineers I can learn from. I've already shipped one app solo — DevStreaks — but I know there's a big gap between a side project with 100 users and a product serving thousands, and that's exactly the kind of engineering judgment I want to build here."

**"Tell me about a time you failed / faced a challenge."**
> Use a real, specific moment — a bug that took days, a hackathon where your idea didn't work, a project that shipped late. Structure: Situation → what went wrong → what you did → what changed after. (Don't use a fake "I'm a perfectionist" non-answer — interviewers see through this immediately.)

**"Tell me about a time you worked in a team / conflict with a teammate."**
> Pull from Code Hunt 2026 (you led the platform + event) or a hackathon team. Be specific about your role vs. others'.

**"Why the switch from full-stack to ML, and which do you actually want?"**
> Be honest and clear here — this is likely to come up because your resume tells two stories. A strong answer: "My foundation and the roles I'm applying for are software engineering — the ML internship was a chance to go deep on something technically hard and prove I can pick up an unfamiliar domain fast. I'm applying for SDE roles because that's where my strongest, most consistent track record is." Don't sound unsure about what you want.

**"Where do you see yourself in 2–3 years?"**
> Keep it grounded — growing as an engineer, owning larger systems, ideally at a product company.

**"Do you have any questions for us?"** — always have 2–3 ready (about the team's stack, what an intern actually works on, how mentorship works).

---

## 7. What an Interviewer Will Likely Challenge on Your Resume

| # | Red Flag | Why it stands out | How to handle it |
|---|----------|-------------------|-------------------|
| 1 | SQL/MySQL listed, no project shows a SQL schema or query | Skills list ≠ proof | Be honest about depth; know fundamentals cold (Section 4/5) |
| 2 | Flask, Django, GraphQL listed, none appear in any listed project | Same as above, compounded — 3 unproven skills | Don't overclaim; pivot to what you *have* built |
| 3 | Firebase listed but not tied to any named project | Ambiguous | Have a specific, truthful answer for where you used it |
| 4 | 98.87% test accuracy | Sounds impressive but invites scrutiny — split? class balance? overfitting? | Know the metric story cold, not just the headline number |
| 5 | "Manuscript in preparation" | Interviewer may ask about publication status, authorship, venue | Answer plainly: it's in progress, not yet submitted/published |
| 6 | Full-stack → ML pivot | Signals possible unclear direction for an SDE role | Have a confident, consistent narrative (Section 6) |
| 7 | One internship only, rest is projects/hackathons | May get asked "why no other internships/experience" | Frame projects as equivalent real-world practice — DevStreaks is a shipped product with real users |
| 8 | DevStreaks "100+ downloads" | Small number — could be seen as low-impact | Reframe around ownership/shipping/maintenance, not scale |
| 9 | Custom loss function "with five mathematical extensions" | Vague, impressive-sounding phrase | Be ready to name and explain at least one or two extensions concretely |

---

## 8. Priority Matrix

**🔴 HIGH — spend most of your remaining prep time here**
- Self-intro delivery (practice out loud, timed)
- All 3 project deep-dives + follow-ups (especially WebRTC internals, DevStreaks data pipeline)
- MANIT internship / transformer / loss function / accuracy metric story
- DSA (your strongest card — keep sharp, don't neglect it while prepping "soft" answers)
- OOP fundamentals with real examples
- The SQL/Flask/Django/GraphQL honesty framing (Section 7, items 1–2)
- HR: "why the ML→SDE pivot" narrative

**🟡 MEDIUM — review, don't over-invest**
- DBMS (normalization, indexes, ACID) — given the SQL gap, this could get probed harder than usual
- Git/GitHub commands beyond the basics
- OS (process/thread, deadlock)
- CN (OSI, TCP/UDP, "what happens when you type a URL")
- Java basics (if asked why you use it for DSA)

**🟢 LOW — light pass, don't spend real prep time**
- Firebase specifics (unless directly asked)
- Matplotlib/NumPy details
- Full hackathon list walk-through (have 1-line summaries ready, that's enough)

---

## 9. Recommended Videos (only where they add real value)

| Topic | Video | Channel | Approx. Duration | Link |
|---|---|---|---|---|
| OOP (4 pillars, real examples) | "OOP in 6 Minutes with Real Examples!" | (indie dev channel) | ~6 min | https://www.youtube.com/watch?v=g-ZNUL96uMw |
| DBMS Normalization (1NF–3NF) | "Complete guide to Database Normalization in SQL" | YouTube tech tutorial | ~15 min | https://www.youtube.com/watch?v=rBPQ5fg_kiY |
| OSI Model | "Lec-2: Introduction to Computer Network \| OSI MODEL in easiest way" | Gate Smashers | ~15 min | https://www.youtube.com/watch?v=4D55Cmj2t-A |
| TCP/IP vs OSI | "Lec-4: TCP/IP Protocol Suite \| OSI vs TCP/IP" | Gate Smashers | ~15 min | https://www.youtube.com/watch?v=GfaHdjApnhU |
| Transformer architecture (self-attention, encoder/decoder) | "Transformer Neural Networks, Clearly Explained!!!" | StatQuest with Josh Starmer | ~36 min (longer than ideal, but the clearest one available — you only need the first ~15 min: word embedding through self-attention) | Search "StatQuest Transformer Neural Networks Clearly Explained" on YouTube |

**Note:** I didn't add videos for WebRTC signaling, Git rebase, or DSA — you clearly already have hands-on strength there (950+ problems, a working WebRTC app), and generic videos won't add much over your own experience. Spend that time rehearsing your own explanations out loud instead.

---

## Ready for the mock interview

I'll now start a strict, realistic mock interview — one question at a time. After each answer, I'll score it out of 10, tell you what was good/wrong, give you a stronger model answer, and follow up.
