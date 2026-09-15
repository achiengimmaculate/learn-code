# 27 Week Software Engineering Plan

Based on the Moringa School / Flatiron Software Engineering Bootcamp outline.

**Start:** Monday 21 September 2026
**Finish:** Sunday 28 March 2027
**Pace:** 20 to 25 hours per week, serious part-time
**Backend:** Python and Flask first, then ported to TypeScript and Next.js

## What I changed from the Moringa outline, and why

Moringa's 27 week track is full-time, roughly 40 hours a week, about 1,080 hours. At 20 to 25 hours I have around 600. So this plan keeps every module and every core concept, but cuts:

- Live lecture hours. Self-paced freeCodeCamp is faster per hour.
- Repetition. Fewer labs on the same idea, more projects that combine ideas.
- Group project overhead.
- Career incubator is compressed into week 1 and week 27 rather than spread out.

Two deliberate additions:

- **Week 5 is a light week.** The Mr&Miss Nakuru County event is 24 October. Business comes first that week.
- **Week 24 is a port week.** Rebuild the Flask API in Next.js. This is where Python and TypeScript meet.

## Where the theory comes from

| Module | Theory source |
|---|---|
| HTML and CSS | freeCodeCamp, Responsive Web Design |
| JavaScript | freeCodeCamp, JavaScript Algorithms and Data Structures |
| React | freeCodeCamp, Front End Libraries |
| Python | freeCodeCamp, Python Programming |
| SQL | freeCodeCamp, Relational Databases |
| Flask | **Not on freeCodeCamp.** Flask Mega-Tutorial and official docs. |
| Next.js | Official Next.js docs in `~/lucim-polls/node_modules/next/dist/docs/` |

Two things to know about freeCodeCamp:

1. **The full path is about 1,800 hours.** Six certifications at roughly 300 hours each, plus a capstone. We have 600. So we read the chapters that match the week we are on and we do not chase certificates. Certificates can be finished later.
2. **Flask is a real gap.** freeCodeCamp's Back End Development and APIs certification teaches Node and Express, not Flask. Useful for week 24, no help in weeks 20 to 23.

Full source list per topic is in [RESOURCES.md](RESOURCES.md).

---

## Module 1 and 2: Front End Development 1

### Week 01 (21 - 27 Sep) - Tooling and HTML structure
Terminal basics. VS Code. Git and GitHub, properly, not by copy-paste. What a repo, a commit and a push actually are. HTML document structure, semantic tags, links, images, lists, tables, forms markup.
**Deliverable:** a personal profile page, hand written, pushed to GitHub. GitHub profile set up.

### Week 02 (28 Sep - 4 Oct) - CSS fundamentals
Selectors and specificity. The box model. Colour, units, typography. Inheritance and the cascade. Why the cascade is the thing that confuses everybody.
**Deliverable:** week 1's page, styled. Same HTML, no changes to it.

### Week 03 (5 - 11 Oct) - CSS layout and responsive design
Flexbox. CSS Grid. Positioning. Media queries. Mobile first thinking.
**Deliverable:** a responsive multi-section landing page that works on a phone.

### Week 04 (12 - 18 Oct) - JavaScript fundamentals 1
Variables, types, operators. Conditionals. Functions, parameters, return values. Scope. The difference between an expression and a statement.
**Deliverable:** a set of small logic exercises, plus a command line style program.

### Week 05 (19 - 25 Oct) - LIGHT WEEK, event on 24 Oct
Consolidation only. Redo week 4 exercises without looking. No new concepts.
**Deliverable:** nothing new. Do not feel guilty about this week.

### Week 06 (26 Oct - 1 Nov) - JavaScript data structures
Arrays and objects. Loops. `map`, `filter`, `reduce`, `find`, `sort`. Nested data. JSON.
**Deliverable:** transform a messy dataset into a clean summary, using array methods only.

### Week 07 (2 - 8 Nov) - The DOM and events
What the DOM actually is. Selecting, creating and removing elements. Event listeners. Forms and user input. Debugging in browser dev tools.
**Deliverable:** an interactive page. Something that responds to clicks and typing.

### Week 08 (9 - 15 Nov) - Async JavaScript and PROJECT 1
Callbacks. Promises. `async`/`await`. `fetch`. Reading API documentation. Error handling. Intro to testing.
**Deliverable:** **Project 1.** A working app that fetches live data from a public API and displays it. HTML, CSS and JavaScript only, no frameworks.

---

## Module 3: Front End Development 2 (React)

### Week 09 (16 - 22 Nov) - React 1: components and props
Why React exists and what problem it solves. Components. JSX. Props. Thinking in components.
**Deliverable:** rebuild a static page from week 3 as React components.

