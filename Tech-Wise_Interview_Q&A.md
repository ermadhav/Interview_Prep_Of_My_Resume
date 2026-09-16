# Interview Q&A — Simple Language Version

## JavaScript

Q1 :- What is the difference between var, let and const?

Ans :- var is old and can cause bugs because it doesn't respect blocks like if/for. let and const are newer and safer — let can be changed later, const cannot be reassigned.

Q2 :- What is a closure?

Ans :- It's when a function remembers the variables from where it was created, even after that outer function has finished running. Example: a counter function that keeps increasing a number every time you call it.

Q3 :- Explain the event loop.

Ans :- JavaScript runs one thing at a time. Slow tasks like API calls go aside and come back later as a callback. The event loop keeps checking: "is the main code done? ok now run the waiting tasks."

Q4 :- == vs ===?

Ans :- == checks value only and converts types if needed. === checks both value and type. Always use === to avoid confusing bugs.

Q5 :- What is "this" in JavaScript?

Ans :- "this" refers to whoever called the function. In a normal function it can change depending on how it's called. In an arrow function, "this" stays the same as the surrounding code.

Q6 :- What are Promises and async/await?

Ans :- A Promise is a placeholder for a value you'll get later (like an API response). async/await is a cleaner way to write Promise code so it looks like normal step-by-step code instead of messy chains.

Q7 :- What is event bubbling?

Ans :- When you click something inside a page, the click event travels upward through its parent elements too, unless you stop it.

Q8 :- null vs undefined?

Ans :- undefined means a variable exists but has no value yet. null means someone deliberately set it to "nothing."

Q9 :- What is a higher-order function?

Ans :- A function that takes another function as input or gives one back. map, filter, and reduce are common examples.

Q10 :- [Project] How did you handle things happening at different times in your WebRTC app?

Ans :- Sometimes connection info arrived before the app was ready for it, so I stored it temporarily and used it once the connection was ready, instead of assuming everything would arrive in order.

---

## TypeScript

Q1 :- Why use TypeScript over JavaScript?

Ans :- It checks for mistakes (like using the wrong data type) before you even run the code, which catches bugs early. But once it compiles to JavaScript, those checks disappear.

Q2 :- interface vs type?

Ans :- Both describe the shape of data. interface is mostly used for objects and can be extended later. type is more flexible and can describe things like unions (A or B).

Q3 :- What is a generic?

Ans :- A way to write one function that works for many data types, instead of writing the same function separately for numbers, strings, etc.

Q4 :- Why avoid using "any"?

Ans :- "any" turns off type checking completely for that value, so you lose the whole benefit of using TypeScript.

Q5 :- [Project] Why was TypeScript useful in DevStreaks?

Ans :- GitHub data and LeetCode data look completely different. TypeScript helped me define clear shapes for both, so I didn't accidentally mix up fields while building the dashboard.

---

## Python

Q1 :- List vs tuple vs set vs dict?

Ans :- List: ordered, can change. Tuple: ordered, can't change. Set: no duplicates, no order. Dict: key-value pairs, fast lookup by key.

Q2 :- What is a list comprehension?

Ans :- A short one-line way to build a list, instead of writing a full for-loop. Example: [x*2 for x in numbers].

Q3 :- What does mutable/immutable mean?

Ans :- Mutable means you can change it after creating it (like a list). Immutable means once created, it can't change (like a string or tuple).

Q4 :- What are *args and **kwargs?

Ans :- They let a function accept any number of extra inputs — *args for normal values, **kwargs for named values.

Q5 :- What is the GIL?

Ans :- It's a lock in Python that only lets one piece of code run at a time, even with multiple threads. So threads don't help speed up heavy calculations — you need multiprocessing for that.

Q6 :- [Project] Why is Python used for machine learning?

Ans :- Because it has ready-made libraries like NumPy, Pandas, and PyTorch that make it easy to handle data and build models without writing everything from scratch.

---

## React.js

Q1 :- What is the virtual DOM?

Ans :- React keeps a lightweight copy of the webpage in memory. When something changes, it compares the copy with the last version and only updates the parts of the real webpage that actually changed. This makes it fast.

Q2 :- useState vs useEffect?

Ans :- useState stores data that can change. useEffect runs some code after the component shows up on screen (like fetching data), and it can also run again when certain values change.

Q3 :- How do you stop unnecessary re-renders?

Ans :- Use React.memo to skip re-rendering if the props didn't change, and useCallback/useMemo to avoid recreating functions or values on every render.

Q4 :- Controlled vs uncontrolled components?

