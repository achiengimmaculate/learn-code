# JavaScript: the whole picture

Written for someone who covered this in pieces, out of order, with gaps. Read it start to finish once. The order matters more than any single section.

---

# PART 1: WHAT JAVASCRIPT IS

Three languages, three jobs:

| | Job | Think of it as |
|---|---|---|
| HTML | What things **are** | Nouns |
| CSS | How things **look** | Adjectives |
| JavaScript | What things **do** | Verbs |

HTML and CSS describe a page. They are declarations. JavaScript is different: it is a real programming language that **runs**, step by step, and can change the page while someone is looking at it.

A button that does nothing is HTML. A button that changes when clicked is JavaScript.

## Where it runs

Inside the browser, on the visitor's own computer. Every browser has a JavaScript engine built in.

That has one consequence worth holding on to: **anyone can read your JavaScript.** Right-click, View Source. So nothing secret goes in it. No passwords, no API keys.

## Attaching it

```html
<script src="script.js" defer></script>
```

`defer` means "download it now, run it once the page has finished loading." Use it. Without it your script may run before the elements it talks about exist, and everything breaks in a way that looks random.

---

# PART 2: VARIABLES

**A variable is a named box you put a value in.**

```js
let score = 0;
const name = "Immaculate";
```

| | Can it be changed later? | Use it |
|---|---|---|
| `const` | No | **By default** |
| `let` | Yes | When the value genuinely changes |
| `var` | Yes | Never. It is the old way and it has traps |

**Reach for `const` first.** Only switch to `let` when you actually need to reassign. This is not pedantry: it means that when you read code later, `const` tells you at a glance that this thing never changes.

One subtlety that confuses everyone:

```js
const list = ["a", "b"];
list.push("c");      // fine, the array changed
list = ["x"];        // error, the variable was reassigned
```

`const` stops you pointing the name at a *different* thing. It does not freeze what is inside.

## Naming

```js
let userName;     // camelCase, the convention
let user_name;    // works, but not JavaScript style
let 2cool;        // error, cannot start with a number
```

Names are **case sensitive**. `userName` and `username` are two different variables, and mixing them up is a classic silent bug.

---

# PART 3: TYPES

```js
let count   = 42;                    // number
let price   = 19.99;                 // also number, no separate integer type
let name    = "Immaculate";          // string
let isOpen  = true;                  // boolean: true or false
let rooms   = ["kitchen", "bedroom"];// array
let person  = { name: "Ann", age: 30 }; // object
let nothing = null;                  // deliberately empty
let missing;                         // undefined: never given a value
```

**`null` versus `undefined`:** `null` means "I set this to empty on purpose." `undefined` means "nobody ever set this." You will see `undefined` constantly when something has gone wrong.

## Strings

Quotes, any of three kinds:

```js
"double"
'single'
`backticks`
```

Backticks are special. They are **template literals** and they let you drop values straight in:

```js
const name = "Ann";
const greeting = `Hello ${name}, you have ${3 + 4} messages`;
```

That `${...}` is far nicer than gluing strings with `+`. Use backticks whenever a string contains a value.

### String methods worth knowing

```js
const s = "Interior Design";

s.length            // 15   (a property, no brackets)
s.toUpperCase()     // "INTERIOR DESIGN"
s.toLowerCase()
s.includes("Design")// true
s.indexOf("Design") // 9
s.slice(0, 8)       // "Interior"
s.replace("Design", "Decor")
s.split(" ")        // ["Interior", "Design"]
s.trim()            // removes spaces at both ends
```

**Strings are immutable.** None of these change `s`. They all return a *new* string. If you want to keep the result, assign it to something.

## Numbers

```js
7 + 2    // 9
7 - 2    // 5
7 * 2    // 14
7 / 2    // 3.5
7 % 2    // 1   remainder. Brilliant for "is this even?"
7 ** 2   // 49  power
```

```js
let n = 5;
n++;        // 6
n += 10;    // 16   shorthand for n = n + 10
```