### Week 10 (23 - 29 Nov) - React state and forms
`useState`. Event handling in React. Controlled inputs. Forms. Why you never edit state directly.
**Deliverable:** a form driven app that holds and updates state.

### Week 11 (30 Nov - 6 Dec) - Lists, keys and lifting state
Rendering lists. Keys and why they matter. Lifting state up. Passing callbacks down. Component composition.
**Deliverable:** a multi-component app where two siblings share data.

### Week 12 (7 - 13 Dec) - React 2: effects, data and routing
`useEffect`. Fetching data in React. Loading and error states. Client side routing. Custom hooks, gently.
**Deliverable:** a React app with more than one page that loads real data.

### Week 13 (14 - 20 Dec) - PROJECT 2
**Deliverable:** **Project 2.** A complete React application consuming a real API, with routing, forms, loading states and error handling. Deployed and live on the internet.

### Week 14 (21 - 27 Dec) - HEALTH AND WELLNESS BREAK
Christmas. Rest. This is in the Moringa outline and it is there for a reason.

---

## Module 4: Back End Development 1 (Python)

### Week 15 (28 Dec - 3 Jan) - Python fundamentals
Syntax and indentation. Variables, types, control flow, functions. What is genuinely different from JavaScript and what is just spelled differently.
**Deliverable:** rewrite three of your week 4 JavaScript exercises in Python.

### Week 16 (4 - 10 Jan) - Python data structures
Lists, dictionaries, tuples, sets. Comprehensions. Modules and packages. Reading and writing files. Virtual environments and `pip`.
**Deliverable:** a Python script that reads a file, processes it and writes a report.

### Week 17 (11 - 17 Jan) - Object oriented programming
Classes and objects. Attributes and methods. `__init__`. Inheritance. Encapsulation. What an object is *for*.
**Deliverable:** model a real domain from your own business as Python classes.

### Week 18 (18 - 24 Jan) - Object modelling and relationships
One to many. Many to many. Join objects. How real systems model relationships before any database appears.
**Deliverable:** model an event, its organizer, its contestants and its votes.

---

## Module 5: Back End Development 2 (Flask, SQL, auth)

### Week 19 (25 - 31 Jan) - SQL
Tables, keys, data types. `SELECT`, `INSERT`, `UPDATE`, `DELETE`. `WHERE`, `ORDER BY`, `GROUP BY`. JOINs. Indexes. Schema design and normalisation.
**Deliverable:** design and query a database by hand, no ORM, pure SQL.

### Week 20 (1 - 7 Feb) - Flask and REST
What a web server does. Routes, requests, responses. HTTP methods and status codes. JSON APIs. What REST actually means.
**Deliverable:** a Flask API with full CRUD, held in memory, no database yet.

### Week 21 (8 - 14 Feb) - Flask-SQLAlchemy
ORMs and what they hide. Models. Migrations. Querying. Relationships in SQLAlchemy. Serialisation.
**Deliverable:** week 20's API, now backed by a real database.

### Week 22 (15 - 21 Feb) - Validation, auth and security
Input validation. Error handling. Password hashing. JWT authentication. Protected routes. Common vulnerabilities and how they happen.
**Deliverable:** users can sign up, log in, and only touch their own data.

### Week 23 (22 - 28 Feb) - PROJECT 3
**Deliverable:** **Project 3.** A complete, secure, documented Flask REST API with a relational database, authentication and tests. Deployed.

---

## The bridge

### Week 24 (1 - 7 Mar) - Port the API to TypeScript and Next.js
Rebuild week 23's API in Next.js. Same endpoints, same schema, same auth. Then compare them side by side and name what is a real difference versus what is only different spelling.

This week is the whole reason for learning both. It is where the concepts detach from the language and become yours.
**Deliverable:** two APIs, two languages, one behaviour. Plus written notes on what genuinely differed.

---

## Module 6: Capstone and Assessment

### Week 25 (8 - 14 Mar) - Capstone: plan and backend
Scope it. Design the schema. Build the API. TypeScript and Next.js.

### Week 26 (15 - 21 Mar) - Capstone: frontend and integration
React frontend. Wire it to the backend. Auth. Error states. Make it real.

### Week 27 (22 - 28 Mar) - Ship, assess, present
Deploy. Write a proper README. Technical assessment. Mock interview. Resume, LinkedIn and portfolio finished.

**Final deliverable:** a deployed full-stack application solving a real business problem, built by you, that you can explain line by line.

---

## The rule that makes all of this work

I type the code. Claude reviews it, questions it, and explains it. If Claude writes my exercise, the week was wasted.