Ans :- Controlled: the input's value is stored in React state, and React fully controls it. Uncontrolled: the browser keeps the value itself, and you only check it when needed using a ref.

Q5 :- Props vs state?

Ans :- Props are passed down from a parent and can't be changed by the child. State is owned by the component itself and can change over time.

Q6 :- Why do lists need "keys" in React?

Ans :- Keys help React know which item is which when the list changes, so it updates efficiently instead of re-rendering everything.

Q7 :- [Project] How did you manage state in your Web Chat App?

Ans :- I kept the call/connection status in the component that handles the call, and shared it with child components using props or context — didn't need anything heavier like Redux for this size of app.

---

## React Native

Q1 :- How is React Native different from a WebView app?

Ans :- React Native builds real native screens and buttons, so it feels and performs like a real app. A WebView app is basically a website wrapped inside an app, so it feels less smooth.

Q2 :- What is the "bridge" in React Native?

Ans :- It's the connector that lets your JavaScript code talk to the native phone code (camera, storage, etc). Newer versions use something faster called JSI.

Q3 :- How do you write different code for iOS and Android?

Ans :- You can check Platform.OS in your code, or create separate files like Component.ios.js and Component.android.js — React Native picks the right one automatically.

Q4 :- FlatList vs mapping a normal array?

Ans :- FlatList only renders what's visible on screen, so long lists stay smooth. Mapping a big array directly renders everything at once, which can make the app slow or crash.

Q5 :- [Project] How did you handle long lists in DevStreaks?

Ans :- Used FlatList for the stats/contribution list so only the visible part loads at once, keeping scrolling smooth even with a lot of data.

---

## Tailwind CSS

Q1 :- What is utility-first CSS?

Ans :- Instead of writing custom CSS classes, you use small ready-made classes directly in your HTML/JSX, like p-4 for padding or flex for flexbox. It's faster to build with.

Q2 :- How do you make a page responsive in Tailwind?

Ans :- You add prefixes like md: or lg: before a class, so it only applies on bigger screens. Example: flex-col md:flex-row.

Q3 :- [Project] How did you do dark mode in DevStreaks?

Ans :- Tailwind has a dark: prefix — you add dark: before a class and it only applies when dark mode is turned on.

---

## Node.js

Q1 :- Is Node.js single-threaded?

Ans :- Mostly yes for running your JavaScript code, but behind the scenes it uses a thread pool for things like file reading, so it's not 100% single-threaded internally.

Q2 :- How do you handle a heavy task without freezing the server?

Ans :- Move it to a separate worker thread or background process, so it doesn't block the main thread from handling other requests.

Q3 :- What is middleware?

Ans :- Code that runs in between a request coming in and the final response going out — used for things like checking login, logging, or reading request data.

Q4 :- [Project] What does your signaling server actually do?

Ans :- It doesn't touch the actual video or audio at all. It just helps two users' apps exchange connection information so they can talk to each other directly. After that, the server isn't involved in the call itself.

---

## Express.js

Q1 :- How does middleware chaining work?

Ans :- Each middleware function can either handle the request or call next() to pass it to the next one in line, like a chain of checkpoints.

Q2 :- How do you handle errors in Express?

Ans :- You write a special error-handling function at the end with 4 parameters (err, req, res, next), and pass errors to it using next(err).

Q3 :- app.use() vs app.get()?

Ans :- app.use() runs for every type of request (or a whole route section). app.get() only runs for GET requests on a specific route.

---

## Flask ⚠️ (be honest — no project uses this directly)

Q1 :- What does @app.route do?

Ans :- It connects a URL to a function, so when someone visits that URL, Flask runs that function.

Q2 :- Flask vs Django?

Ans :- Flask is lightweight — you add only what you need. Django comes with a lot built in already, like login system and admin panel. Flask is good for small/simple APIs, Django for bigger apps.

Q3 :- Why not use Flask's default server in production?

Ans :- It's made for testing, not for handling real traffic safely or quickly. Real apps use something like Gunicorn instead.

Honest answer if asked where you used it: "I know the basics from studying it, but I haven't shipped a project with Flask — my backend work has mainly been in Node and Express."

---

## Django ⚠️

Q1 :- What is Django's ORM?

Ans :- It lets you work with the database using Python code instead of writing raw SQL. Django turns your Python code into SQL behind the scenes.

Q2 :- What is a Django model?

Ans :- A Python class that represents a database table — each field in the class becomes a column.

Q3 :- What does Django give you that Flask doesn't?

