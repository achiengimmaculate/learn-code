# JavaScript frameworks and libraries

MDN Core module 6. In practice: React.

This one matters more than the others, because **Lucim Polls is already built in React**. Everything below is in code you own.

---

# PART 1: WHY FRAMEWORKS EXIST

## The problem

You already know how to change a page:

```js
const btn = document.querySelector("button");
btn.textContent = "Stop machine";
txt.textContent = "The machine has started!";
```

You wrote that. It works. Now imagine a page with a hundred moving parts: a vote count, a list of contestants that filters as you type, a form that validates, a total that updates.

Every one of them needs you to **find the element and change it by hand**. And every piece of data might appear in three places at once, so one change means three updates, and if you forget one, the screen lies to the user.

That is the problem. Not that it is hard, but that it does not scale and the bugs are invisible.

## The shift: imperative to declarative

This is the single idea behind every framework. Everything else is detail.

**Imperative** (vanilla JS). You give instructions:

> Find the button. Change its text to "Stop machine". Find the paragraph. Change its text.

**Declarative** (React). You describe the result:

> When the machine is running, the button says "Stop machine" and the paragraph says "The machine has started."

You never touch the DOM. You change **data**, and React works out what the page should now look like and makes the minimum changes needed.

Your machine example, in React:

```jsx
function Machine() {
  const [isRunning, setIsRunning] = useState(false);

  return (
    <div>
      <button onClick={() => setIsRunning(!isRunning)}>
        {isRunning ? "Stop machine" : "Start machine"}
      </button>
      <p>{isRunning ? "The machine has started!" : "The machine is stopped."}</p>
    </div>
  );
}
```

No `querySelector`. No `textContent`. You flip one boolean and both pieces of text follow, automatically, forever. **They cannot get out of sync, because there is only one source of truth.**

## Framework or library?

A **library** is a toolbox you call. A **framework** calls you: it runs the show and your code slots into it.

React is technically a library. Nobody minds either word. The distinction is trivia.

---

# PART 2: COMPONENTS

**A component is a function that returns a piece of UI.**

```jsx
function Welcome() {
  return <h1>Hello</h1>;
}
```

That is a whole React component. A function. Returns markup. Nothing more mysterious than that.

Use it like a tag:

```jsx
<Welcome />
```

## Two rules

1. **The name must start with a capital letter.** `Welcome`, not `welcome`. That is how React tells your components apart from HTML tags like `<div>`.
2. **It must return exactly one top-level element.**

Need to return several things side by side? Wrap them:

```jsx
function Card() {
  return (
    <>
      <h2>Kitchen</h2>
      <p>45,000</p>
    </>
  );
}
```

`<>...</>` is a **fragment**: a wrapper that groups things without adding a real element to the page.

## Why components

You already know why, from CSS. A class lets you write a style once and apply it everywhere. A component does the same for markup *and* behaviour.

Build a `<ContestantCard />` once, use it two hundred times, change it in one place.

---

# PART 3: JSX

JSX is the HTML-looking stuff inside your JavaScript.

```jsx
const heading = <h1>Hello</h1>;
```

It is not HTML and it is not a string. It is JavaScript, with a build step that turns it into real function calls before the browser sees it.

## Curly braces put JavaScript in

```jsx
const name = "Immaculate";
const count = 3;

<h1>Hello {name}</h1>
<p>You have {count * 2} votes</p>
<p>{count > 0 ? "Some votes" : "No votes yet"}</p>
```

**Anything inside `{}` is a JavaScript expression.** An expression, meaning something that produces a value. You cannot put an `if` statement or a `for` loop in there. Ternaries and `.map()` are how you handle those, which is why they turn up everywhere in React.

## Differences from HTML

| HTML | JSX | Why |
|---|---|---|
| `class` | `className` | `class` is a reserved word in JavaScript |
| `for` | `htmlFor` | same reason |
| `onclick` | `onClick` | camelCase for every event |
| `<br>` | `<br />` | every tag must close |
| `style="color:red"` | `style={{color: 'red'}}` | an object, not a string |