**The famous gotcha:**

```js
"5" + 3    // "53"   string + number glues them
"5" - 3    // 2      minus has no string meaning, so it converts
```

Numbers that arrive from a form or a web page are **strings**. Convert them first:

```js
Number("5") + 3     // 8
parseInt("5")       // 5
```

---

# PART 4: MAKING DECISIONS

```js
if (score > 100) {
  console.log("You win");
} else if (score > 50) {
  console.log("Not bad");
} else {
  console.log("Try again");
}
```

## Comparison

```js
a === b   // equal, and same type     USE THIS
a !== b   // not equal                USE THIS
a >  b
a <  b
a >= b
a <= b
```

**Always use `===`, never `==`.**

`==` converts types before comparing, which gives you nonsense like `"5" == 5` being true and `0 == ""` being true. `===` compares without converting. There is no good reason to use `==` while you are learning.

## Combining

```js
&&   // AND, both must be true
||   // OR, at least one must be true
!    // NOT, flips it
```

```js
if (isLoggedIn && hasPaid) { }
if (isAdmin || isOwner) { }
if (!isOpen) { }
```

## Truthy and falsy

Any value can be treated as true or false. These are **falsy**:

```
false   0   ""   null   undefined   NaN
```

Everything else is **truthy**, including `"0"`, `"false"` and `[]`.

So this works:

```js
if (name) {        // "is name a non-empty string?"
```

## switch

For many branches on one value:

```js
switch (room) {
  case "kitchen":
    cost = 45000;
    break;
  case "bedroom":
    cost = 30000;
    break;
  default:
    cost = 0;
}
```

**Do not forget `break`.** Without it execution falls through into the next case, which is almost never what you want.

## The ternary

A compact if/else that produces a value:

```js
const label = isOpen ? "Open" : "Closed";
```

Fine for short things. Do not nest them.

---

# PART 5: LOOPS

## for...of, the one to use most

```js
const rooms = ["kitchen", "bedroom", "dining"];

for (const room of rooms) {
  console.log(room);
}
```

Readable, hard to get wrong. Reach for this first.

## Classic for

When you need the index, or a specific number of repeats:

```js
for (let i = 0; i < 10; i++) {
  console.log(i);
}
```

Three parts separated by semicolons: **start**, **keep going while**, **do after each pass**.

`i < 10` not `i <= 10`. Counting starts at 0, so ten items are 0 to 9. Getting this wrong by one is so common it has a name: an off-by-one error.

## while

When you do not know how many times:

```js
while (!finished) {
  // something must eventually set finished = true
}
```

Careful. If nothing changes the condition, the browser tab freezes.

## break and continue

```js
break;      // leave the loop entirely
continue;   // skip the rest of this pass, go to the next
```

---

# PART 6: FUNCTIONS

**A function is a named block of instructions you can run whenever you like.**

```js
function calculateCost(area, rate) {
  return area * rate;
}

const total = calculateCost(20, 1500);   // 30000
```

- **Parameters** (`area`, `rate`) are the names used inside
- **Arguments** (`20`, `1500`) are the actual values passed in
- **`return`** sends a value back out

## return

```js
function double(n) {
  return n * 2;
}

function shout(n) {
  console.log(n * 2);     // prints, but returns undefined
}
```

**`console.log` is not `return`.** Logging shows you something. Returning hands a value back so the rest of your code can use it. Confusing the two is the most common early mistake.

`return` also **stops the function immediately.** Nothing after it runs.

## Three ways to write one

```js
// declaration
function add(a, b) { return a + b; }

// expression
const add = function(a, b) { return a + b; };

// arrow function
const add = (a, b) => a + b;
```

Arrow functions are everywhere in modern code. With a single expression the `return` is implied. You will see them constantly as callbacks:

```js
button.addEventListener("click", () => {
  console.log("clicked");
});
```

## Scope

```js
function test() {
  const inside = "only visible in here";
}
console.log(inside);   // error
```