Ans :- A ready-made admin panel, login system, and database tools — you don't have to build these yourself.

Honest answer: same as Flask — mention it's understood conceptually, not project-tested.

---

## GraphQL ⚠️

Q1 :- What problem does GraphQL solve?

Ans :- With normal REST APIs you sometimes get more data than you need, or need multiple requests to get everything. GraphQL lets you ask for exactly the fields you want in one request.

Q2 :- What is a resolver?

Ans :- A function that tells GraphQL how to actually fetch the data for a specific field when it's requested.

Q3 :- Query vs mutation?

Ans :- Query is for reading data. Mutation is for changing data (adding, updating, deleting).

Honest answer: "I understand GraphQL in theory, but all my real projects use REST APIs."

---

## REST APIs

Q1 :- What makes an API "RESTful"?

Ans :- It uses clear URLs for resources (like /users/5) and uses the right HTTP method for the right action — GET to read, POST to create, PUT to update, DELETE to remove.

Q2 :- What does "idempotent" mean?

Ans :- Doing the same request multiple times gives the same result as doing it once. GET, PUT, DELETE are idempotent. POST usually isn't (it can create duplicates).

Q3 :- Common HTTP status codes?

Ans :- 200 = success, 201 = created, 400 = bad request from client, 401 = not logged in/unauthorized, 404 = not found, 500 = server broke.

---

## MongoDB

Q1 :- SQL vs NoSQL — when to use which?

Ans :- Use SQL when your data has clear, fixed relationships and needs strict consistency (like banking data). Use NoSQL (MongoDB) when your data structure can change often and you need flexibility and speed, like chat messages or user profiles.

Q2 :- What is a document and a collection?

Ans :- A document is like one record (similar to a row in SQL) but stored as flexible JSON-like data. A collection is a group of documents (similar to a table).

Q3 :- Embedding vs referencing data?

Ans :- Embed data if it's always used together and won't grow too big (like a user's address inside their profile). Reference (link by ID) if the data is shared or can grow a lot (like all of a user's messages).

Q4 :- What is an index and its downside?

Ans :- An index makes searching faster by organizing data for quick lookup. The downside is that every time you add or change data, the index also has to update, which slows down writes a little.

Q5 :- [Project] Would you embed or store chat messages separately?

Ans :- I'd store messages in their own collection instead of putting them inside the room's document, because a room's chat history can grow very large, and MongoDB documents have a size limit.

---

## MySQL / SQL ⚠️ (biggest resume gap — know this section well)

Q1 :- How do you find duplicate rows in a table?

Ans :- Group the rows by the column you're checking, then only keep groups where the count is more than 1: SELECT column, COUNT(*) FROM table GROUP BY column HAVING COUNT(*) > 1.

Q2 :- What is the difference between INNER JOIN and LEFT JOIN?

Ans :- INNER JOIN only shows rows that match in both tables. LEFT JOIN shows all rows from the first table, and fills in empty (NULL) values if there's no match in the second table.

Q3 :- What is normalization? (1NF, 2NF, 3NF simply)

Ans :- It's organizing a database to avoid repeating the same data everywhere. 1NF: no mixed/multiple values in one cell. 2NF: every column depends on the whole key, not just part of it. 3NF: no column depends on another non-key column.

Q4 :- Primary key vs foreign key?

Ans :- A primary key uniquely identifies each row in its own table. A foreign key is a column that points to a primary key in another table, connecting the two tables.

Q5 :- What is an index in simple terms?

Ans :- It's like the index at the back of a book — instead of reading every page to find something, you jump straight to it. It makes searching much faster.

Q6 :- What are ACID properties?

Ans :- Atomicity (all steps happen or none do), Consistency (data stays valid), Isolation (transactions don't mess with each other), Durability (once saved, it's saved even if the system crashes).

Q7 :- What is a transaction?

Ans :- A group of database operations treated as one unit — either all of them succeed together (COMMIT) or none of them happen (ROLLBACK).

Honest answer if pushed: "My real project experience is with MongoDB. I know SQL well conceptually and from coursework, but I haven't built a production project on it yet."

---

## Firebase ⚠️

Q1 :- Firestore vs Realtime Database?

Ans :- Firestore organizes data into documents and collections and is easier to search/filter. Realtime Database is one big tree of JSON data — simpler but harder to query for complex apps.

Q2 :- How does Firebase Authentication work?

Ans :- It handles user sign-up and login for you (email/password, Google login, etc.) and gives you a token to confirm who the user is, so you don't have to build login from scratch.

Q3 :- What are Firebase security rules?