Those double braces in `style` are not special syntax. The outer pair means "JavaScript here", the inner pair is an object literal.

## Returning multi-line JSX

Wrap it in brackets so the `return` does not stop at the end of the line:

```jsx
return (
  <div>
    <h1>Title</h1>
  </div>
);
```

---

# PART 4: PROPS

**Props are how a parent passes data down to a child.** Like attributes on an HTML tag, but they can carry anything.

```jsx
function RoomCard(props) {
  return (
    <div>
      <h2>{props.name}</h2>
      <p>KES {props.cost}</p>
    </div>
  );
}
```

```jsx
<RoomCard name="Kitchen" cost={45000} />
<RoomCard name="Bedroom" cost={30000} />
```

Note the difference: `name="Kitchen"` is a string so it uses quotes. `cost={45000}` is a number so it needs braces. **Quotes give you a string, braces give you a JavaScript value.**

## Destructuring

You will almost always see props written like this instead:

```jsx
function RoomCard({ name, cost }) {
  return (
    <div>
      <h2>{name}</h2>
      <p>KES {cost}</p>
    </div>
  );
}
```

Same thing, unpacked at the top. Less typing, and you can see at a glance what the component expects.

## Props are read-only

**A component must never change its own props.**

```jsx
function Bad({ count }) {
  count = count + 1;   // no
}
```

Data flows **down**, parent to child, one direction. If a child needs to change something, the parent hands it a function to call. More on that under lifting state.

## children

```jsx
function Panel({ children }) {
  return <div className="panel">{children}</div>;
}
```

```jsx
<Panel>
  <h2>Anything</h2>
  <p>goes in here</p>
</Panel>
```

`children` is whatever you put between the opening and closing tags. It is how you build wrappers and layouts.

---

# PART 5: STATE

**Props come from outside and never change. State lives inside and does.**

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Clicked {count} times
    </button>
  );
}
```

## Reading that line

```jsx
const [count, setCount] = useState(0);
```

- `useState(0)` creates a piece of state starting at `0`
- It hands back two things: **the current value**, and **a function to change it**
- The square brackets unpack them into two names
- Convention: `x` and `setX`

## The rule

**Never change state directly.**

```jsx
count = count + 1;        // nothing happens
setCount(count + 1);      // correct
```

Assigning to the variable does nothing, because React has no way of knowing you did it. Calling the setter tells React "this changed, re-render."

## Objects and arrays in state

Same rule, and it catches everyone:

```jsx
// wrong, mutates the existing array
rooms.push("Kitchen");
setRooms(rooms);

// right, makes a new array
setRooms([...rooms, "Kitchen"]);
```

```jsx
// wrong
user.name = "Ann";
setUser(user);

// right
setUser({ ...user, name: "Ann" });
```

`...` is the **spread operator**: "copy everything out of this, then add my changes." React compares the old value to the new one, and a mutated array is still the same array, so it concludes nothing changed and skips the update.

## State is per instance

```jsx
<Counter />
<Counter />
```

Two independent counters. Each gets its own `count`. State belongs to the instance, not the function.

---

# PART 6: EVENTS

```jsx
<button onClick={handleClick}>Click</button>
```

Almost the same as `addEventListener`, with two differences: it is camelCase, and you pass the function itself rather than a string.

```jsx
function Button() {
  function handleClick() {
    console.log("clicked");
  }

  return <button onClick={handleClick}>Click</button>;
}
```

## The mistake everyone makes once

```jsx
<button onClick={handleClick}>    // correct, pass the function
<button onClick={handleClick()}>  // wrong, CALLS it during render
```

With the brackets, the function runs immediately when the component renders, not when anyone clicks. If it sets state, you get an infinite loop.

Need to pass an argument? Wrap it in an arrow function:

```jsx
<button onClick={() => handleDelete(room.id)}>Delete</button>
```

Now you are passing a *new* function that calls yours when clicked.

## Forms

```jsx
function Form() {
  const [name, setName] = useState("");

  function handleSubmit(event) {
    event.preventDefault();
    console.log(name);
  }

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="name">Name</label>
      <input
        id="name"
        value={name}
        onChange={(e) => setName(e.target.value)}
      />
      <button type="submit">Send</button>
    </form>
  );
}
```

That input is **controlled**: its `value` comes from state, and every keystroke fires `onChange` which updates state, which re-renders with the new value. The state is the single source of truth, not the DOM.

`event.preventDefault()` is the same thing you learned in vanilla JS. Without it the page reloads.

---

# PART 7: LISTS AND KEYS

```jsx
const rooms = [
  { id: 1, name: "Kitchen", cost: 45000 },
  { id: 2, name: "Bedroom", cost: 30000 }
];