Variables declared inside a function exist only inside it. This is a feature: it means two functions can both use a variable called `i` without colliding.

---

# PART 7: ARRAYS

**An ordered list. Positions start at 0.**

```js
const rooms = ["kitchen", "bedroom", "dining"];

rooms[0]        // "kitchen"
rooms[2]        // "dining"
rooms.length    // 3
rooms[rooms.length - 1]   // the last one
```

## Changing them

```js
rooms.push("bathroom");     // add to the end
rooms.pop();                // remove from the end
rooms.unshift("hallway");   // add to the start
rooms.shift();              // remove from the start
rooms.includes("kitchen");  // true
rooms.indexOf("bedroom");   // 1
rooms.join(", ");           // "kitchen, bedroom, dining"
```

## The three that matter most

These three turn up everywhere, and in React especially. Learn them properly.

**`forEach`** does something with each item:

```js
rooms.forEach(room => {
  console.log(room);
});
```

**`map`** makes a **new array** by transforming each item:

```js
const upper = rooms.map(room => room.toUpperCase());
// ["KITCHEN", "BEDROOM", "DINING"]
```

**`filter`** makes a **new array** of items that pass a test:

```js
const long = rooms.filter(room => room.length > 6);
// ["kitchen", "bedroom"]
```

The distinction: **`map` gives you the same number of items, changed. `filter` gives you fewer items, unchanged.**

Also useful:

```js
rooms.find(r => r.startsWith("k"));   // the first match, or undefined
rooms.sort();
const total = costs.reduce((sum, c) => sum + c, 0);   // boils down to one value
```

---

# PART 8: OBJECTS

**An array holds things in order. An object holds things by name.**

```js
const room = {
  name: "Kitchen",
  area: 20,
  cost: 45000,
  isDone: false
};
```

Each entry is a **key** and a **value**.

```js
room.name           // "Kitchen"      dot notation, usual
room["name"]        // same thing     needed when the key is in a variable
room.area = 25;     // change
room.client = "Ann";// add
```

## Methods

A function stored in an object is called a **method**:

```js
const room = {
  name: "Kitchen",
  describe() {
    return `${this.name} costs ${this.cost}`;
  }
};
```

`this` means "the object I am inside."

## Arrays of objects

This is the shape almost all real data takes:

```js
const rooms = [
  { name: "Kitchen", cost: 45000 },
  { name: "Bedroom", cost: 30000 }
];

rooms[0].name                                  // "Kitchen"
rooms.map(r => r.name)                         // ["Kitchen", "Bedroom"]
rooms.filter(r => r.cost > 35000)              // just the kitchen
rooms.reduce((sum, r) => sum + r.cost, 0)      // 75000
```

Get comfortable with this shape. Every API you ever call returns something like it.

## JSON

**JSON is text that looks like a JavaScript object.** It is how data travels between computers.

```json
{ "name": "Kitchen", "cost": 45000 }
```

Differences from a real object: **keys must be in double quotes**, no functions, no trailing commas.

```js
JSON.parse(text)      // text  -> object
JSON.stringify(obj)   // object -> text
```

---

# PART 9: THE DOM

**The DOM is JavaScript's handle on the page.** The browser reads your HTML and builds a tree of objects from it. JavaScript can then read and change that tree, and the page updates instantly.

## Finding elements

```js
document.querySelector(".feature");      // the FIRST match
document.querySelectorAll("li");         // ALL matches
document.getElementById("kitchen");
```

`querySelector` takes **any CSS selector**. Everything you learned about selectors transfers directly.

```js
document.querySelector("nav ul li a");
document.querySelector("#kitchen .price");
```

## Changing them

```js
el.textContent = "New text";          // text only, safe
el.innerHTML = "<strong>Bold</strong>"; // parses HTML, use carefully

el.setAttribute("src", "photo.jpg");
el.getAttribute("href");

el.classList.add("active");
el.classList.remove("hidden");
el.classList.toggle("open");

el.style.color = "red";               // works, but prefer classList
```

