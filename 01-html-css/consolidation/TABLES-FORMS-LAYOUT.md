# Tables, forms and layout

The three topics that need a second pass.

---

# PART 1: TABLES

## The mental model

**A table is a spreadsheet.** Rows across, columns down, and every cell belongs to both a row and a column.

The whole job of table markup is answering one question for every cell: **which labels describe me?** A sighted person answers it instantly by glancing up and left. Someone using a screen reader cannot glance. They hear one cell at a time, so the markup has to carry that information.

That is why tables have more structure than lists. Not fussiness. The structure *is* the meaning.

## The parts

```html
<table>
  <caption>What this table is about</caption>

  <thead>
    <tr>
      <th scope="col">Room</th>
      <th scope="col">Cost</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <th scope="row">Kitchen</th>
      <td>45,000</td>
    </tr>
  </tbody>
</table>
```

| Element | What it is |
|---|---|
| `<table>` | The whole thing |
| `<caption>` | Its title. Always first, right after `<table>` |
| `<thead>` | The header row or rows |
| `<tbody>` | The actual data |
| `<tfoot>` | Totals, if you have them |
| `<tr>` | **T**able **r**ow. One horizontal line |
| `<th>` | **T**able **h**eader. A cell that *labels* other cells |
| `<td>` | **T**able **d**ata. A cell holding a value |

## `<th>` versus `<td>`, the only real decision

Ask: **does this cell label other cells, or is it a value?**

- "Room", "Cost", "Area" are labels → `<th>`
- "Kitchen", "45,000", "12sqm" are values → `<td>`

A `<th>` can sit at the top of a column *or* at the start of a row. Your first column is very often `<th>` cells.

## `scope`, which is what makes it accessible

`scope` tells a screen reader which direction a header applies in.

```html
<th scope="col">Cost</th>   <!-- labels the column below it -->
<th scope="row">Kitchen</th> <!-- labels the row beside it -->
```

Without it, a screen reader has to guess. With it, reaching the cell "45,000" it can announce "Kitchen, Cost, 45,000" and the listener knows exactly where they are.

**Rule: every `<th>` gets a `scope`.**

## Spanning

```html
<td colspan="2">Stretches across two columns</td>
<td rowspan="3">Stretches down three rows</td>
```

Useful, but it is where tables get confusing. Build it without spans first, get it working, then add them.

## The one thing tables are not for

**Never use a table to lay out a page.** It was common in 1999 and it is wrong now. Tables are for data that genuinely has rows and columns. Page layout is grid and flexbox, below.

---

# PART 2: FORMS

## The mental model

**A form is a questionnaire that gets posted somewhere.** The user fills in fields, presses a button, and the browser packages the answers and sends them to a server.

Everything in form markup serves one of three jobs:
1. **Asking** the question (the label)
2. **Collecting** the answer (the input)
3. **Naming** the answer so the server knows what it is (the `name` attribute)

## The shape

```html
<form action="/subscribe" method="post">

  <label for="email">Email address</label>
  <input type="email" id="email" name="email" required>

  <button type="submit">Send</button>

</form>
```

- **`action`** where the answers go. Leave it off while practising.
- **`method`** how they travel. `post` for anything private, `get` for searches.

## Labels, the part everyone gets wrong

```html
<label for="email">Email address</label>
<input type="email" id="email">
```

**`for` on the label must match `id` on the input.** Exactly. Those two attributes are what glue them together.

Why it matters:

1. A screen reader reaching the input announces "Email address". Without the link it says "edit text" and the user has no idea what to type.
2. Clicking the *label* focuses the input. On a phone, that turns a tiny checkbox into a target you can actually hit.

**Every single input needs a label.** Placeholder text is not a label, it vanishes the moment you start typing.

## `name` versus `id`

They confuse everyone, so:

- **`id`** is for the browser. It links the label, and CSS and JavaScript find the element with it. Must be unique on the page.
- **`name`** is for the server. It is the key the answer is filed under, like `email=someone@example.com`.

An input with no `name` is not sent at all.

## Input types

```html
<input type="text">      ordinary text
<input type="email">     keyboard shows @ on phones, basic validation
<input type="password">  dots
<input type="number">
<input type="tel">       numeric keypad on phones
<input type="date">      date picker
<input type="checkbox">  many choices
<input type="radio">     one choice from a group, same name for the group
<input type="file">
```

Not just text:

```html
<textarea id="message" name="message" rows="5"></textarea>

<select id="room" name="room">
  <option value="kitchen">Kitchen</option>
  <option value="bedroom">Bedroom</option>
</select>
```

`type` matters more than it looks. The right one gives phone users the right keyboard.

## Buttons

```html
<button type="submit">Send</button>
<button type="button">Does nothing by itself</button>
```

