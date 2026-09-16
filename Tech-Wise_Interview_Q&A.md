## Programming Languages

### JavaScript

**1. `var` vs `let` vs `const`?**
`var` is function-scoped and hoisted with `undefined`; `let`/`const` are block-scoped and sit in a "temporal dead zone" until initialized. `const` means the binding can't be reassigned — but if it holds an object, the object's contents can still change.

**2. What is a closure?**
A function that "remembers" variables from its outer scope even after that outer function has returned. Example: a counter function that returns an inner function which increments a variable defined in the outer function — the inner function keeps access to that variable across calls.

**3. Event loop, call stack, micro/macro tasks?**
JS runs on a single call stack. Synchronous code executes there directly. Async work (timers, I/O) goes to Web APIs, and when done, callbacks go into queues — microtasks (Promises) run before macrotasks (setTimeout, I/O) after the current stack empties, on each loop tick.

**4. `==` vs `===`?**
`==` coerces types before comparing (so `'5' == 5` is true); `===` compares value and type strictly. Always prefer `===` unless you have a specific reason to coerce.

**5. `this` in JS vs arrow functions?**
Regular functions get `this` based on how they're called (call-site binding). Arrow functions don't have their own `this` — they inherit it lexically from the enclosing scope, which is why they're useful inside callbacks/class methods.

**6. Promise / async-await vs callbacks?**
Promises represent a future value with `.then`/`.catch`; `async/await` is syntactic sugar over Promises that lets async code read like synchronous code. Both solve "callback hell" (deeply nested callbacks) by flattening control flow.

**7. Event bubbling vs capturing?**
Capturing goes top-down (document → target); bubbling goes bottom-up (target → document) — bubbling is the default in most `addEventListener` calls unless you pass `{ capture: true }`.

**8. `null` vs `undefined`?**
`undefined` means a variable was declared but never assigned; `null` is an intentional "no value" assigned by a developer.

**9. Higher-order function?**
A function that takes another function as an argument or returns one — `map`, `filter`, `reduce` are classic examples I use constantly for transforming API response arrays.

**10. Prototypal inheritance?**
Objects can inherit properties/methods directly from other objects via the prototype chain, instead of classes (ES6 `class` syntax is sugar over this same prototype mechanism).

**11. [Project] Async ICE candidates in WebRTC?**
ICE candidates can arrive before or after the remote description is set, so I had to queue candidates that arrived early and apply them once the connection was ready, rather than assuming a fixed order — handled with async/await around the signaling events.

**12. Debounce/throttle — where needed?**
Debounce delays execution until input stops (e.g., a search box); throttle limits execution to once per interval (e.g., scroll handlers). In ISS Tracker, I'd throttle position-polling/rendering so the globe doesn't try to re-render faster than the API actually updates.

---

### TypeScript

**1. What does TS add beyond JS?**
Static type-checking at compile time — it catches type mismatches before runtime, but all types are erased when compiled to JS, so there's zero runtime type safety without added validation.

**2. `interface` vs `type`?**
Both describe shapes, but interfaces support declaration merging (re-opening the same interface to add fields) and are generally preferred for object shapes; `type` is more flexible for unions, intersections, and primitives.

**3. Generics?**
A way to write reusable code that works over multiple types while preserving type information — e.g., `function identity<T>(arg: T): T` returns whatever type it's given instead of losing type info to `any`.

**4. Why is `any` risky?**
It opts a value out of type-checking entirely, silently defeating the purpose of using TypeScript — overusing it is basically writing JS with extra syntax.

**5. Union types and narrowing?**
A union (`string | number`) means a value could be either type; narrowing (via `typeof`, `instanceof`, or custom type guards) lets TypeScript know which one you're dealing with in a given code branch.

**6. [Project] DevStreaks data shapes?**
GitHub and LeetCode APIs return completely different JSON shapes, so I defined separate interfaces for each and normalized both into one internal `UserStats` type before rendering — that way the UI components only ever deal with one consistent shape.

**7. Interface extension vs type intersection?**
`interface B extends A` and `type B = A & { ... }` achieve similar results for object shapes, but `extends` gives clearer error messages on conflicts, while `&` is more general-purpose (works with primitives/unions too).

**8. `strict: true`?**
Enables a bundle of stricter checks — no implicit `any`, strict null checks, strict function types — catching far more bugs at compile time than default settings.

---

### Python