function RoomList() {
  return (
    <ul>
      {rooms.map((room) => (
        <li key={room.id}>{room.name} — KES {room.cost}</li>
      ))}
    </ul>
  );
}
```

This is why `.map()` mattered so much in the JavaScript notes. **Turning an array of data into an array of UI is most of what React does.**

## Keys

**Every item in a list needs a `key`.** It must be unique among its siblings and stable between renders.

React uses keys to match up items across renders. Without them it cannot tell whether you inserted something at the top or changed everything.

```jsx
<li key={room.id}>          // good, a real stable id
<li key={index}>            // bad in most cases
```

**Why the index is a trap:** delete the first item and every remaining item's index shifts. React thinks item 0 changed its text rather than that item 0 was removed, and anything attached to those rows, like typed-in form values or focus, ends up on the wrong row.

Index is only safe when the list never reorders, never filters and never has items removed.

---

# PART 8: CONDITIONAL RENDERING

**Ternary**, when there are two options:

```jsx
{isLoggedIn ? <Dashboard /> : <LoginForm />}
```

**`&&`**, when it is show-or-nothing:

```jsx
{hasVotes && <p>You have voted</p>}
```

**An early return**, when whole branches differ:

```jsx
function Profile({ user }) {
  if (!user) return <p>Loading...</p>;
  return <h1>{user.name}</h1>;
}
```

## One gotcha with `&&`

```jsx
{count && <p>You have {count} votes</p>}
```

When `count` is `0`, this renders a literal **0** on the page, because `0` is falsy but still a renderable value. Use an explicit comparison:

```jsx
{count > 0 && <p>You have {count} votes</p>}
```

---

# PART 9: LIFTING STATE UP

Two components need the same data. Where does it live?

**In their nearest common parent.** Then it flows down as props, and changes flow back up as functions.

```jsx
function App() {
  const [search, setSearch] = useState("");

  return (
    <>
      <SearchBar value={search} onChange={setSearch} />
      <ResultList search={search} />
    </>
  );
}

function SearchBar({ value, onChange }) {
  return <input value={value} onChange={(e) => onChange(e.target.value)} />;
}
```

`SearchBar` owns no state. It is handed a value and a function. It calls the function, the parent's state changes, and both children re-render with the new value.

**Data down, events up.** That is the whole pattern, and once it clicks, most of React's structure makes sense.

---

# PART 10: useEffect

Most of what a component does is turn data into markup. `useEffect` is for the things that fall outside that: fetching data, timers, subscriptions, reaching into the browser directly.

```jsx
import { useState, useEffect } from "react";