**A `<button>` inside a form submits by default.** If you want one that does not, you must say `type="button"`.

## Grouping

```html
<fieldset>
  <legend>Which rooms?</legend>
  <!-- related checkboxes -->
</fieldset>
```

Use it for radio buttons and checkbox groups so the whole group has a name, not just each option.

---

# PART 3: LAYOUT

## Start here: normal flow

Before any CSS, a page already has a layout. **Block** elements stack vertically, each on its own line. **Inline** elements sit side by side within a line.

```
block:  <div> <p> <h1> <ul> <li> <section>
inline: <span> <a> <strong> <em> <img>
```

Everything below is a way of *overriding* normal flow. So the first question is always: **do I actually need to override it?** A column of paragraphs already works, on every screen size, for free.

## The one distinction that matters

| | Flexbox | Grid |
|---|---|---|
| Dimensions | **One** | **Two** |
| Think of it as | A row, or a column | A chessboard |
| Good for | Navs, button groups, toolbars, centring | Page structure, card galleries |
| Decided by | The content | You, up front |

**Flexbox arranges things along a line. Grid arranges things in rows and columns at the same time.**

If you are lining things up in one direction, flexbox. If you are placing things into a structure of rows *and* columns, grid.

## Flexbox

```css
.nav-list {
  display: flex;              /* children now sit in a row */
  justify-content: space-between;  /* spacing ALONG the row */
  align-items: center;        /* alignment ACROSS the row */
  gap: 20px;
}
```

The trick is the two axes:

- **`justify-content`** works along the main axis (horizontal by default)
- **`align-items`** works across it (vertical by default)

```
justify-content: flex-start | center | flex-end | space-between | space-around
align-items:     flex-start | center | flex-end | stretch
```

Switch direction and the axes swap with it:

```css
flex-direction: column;   /* now justify-content is vertical */
```

That swap is the single most confusing thing about flexbox. The properties do not mean "horizontal" and "vertical", they mean "along" and "across".

## Grid

```css
.layout {
  display: grid;
  grid-template-columns: 3fr 1fr;  /* two columns, first 3x wider */
  gap: 20px;
}
```

**`fr` means "fraction of the space left over."** `3fr 1fr` splits it three to one. `1fr 1fr 1fr` gives three equal columns.

You can mix:

```css
grid-template-columns: 200px 1fr;   /* fixed sidebar, flexible rest */
```

And let it decide how many fit:

```css
grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
```

That one says "as many columns as fit, each at least 200px". It is responsive with no media query at all.

## Positioning

```css
position: static;    /* the default, normal flow */
position: relative;  /* nudged from where it would be */
position: absolute;  /* removed from flow, placed against its positioned parent */
position: fixed;     /* stuck to the viewport, ignores scrolling */
position: sticky;    /* normal until it hits an edge, then stuck */
```

`sticky` plus `top: 0` is the nav bar that follows you down. You have already used it.

## Float

```css
float: left;
```

Makes text wrap around something, like an image in a magazine column. **That is all it should be used for now.** It was once the main way to build layouts, which is why old tutorials are full of it. Grid and flexbox replaced it.

## Centring

```css
.container {
  max-width: 980px;
  margin: 0 auto;
}
```

`max-width` caps the width, `margin: 0 auto` splits the leftover space equally either side. Works at any screen size, and below 980px it simply fills what is available.

## Mobile first

**Write the small screen first, then add media queries that widen it.**

```css
/* the default: phone */
.cards { display: grid; gap: 20px; }

/* bigger screens get more columns */
@media (min-width: 600px) {
  .cards { grid-template-columns: 1fr 1fr; }
}

@media (min-width: 900px) {
  .cards { grid-template-columns: 1fr 1fr 1fr; }
}
```

Why this way round: a phone layout is a single column, which is the simplest thing to write. Starting wide and stripping away means fighting your own CSS.

Always use `min-width` for this, so each query adds to the one before.

## `box-sizing`, set it once and forget

```css
* {
  box-sizing: border-box;
}
```

By default `width: 200px` means 200px of *content*, and padding and border get added on top, so the box ends up bigger than you asked for. `border-box` makes width mean the whole box, including padding and border.

Put it at the top of every stylesheet. Everyone does.

---

# How to approach a layout

1. **Write the HTML first, with no CSS.** If the page makes sense as a plain stack of content, the structure is right.
2. **Ask whether you need layout CSS at all.** A column of text does not.
3. **One direction? Flexbox. Two? Grid.**
4. **Build the phone version first**, then add `min-width` queries.
5. **Use the browser's layout tools.** Right-click, Inspect. Chrome and Firefox both draw grid lines and flex axes over the page so you can see what your CSS is actually doing.

That last one is worth more than any amount of reading.