**1. List vs tuple vs set vs dict?**
List: ordered, mutable. Tuple: ordered, immutable (faster, hashable). Set: unordered, unique elements, fast membership checks. Dict: key-value pairs, fast lookups by key.

**2. List comprehension?**
`[x**2 for x in range(10) if x % 2 == 0]` instead of a `for` loop with `.append()` — more concise and often faster since it's optimized internally.

**3. Mutable vs immutable?**
Lists, dicts, sets are mutable (can change in place); strings, tuples, numbers are immutable (any "change" creates a new object).

**4. `*args` / `**kwargs`?**
`*args` collects extra positional arguments into a tuple; `**kwargs` collects extra keyword arguments into a dict — used for flexible function signatures.

**5. GIL?**
The Global Interpreter Lock allows only one thread to execute Python bytecode at a time, even on multi-core machines — so threading doesn't help CPU-bound work (use multiprocessing instead), though it's fine for I/O-bound work.

**6. `is` vs `==`?**
`is` checks identity (same object in memory); `==` checks value equality. Two equal-value lists are `==` but not `is` unless they're literally the same object.

**7. Decorators?**
A function that wraps another function to extend its behavior without modifying it — e.g., `@timer` to log how long a function takes. I'd tie this to any logging/timing utilities used in the ML pipeline if applicable.

**8. [Project] Why Python for ML?**
Because of the ecosystem — NumPy/Pandas for data handling, PyTorch/TensorFlow for model building, and a huge community of prebuilt architectures (like Swin Transformer implementations) to build on instead of writing everything from scratch.

---

## Frontend

### React.js

**1. Virtual DOM?**
React keeps an in-memory representation of the UI, diffs it against the previous version when state changes, and only patches the real DOM where things actually changed — much cheaper than re-rendering the whole page.

**2. `useState` vs `useEffect`, dependency array?**
`useState` holds component state; `useEffect` runs side effects (data fetching, subscriptions) after render. The dependency array controls when it re-runs — empty array = once on mount, omitted = every render, specific values = re-run only when those change.

**3. Preventing unnecessary re-renders?**
`React.memo` skips re-rendering a component if props haven't changed; `useCallback` memoizes functions so they aren't recreated each render (avoiding breaking `memo` on children); `useMemo` memoizes expensive computed values.

**4. Controlled vs uncontrolled components?**
Controlled: form input value is driven by React state (`value` + `onChange`). Uncontrolled: the DOM holds its own state, accessed via a `ref` when needed. Controlled is more common in React apps for validation/consistency.

**5. Props vs state?**
Props are passed in from a parent and read-only inside the child; state is local and owned by the component itself, and changing it triggers a re-render.

**6. Lifting state up?**
Moving shared state to the closest common ancestor of components that need it, then passing it down via props — avoids duplicated/out-of-sync state.

**7. Component lifecycle (hooks)?**
Mount → `useEffect` with empty deps runs once. Update → effects with matching deps re-run. Unmount → the cleanup function returned from `useEffect` runs (e.g., clearing intervals, unsubscribing).

**8. Keys in lists?**
Keys let React track which items changed/added/removed between renders efficiently — using array index as a key can cause bugs if the list reorders, so a stable unique ID is preferred.

**9. Context vs prop drilling?**
Prop drilling passes data through many intermediate components that don't need it. `useContext` lets deeply nested components read shared state directly — useful for things like theme or auth state.

**10. [Project] Web Chat App state management?**
Connection/call state (peer connection, media streams, call status) was managed with local component state and lifted to the top-level call component, with context if multiple screens needed the same connection info — kept it simple rather than pulling in Redux for a project this size.