function Events() {
  const [events, setEvents] = useState([]);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    fetch("/api/events")
      .then((res) => res.json())
      .then((data) => {
        setEvents(data);
        setLoading(false);
      });
  }, []);

  if (loading) return <p>Loading...</p>;

  return (
    <ul>
      {events.map((e) => <li key={e.id}>{e.name}</li>)}
    </ul>
  );
}
```

## The dependency array

That `[]` at the end decides **when** the effect runs. It is the whole thing:

```jsx
useEffect(() => { ... });            // after EVERY render. Almost always a bug.
useEffect(() => { ... }, []);        // once, when the component first appears
useEffect(() => { ... }, [eventId]); // whenever eventId changes
```

**Forgetting the array is the classic React infinite loop.** The effect sets state, state causes a re-render, the re-render runs the effect, forever.

## Cleanup

Return a function and React runs it when the component goes away:

```jsx
useEffect(() => {
  const id = setInterval(tick, 1000);
  return () => clearInterval(id);
}, []);
```

Without that, the timer keeps running after the component is gone.

---

# PART 11: THE RULES OF HOOKS

Anything starting with `use` is a hook. `useState`, `useEffect`, and the rest.

**Two rules, no exceptions:**

1. **Only call hooks at the top level of a component.** Never inside an `if`, a loop, or a nested function.
2. **Only call them from components or from other hooks.** Not from ordinary functions.

```jsx
// wrong
if (isLoggedIn) {
  const [name, setName] = useState("");
}

// right
const [name, setName] = useState("");
if (isLoggedIn) { ... }
```

Why: React tracks your state by **the order the hooks were called**, not by name. Put one behind an `if` and the order changes between renders, and React hands you the wrong value.

## The other hooks you will meet

```jsx
useRef()       // a value that survives renders without causing one. Often a DOM element.
useContext()   // read shared data without passing props down every level
useMemo()      // cache an expensive calculation
useCallback()  // cache a function
```

Learn `useState` and `useEffect` properly first. The rest can wait until you hit the problem they solve.

---

# PART 12: REACT AND NEXT.JS

Worth knowing, because it is the gap between this module and your own product.

**React** gives you components, props, state and rendering. That is all. It does not do routing, data loading, or servers.

**Next.js** is a framework built on top of React that adds the rest: file-based routing, server rendering, API routes, bundling, deployment.

**Everything in these notes applies unchanged inside Next.js.** Components, props, state, effects, keys. Same React.

What Next.js adds on top:

- **Pages are files.** `app/vote/page.tsx` becomes the `/vote` route. No router to configure.
- **Server Components by default.** Components run on the server and send HTML, which is faster. They cannot use `useState` or `onClick`, because those need a browser.
- **`"use client"`** at the top of a file marks it as a component that runs in the browser. Anything with state or event handlers needs it.

That one line is the thing that confuses people moving from React to Next.js. If you see `"use client"` at the top of a Lucim Polls file, that is why.

---

# COMMON MISTAKES

| Mistake | What happens |
|---|---|
| `onClick={handleClick()}` | Runs during render, not on click |
| `count = count + 1` | Nothing. Use the setter. |
| `arr.push(x); setArr(arr)` | Nothing. React sees the same array. Use `[...arr, x]` |
| `useEffect` with no dependency array | Infinite loop |
| `key={index}` on a list that changes | Items get the wrong state |
| `{count && <p>...</p>}` | Renders a literal `0` |
| `class=` instead of `className=` | Ignored |
| Lowercase component name | React treats it as an HTML tag |
| Hook inside an `if` | React returns the wrong state |

---

# WHAT TO MASTER FIRST

1. **A component is a function that returns UI.**
2. **Props down, events up.**
3. **`useState`: never assign, always use the setter, never mutate.**
4. **`.map()` with a stable `key` for lists.**
5. **`useEffect` with the right dependency array.**

Those five are React. Everything else is built on them.

---

# SELF-CHECK

- [ ] Can I explain declarative versus imperative in my own words?
- [ ] What is the difference between props and state?
- [ ] Why does `setCount` exist instead of just `count = count + 1`?
- [ ] Why does `arr.push()` then `setArr(arr)` not work?
- [ ] What are keys for, and why is the array index usually wrong?
- [ ] What does the dependency array in `useEffect` control?
- [ ] Why must hooks never go inside an `if`?
- [ ] What does `"use client"` do in a Next.js file?

Any unticked box is worth going back for. All eight show up in Lucim Polls.
