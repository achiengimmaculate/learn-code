# Consolidation project: one page, everything I know

## The point of this

Nine projects so far, every one of them starting from a file MDN gave me. This one starts from an empty folder.

That is the whole difference. It is going to be slower and more uncomfortable, and that discomfort is the thing that turns "I have seen this" into "I can do this."

## Pick a subject

It must be something I already know, so I never have to invent content. Suggestions:

- Interior design, since I keep coming back to it
- Nebula
- IMAKEL SYSTEMS, what I do and what it costs
- A place in Nakuru I know well

One subject, one page.

## What it has to contain

Everything below appears somewhere in weeks 1 to 3. Nothing here is new.

### Stage 1: skeleton
- Doctype, `html` with `lang`, `head`, `body`
- `charset` and `viewport` meta tags
- A real `<title>`
- A linked external stylesheet, in its own file

### Stage 2: structure
- `<header>` with a heading and a `<nav>`
- `<main>` containing at least four `<section>` elements, each with an `id`
- `<footer>`
- Exactly one `<h1>`, and `<h2>` for each section

### Stage 3: content
- Real paragraphs, written by me
- `<strong>` and `<em>` used where they genuinely belong
- A `<ul>` and an `<ol>`, each chosen for the right reason
- At least two links, one external and one fragment link to a section
- An image in a `<figure>` with a `<figcaption>` and proper `alt`

### Stage 4: a table
- `<caption>`, `<thead>`, `<tbody>`
- `<th>` with `scope`
- At least three columns of real data

### Stage 5: a form
- A `<form>` with at least three fields
- Every field has a `<label>` properly joined to its input
- A submit `<button>`
- It does not need to go anywhere

### Stage 6: layout
- The nav laid out with **flexbox**
- At least one section laid out with **grid**
- The page centred with `max-width` and `margin: 0 auto`
- `box-sizing: border-box` set once at the top

### Stage 7: styling and responsive
- A colour scheme, three or four colours, chosen deliberately
- Typography: a font stack, sizes, `line-height`
- Spacing done with `margin` and `padding` on purpose, not by guessing
- **Mobile first**: plain CSS for small screens, then a `@media` query widening it
- Works at 375px wide and at full desktop

## How we work through it

One stage at a time.

1. I read the stage.
2. **Before I write it**, Claude explains the concepts involved and answers my questions. No code from Claude.
3. I build that stage myself.
4. Claude reviews what I wrote, line by line, and explains every block of it back to me, including the bits that are right.
5. I commit before moving on.

That last point is not optional. Seven stages, seven commits.

## The rules

- **No copying from the MDN challenge files.** Reading the docs to look something up is fine. Opening a finished file and lifting from it is not.
- **Console open, always.** Check it every time I reload.
- **If I get stuck for more than fifteen minutes**, say what I tried and what I expected. Being stuck is information, not failure.

## When it is finished

- Push it to GitHub
- Fill in `NOTES.md` properly, including what I had to look up
- Whatever I had to look up is what I do not know yet, and that is the honest result of this exercise