**11. [Project] ISS Tracker rendering efficiency?**
I throttled how often new position data triggers a re-render of the globe (matching the API's actual update frequency) rather than re-rendering on every animation frame, and kept the heavy Three.js scene setup outside React's render cycle.

---

### React Native

**1. vs WebView-based hybrid apps?**
React Native renders actual native UI components (not a webview), so it gets native performance and look-and-feel, while write-once-run-anywhere frameworks like Cordova render HTML inside a WebView, which feels and performs like a website.

**2. Bridge / JSI?**
The old architecture used an async "bridge" (JSON messages) between JS and native code, which could bottleneck under heavy UI updates. The newer JSI (JavaScript Interface) allows more direct, synchronous communication for better performance.

**3. Platform-specific code?**
`Platform.OS === 'ios'` checks, or separate `Component.ios.js` / `Component.android.js` files that React Native automatically picks based on platform.

**4. Styling differences from web?**
No CSS cascade/inheritance by default, Flexbox is the default layout model (not block/inline), and units are unitless numbers instead of px/em.

**5. `FlatList` vs mapping with `View`s?**
`FlatList` only renders items currently visible on screen (virtualization), so it stays performant for long lists; mapping a big array into `View`s renders everything at once, which can crash or lag on large datasets.

**6. [Project] DevStreaks long contribution history?**
Used `FlatList` (or a virtualized scroll component) for the contribution/stats list so only visible items render, keeping scroll performance smooth even with a full year of GitHub data.

**7. [Project] Shipping DevStreaks?**
Built with Expo (or bare React Native — be specific to what you actually did), went through build signing for the target store, and handled versioning across the monthly update cycle — plus store review requirements each release.

**8. Async data + loading states?**
Track a loading boolean (or use a data-fetching library's built-in status), show a spinner/skeleton while `true`, and handle the error case separately from the empty-data case.

---

### Tailwind CSS

**1. Utility-first vs custom CSS?**
Utility classes (`flex`, `p-4`, `text-lg`) let you style directly in markup without switching files or naming classes — faster iteration, smaller CSS bundle since only used utilities ship.

**2. Responsive design?**
Breakpoint prefixes like `md:`, `lg:` apply a utility only above that screen width — e.g., `flex-col md:flex-row` stacks on mobile, rows on desktop.

**3. Criticism and fix?**
Class strings get long and can hurt readability; fixed by extracting repeated patterns into components, or using `@apply` in a CSS file to bundle utilities under one class name.

**4. [Project] Dark mode?**
Tailwind's `dark:` variant applies styles when dark mode is active (via a class or media query strategy) — used for DevStreaks' dark-themed dashboard.

---

## Backend & Frameworks

### Node.js

**1. Single-threaded?**
The main JS execution is single-threaded via the event loop, but Node uses libuv's thread pool under the hood for things like file I/O and some crypto operations — so it's not purely single-threaded at the system level.

**2. CPU-heavy tasks without blocking?**
Offload to worker threads (`worker_threads` module) or a separate process/queue (e.g., a job queue), since a long synchronous computation on the main thread blocks all other requests.

**3. Middleware?**
Functions that run between receiving a request and sending a response — they can modify `req`/`res`, end the cycle, or call `next()` to pass control to the next middleware.

**4. Callback hell fix?**
Promises flatten nested callbacks into chainable `.then()` calls, and `async/await` flattens it further into linear, synchronous-looking code with normal try/catch error handling.

**5. `require` vs `import`?**
`require` is CommonJS (synchronous, Node's original module system); `import` is ES Modules (can be async, supports tree-shaking) — Node supports both now depending on config (`type: "module"` or `.mjs`).

**6. Environment variables?**
Loaded via `process.env` (often with a `.env` file and a package like `dotenv`) — keeps secrets like API keys out of source code and lets config differ between dev/prod.

**7. [Project] Signaling server role?**
Correct — it never touches actual audio/video/data; it only relays session-setup metadata (SDP offers/answers, ICE candidates) between the two peers so they can establish a direct connection. Once connected, media flows peer-to-peer, not through the server.

---

### Express.js

**1. Middleware chaining / `next()`?**
Each middleware function receives `(req, res, next)`; calling `next()` passes control to the next matching middleware/route handler in the chain, or `next(err)` skips to error-handling middleware.

**2. Global error handling?**
A special error-handling middleware with 4 parameters `(err, req, res, next)` placed at the end of the middleware stack catches errors passed via `next(err)` or thrown in async handlers (with a wrapper, since Express doesn't auto-catch async errors by default).

**3. `app.use()` vs `app.get()/post()`?**
`app.use()` applies to all HTTP methods on a path (or globally if no path given) — used for things like body parsing, logging, auth checks. `app.get()/post()` are specific to that HTTP verb and route.

**4. Structuring routes?**
Split routes into separate router files (`express.Router()`) per resource, with controller functions handling logic separately from route definitions — keeps `app.js` thin.

**5. [Project] WebRTC signaling setup?**
Used WebSocket events (e.g., via `socket.io`) rather than plain REST for signaling, since signaling needs low-latency, bidirectional, real-time message passing (offer/answer/ICE candidates) that a request-response REST call isn't suited for.

---

### Flask ⚠️

**1. Route decorator?**
`@app.route('/path')` maps a URL pattern to a Python function that handles requests to it — Flask calls that function when a matching request arrives.

**2. Flask vs Django?**
Flask is a minimal "microframework" — you add only what you need (routing, then bring your own ORM/auth). Django is "batteries-included" with a built-in ORM, admin panel, and auth system out of the box. Pick Flask for small/flexible APIs, Django for larger apps needing structure fast.

**3. Handling request data?**
`request.args` for query params, `request.form` for form data, `request.json` for JSON bodies.

**4. Dev server in production?**
Flask's built-in server is single-threaded and not hardened for production traffic/security — production deployments use a WSGI server like Gunicorn behind a reverse proxy like Nginx.

*(Honest framing: "I've studied Flask's fundamentals but haven't shipped a project on it — my backend experience is strongest in Node/Express.")*

---

### Django ⚠️

**1. ORM?**
Lets you interact with the database using Python classes/objects instead of raw SQL — Django translates model queries (`User.objects.filter(...)`) into SQL automatically.

**2. Models and migrations?**
A model is a Python class mapping to a database table; migrations are auto-generated files that track schema changes over time so you can apply/roll back database structure changes safely.

**3. What Django gives out of the box?**
Admin panel, authentication system, ORM, form handling, and a defined project structure — much more than Flask provides by default.

**4. MVT vs MVC?**
Django calls it Model-View-Template: Model = data layer, Template = presentation (like a "view" in MVC), and Django's "View" is actually more like a controller — it's the same pattern with different naming.

*(Same honest framing as Flask.)*

---

### GraphQL ⚠️

**1. Problem it solves?**
REST often over-fetches (returns more fields than needed) or under-fetches (needs multiple round trips for related data). GraphQL lets the client specify exactly the fields/shape it wants in a single request.

**2. Resolver?**
A function that knows how to fetch the data for a specific field in the schema — when a query asks for `user.posts`, a resolver defines how to actually get those posts.

**3. Query vs mutation?**
Query reads data (like GET); mutation changes data (like POST/PUT/DELETE) — both go through the same single GraphQL endpoint.

**4. Versioning?**
GraphQL generally avoids versioning by evolving the schema — adding new fields is non-breaking, and deprecated fields are marked rather than removed abruptly.

*(Honest framing: "I understand GraphQL conceptually but all my shipped projects use REST — that's the tradeoff I've worked with hands-on.")*

---

### REST APIs

**1. What makes an API RESTful?**
Statelessness (no client session stored server-side between requests), resource-based URLs (`/users/1` not `/getUser?id=1`), and correct use of HTTP verbs (GET/POST/PUT/DELETE) matching their semantics.

**2. Idempotent methods?**
GET, PUT, DELETE are idempotent (repeating them has the same effect as doing it once); POST is not (repeating it can create duplicates).

**3. Status codes?**
200 success, 201 created, 400 bad request, 401 unauthorized, 404 not found, 500 server error — knowing these cold signals real API experience.

**4. Versioning approach?**
Common approaches: URL versioning (`/v1/users`), header-based versioning, or query param versioning — URL versioning is simplest and most common for smaller APIs.

**5. [Project] REST vs real-time in Web Chat App?**
Any setup/auth-style operations (like generating a personal room code) could go through REST endpoints, while the actual signaling exchange (offer/answer/ICE candidates) runs over WebSocket events since it needs to be real-time and bidirectional.

---

## Databases

### MongoDB

**1. SQL vs NoSQL, when to choose?**
SQL (relational) is best for structured data with clear relationships and where strong consistency/joins matter (e.g., financial records). NoSQL (like MongoDB) is best for flexible/evolving schemas and read-heavy, document-shaped data — e.g., user profiles or chat messages.

**2. Document/collection mapping?**
A document is like a row (but nested/flexible JSON-like structure); a collection is like a table (a group of documents).

**3. Embedding vs referencing?**
Embed when data is always accessed together and doesn't grow unbounded (e.g., a user's address inside their profile). Reference (store an ID, look up separately) when data is shared across documents or grows large (e.g., a user's full message history).

**4. Indexes — benefit and tradeoff?**
Indexes speed up reads by avoiding full collection scans, but every write now has to also update the index, so heavy-write collections need indexes chosen carefully.

**5. Is MongoDB ACID?**
Yes for single-document operations by default; multi-document transactions are supported since MongoDB 4.0 but come with more overhead, so schema design often avoids needing them.

**6. [Project] Embed or reference messages?**
I'd reference messages in a separate collection rather than embed them inside a room document, since a room's message history can grow unbounded and MongoDB documents have a 16MB size limit — embedding would eventually break.

---

### MySQL / SQL ⚠️

**1. Find duplicate rows?**
`SELECT column, COUNT(*) FROM table GROUP BY column HAVING COUNT(*) > 1;` — groups rows by the column and filters to groups appearing more than once.

**2. INNER JOIN vs LEFT JOIN vs subquery?**
INNER JOIN returns only matching rows in both tables. LEFT JOIN returns all rows from the left table plus matches from the right (NULLs where no match). A subquery nests one query inside another — useful when you need a computed value or filtered set before the main query runs.

**3. Normalization forms?**
1NF: atomic values, no repeating groups. 2NF: 1NF + no partial dependency on part of a composite key. 3NF: 2NF + no transitive dependency (non-key columns depend only on the key, not on each other).

**4. Primary vs foreign vs unique key?**
Primary key uniquely identifies a row in its own table. Foreign key references a primary key in another table to enforce relationships. Unique constraint just ensures no duplicate values in a column, without being the row's identifier.

**5. Index and B-Tree?**
An index is a separate sorted data structure (commonly a B-Tree) pointing to row locations, so lookups can binary-search instead of scanning every row — turns an O(n) scan into roughly O(log n).

**6. ACID?**
Atomicity (all-or-nothing), Consistency (valid state to valid state), Isolation (concurrent transactions don't interfere), Durability (committed data survives a crash).

**7. GROUP BY / HAVING / WHERE order?**
Execution order is roughly: FROM → WHERE (filters rows) → GROUP BY (groups them) → HAVING (filters groups) → SELECT → ORDER BY. `WHERE` can't filter on aggregate results; `HAVING` can.

**8. Transaction / COMMIT / ROLLBACK?**
A transaction bundles multiple statements into one atomic unit; `COMMIT` saves all changes permanently, `ROLLBACK` undoes everything in the transaction if something failed partway through.

*(Honest framing if pushed on hands-on project use: "My database experience in shipped projects is MongoDB — my SQL knowledge is solid conceptually and from coursework, but I'd want to be upfront that I haven't built a production SQL schema yet.")*

---

### Firebase ⚠️

**1. Firestore vs Realtime Database?**
Firestore is document/collection-based with richer querying and better scaling; Realtime Database is a single large JSON tree, simpler but harder to query and scale for complex data.

**2. Firebase Auth?**
Handles user sign-up/login (email/password, OAuth providers like Google) and issues tokens the backend can verify, without you building auth infrastructure from scratch.

**3. Security rules?**
Server-side rules defining who can read/write which documents — critical because Firebase clients talk directly to the database, so without rules, any client could read/write anything.

**4. Specific use in your work?**
*(Answer with a real, specific detail here — this is the question they'll actually ask; a vague answer here is worse than saying you used it minimally for one specific feature.)*

---

## Data & Libraries

### NumPy

**1. Why NumPy over lists?**
NumPy arrays are stored in contiguous memory and operations are vectorized (run in optimized C code), so they're much faster than looping over Python lists for numerical work.

**2. Broadcasting?**
NumPy automatically expands smaller arrays to match the shape of larger ones during arithmetic (e.g., adding a scalar to every element of an array) without explicitly writing loops.

**3. Element-wise vs matrix multiply?**
`*` multiplies element-by-element (shapes must match or broadcast); `@` or `np.dot()` performs actual matrix multiplication following linear algebra rules.

---

### Pandas

**1. Series vs DataFrame?**
A Series is a single labeled 1D array (like one column); a DataFrame is a 2D table of Series (like a spreadsheet).

**2. Handling missing data?**
`dropna()` removes rows/columns with missing values; `fillna()` replaces them with a value, mean, median, or forward/backward fill depending on the context.

**3. [Project] Class imbalance handling?**
Used Pandas to inspect class distribution across MRI tumor categories, then addressed the imbalance through techniques like weighted sampling or the custom loss function's class-weighting terms, rather than naively duplicating minority-class samples.

**4. `loc` vs `iloc`?**
`loc` selects by label (row/column names); `iloc` selects by integer position — easy to mix up, worth being precise about in an interview.

---

### Matplotlib

**1. Visualizing model performance?**
Plotted training/validation accuracy and loss curves per epoch to check for overfitting (validation loss rising while training loss falls), and a confusion matrix to see per-class performance across tumor types.

**2. `plot()` vs `scatter()`?**
`plot()` draws connected lines (good for continuous trends like loss curves over epochs); `scatter()` draws unconnected points (good for showing individual data points or relationships between two variables without implying order).

---

## Core CS Concepts

### Data Structures & Algorithms

**1. Time/space complexity basics?**
Array: O(1) index access, O(n) search/insert-in-middle. Linked list: O(n) search, O(1) insert/delete at known node. Stack/queue: O(1) push/pop. Hash map: O(1) average lookup/insert. Balanced tree: O(log n) search/insert.

**2. Hash map vs tree for lookups?**
Hash map when you just need fast key-based lookup with no ordering requirement (O(1) average). Tree (like a BST) when you need sorted order, range queries, or predictable worst-case behavior (O(log n) if balanced).

**3. BFS vs DFS?**
BFS explores level by level (uses a queue) — good for shortest path in unweighted graphs. DFS explores as deep as possible before backtracking (uses a stack/recursion) — good for exploring all paths, cycle detection, topological sort.

**4. Sliding window signal?**
Used for problems about contiguous subarrays/substrings with a condition (max sum of size k, longest substring without repeats) — lets you avoid recomputing from scratch by adding/removing one element as the window slides.

**5. Recursion vs iteration?**
Recursion is often more readable for naturally recursive problems (trees, divide-and-conquer) but risks stack overflow on deep recursion and has function-call overhead; iteration avoids that but can be less intuitive to write/read for the same logic.

**6. Problem-solving process?**
Clarify constraints and edge cases out loud → state a brute-force approach and its complexity → identify the bottleneck → think about what data structure or technique removes that bottleneck → code it, talking through each step, then test with an example.

---

### Object-Oriented Programming (OOP)

**1. Four pillars with real examples?**
Encapsulation: a class exposes methods but hides internal state (e.g., a `User` class exposing `login()` rather than letting you touch a raw password field). Abstraction: hiding complex implementation behind a simple interface (e.g., calling `fetchData()` without knowing the HTTP details underneath). Inheritance: a `AdminUser` class extending a base `User` class to reuse shared behavior. Polymorphism: different classes implementing the same method differently (e.g., a `render()` method that behaves differently for a `TextMessage` vs `ImageMessage` class).

**2. Overloading vs overriding?**
Overloading: same method name, different parameters, in the same class (compile-time). Overriding: a subclass redefines a method inherited from a parent class (runtime).

**3. Composition over inheritance?**
Composition builds objects by combining smaller, focused objects ("has-a") rather than deep inheritance chains ("is-a"), which keeps code more flexible and avoids fragile hierarchies that break when a shared parent changes.

**4. Interface vs abstract class?**
An interface only declares method signatures (no implementation, in most languages); an abstract class can have some implemented methods and some abstract ones, and supports shared state — use an interface for a pure contract, abstract class when sharing partial implementation.

**5. Constructors, multiple?**
A constructor initializes a new object's state. Many languages (Java, C++) support multiple constructors via overloading (different parameter lists); JS/Python typically only allow one, using default parameters instead.

---

### Git & GitHub

**1. `merge` vs `rebase`?**
`merge` creates a new commit joining two branch histories, preserving full history including all side branches. `rebase` replays your commits on top of another branch's tip, creating a linear history — cleaner history, but rewrites commit hashes (risky on shared/pushed branches).

**2. Merge conflicts?**
Happens when two branches change the same lines differently. Git marks the conflicting sections in the file; you manually edit to resolve, then `git add` the resolved file and continue/commit.

**3. `fetch` vs `pull`?**
`fetch` downloads new commits/branches from the remote but doesn't change your working branch. `pull` = `fetch` + `merge` (or rebase, depending on config) into your current branch automatically.

**4. Undoing a pushed commit?**
`git revert <commit>` creates a new commit that undoes the changes, safe for shared branches. `git reset --hard` rewrites history and should generally be avoided on branches others have already pulled, since it can cause conflicts for collaborators.

**5. Detached HEAD?**
Happens when you check out a specific commit (not a branch) — any new commits you make aren't attached to a branch and can be lost unless you create a branch from that point before switching away.

**6. [Project] Branching workflow?**
Even solo, using feature branches per project/feature and merging into `main` via PRs (even self-reviewed) keeps history organized and makes it easy to roll back a bad feature without touching stable code — worth describing your actual habit here.

**7. `.gitignore`?**
Lists files/patterns Git should never track — `node_modules/`, `.env`, build artifacts — keeps the repo clean and prevents accidentally committing secrets or huge generated folders.