Ans :- Rules that control who can read or write specific data. Important because in Firebase, the app talks directly to the database, so without rules anyone could access anything.

Q4 :- Where exactly did you use Firebase?

Ans :- (Answer honestly with the real, specific place you used it — this will likely be asked directly.)

---

## NumPy / Pandas / Matplotlib

Q1 :- Why use NumPy instead of normal Python lists?

Ans :- NumPy is much faster for number-crunching because it stores data efficiently and does calculations on the whole array at once instead of looping one by one.

Q2 :- What is broadcasting in NumPy?

Ans :- It lets you do math between arrays of different sizes by automatically "stretching" the smaller one to match — like adding one number to every value in a big list without writing a loop.

Q3 :- Series vs DataFrame in Pandas?

Ans :- A Series is a single column of data. A DataFrame is a full table made of many Series (columns) together.

Q4 :- How do you handle missing data in Pandas?

Ans :- You can drop the missing rows (dropna) or fill them in with a value like the average (fillna).

Q5 :- [Project] How did you handle the imbalanced MRI dataset?

Ans :- I checked how many samples each tumor category had using Pandas, then handled the imbalance through the model's loss function (giving more weight to rare classes) rather than just copying data around.

Q6 :- What is Matplotlib used for in your project?

Ans :- I used it to plot accuracy and loss over training epochs, to check if the model was learning well or overfitting, and to show a confusion matrix of results per class.

---

## Data Structures & Algorithms

Q1 :- What are the basic time complexities I should know?

Ans :- Array: O(1) to access by index, O(n) to search. Linked list: O(n) to search. Hash map: O(1) average lookup. Balanced tree: O(log n) search. Stack/Queue: O(1) push/pop.

Q2 :- When do you use a hash map vs a tree?

Ans :- Hash map when you just need fast lookup and don't care about order. Tree when you need sorted data or range-based searches.

Q3 :- BFS vs DFS?

Ans :- BFS explores level by level, good for finding the shortest path. DFS goes as deep as possible first, good for exploring all possibilities or detecting cycles.

Q4 :- What is the sliding window technique?

Ans :- Instead of recalculating everything for every subarray, you keep a "window" and just add/remove one element as it moves — much faster for problems about continuous subarrays.

Q5 :- How do you approach a new coding problem?

Ans :- First understand the problem and edge cases out loud. Then think of the simplest (brute-force) way to solve it. Then look for the slow part and think how to speed it up using a better data structure or technique. Then code it while explaining each step.

---

## OOP (Object-Oriented Programming)

Q1 :- Explain the 4 pillars of OOP simply.

Ans :- Encapsulation: hide the internal details, only expose what's needed (like a class only allowing login() instead of directly touching the password). Abstraction: hide complexity behind a simple action (calling one function instead of knowing all the steps inside). Inheritance: one class reusing another class's features (AdminUser reusing User's code). Polymorphism: same function name behaving differently for different classes (a render() function that works differently for text vs image messages).

Q2 :- Overloading vs overriding?

Ans :- Overloading: same method name, different inputs, in the same class. Overriding: a child class replaces a method it inherited from the parent class.

Q3 :- What does "composition over inheritance" mean?

Ans :- Instead of building one class on top of another in a long chain, you build small independent pieces and combine them — it's more flexible and less likely to break.

Q4 :- Interface vs abstract class?

Ans :- Interface only says what methods must exist, no actual code inside. Abstract class can have some real code already written, plus some methods that must be filled in by subclasses.

---

## Git & GitHub

Q1 :- Merge vs rebase?

Ans :- Merge combines two branches and keeps full history, including a merge commit. Rebase replays your changes on top of another branch, making history look like a straight line — but it's risky if others already have the old history.

Q2 :- What causes a merge conflict?

Ans :- When two branches change the exact same lines of a file differently, and Git doesn't know which version to keep, so it asks you to decide.

Q3 :- Fetch vs pull?

Ans :- Fetch just downloads the latest changes without applying them to your branch. Pull downloads and immediately merges them into your current branch.

Q4 :- How do you undo a commit that's already pushed?

Ans :- Use git revert — it creates a new commit that undoes the old one safely. Avoid git reset --hard on shared branches because it can mess up history for others.

Q5 :- What is .gitignore for?

Ans :- It tells Git which files to never track, like node_modules or .env files with secret keys.

Q6 :- [Project] What's your usual Git workflow?

Ans :- I create a separate branch for each feature, work on it, then merge it back into main — even for solo projects, this keeps things organized and easy to undo if something breaks.

---