**Prefer `classList` over `style`.** Keep the look in CSS and let JavaScript just switch classes on and off. Much easier to maintain.

**`textContent` over `innerHTML`** unless you genuinely need to insert tags. `innerHTML` with text a user typed is how websites get attacked.

## Making elements

```js
const li = document.createElement("li");
li.textContent = "New room";
document.querySelector("ul").appendChild(li);

el.remove();
```

---

# PART 10: EVENTS

**An event is something that happens: a click, a keypress, a page finishing loading. You attach a function to run when it does.**

```js
button.addEventListener("click", () => {
  console.log("clicked");
});
```

Three parts: the **element**, the **event name**, and the **function to run**.

That function is a **callback**: you are not calling it, you are handing it over to be called later, if and when the thing happens.

## Common events

```
click   dblclick   mouseover   mouseout
keydown   keyup
submit    (forms)
change    input     (form fields)
load      DOMContentLoaded
```

## The event object

Your callback gets handed an object describing what happened:

```js
button.addEventListener("click", (event) => {
  console.log(event.target);   // which element was clicked
});
```

For forms this matters:

```js
form.addEventListener("submit", (event) => {
  event.preventDefault();   // stop the page reloading
  // now handle it yourself
});
```

**`preventDefault()`** cancels the browser's normal response. Without it a form submit reloads the page and your code never gets a chance.

## Bubbling

When you click a button inside a div, the event fires on the button, **then the div, then the body**, rippling outward. That is **bubbling**.

It is mostly useful. It means you can listen on a parent and catch clicks on any child, including ones added later:

```js
list.addEventListener("click", (event) => {
  if (event.target.matches("li")) {
    console.log("clicked", event.target.textContent);
  }
});
```

One listener instead of a hundred.

To stop it spreading: `event.stopPropagation()`.

---

# PART 11: WHEN IT GOES WRONG

**JavaScript, unlike CSS, shouts when it fails.** Open the console. Right-click, Inspect, Console tab.

## The errors you will actually meet

**`Uncaught TypeError: Cannot read properties of null`**

The single most common one. It means `querySelector` found nothing, so you are trying to use `null` as if it were an element.

Causes, in order of likelihood:
1. A typo in the selector
2. The script ran before the HTML existed. **Add `defer`.**
3. The element genuinely is not on the page

**`ReferenceError: x is not defined`**

Misspelled variable, or used before it was declared, or out of scope.

**`SyntaxError: Unexpected token`**

A missing bracket, brace or quote. The line number is where the browser *noticed*, which is often after where the mistake is. Look above it.

## console.log is your main tool

```js
console.log(myVariable);
console.log("got here");
console.log({ name, age, score });   // prints names and values together
```

Sprinkle it liberally. "Does this line even run?" and "what is this value right now?" answer most bugs.

```js
console.error()   console.warn()   console.table(arrayOfObjects)
```

`console.table` on an array of objects prints a proper grid. Lovely for data.

---

# WHAT MATTERS MOST

If you only properly master five things out of all the above:

1. **Functions.** Parameters in, `return` out.
2. **Arrays of objects**, plus `map` and `filter`. This is the shape of all real data.
3. **`querySelector` and `addEventListener`.** This is how a page becomes interactive.
4. **`===` not `==`**, and `const` before `let`.
5. **Reading the console.** Every bug above announces itself there.

Those five carry you into React. The rest you can look up.

---

# MOST LIKELY GAPS

Covering this out of order usually leaves holes in the same places. Test yourself honestly:

- [ ] Can I explain the difference between `return` and `console.log`?
- [ ] Can I write a `map` without looking it up?
- [ ] Do I know why `event.preventDefault()` exists?
- [ ] Can I say what `null` means versus `undefined`?
- [ ] Do I know why `"5" + 3` is `"53"`?
- [ ] Can I explain what a callback is?
- [ ] Do I know why `defer` is on the script tag?

Any unticked box is a thing to go back to. They are all small, and all load-bearing.
