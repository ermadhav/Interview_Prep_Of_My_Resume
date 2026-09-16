## Project Deep-Dives (1–2 min each)

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
