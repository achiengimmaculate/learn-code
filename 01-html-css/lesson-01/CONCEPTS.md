# Week 1 Concepts: HTML

Read this before the freeCodeCamp work, then again after. It covers the things tutorials skip because they assume you already know them.

---

## 1. What a web page actually is

A web page is a **text file**. That is the whole secret.

When you visit a website, a computer somewhere sends your browser a file full of text. Your browser reads that text and draws it on screen. There is no magic layer. The file you write in week 1 is the same kind of file that runs Lucim Polls.

The `.html` extension tells the browser "read this as HTML."

## 2. What HTML is for

HTML answers one question about every piece of content: **what is this?**

Not what colour it is. Not how big. Just what it is. This is a heading. This is a paragraph. This is a list. This is a link.

Why this matters practically:
- **Screen readers** read pages aloud to blind users. They rely entirely on what you said things *are*.
- **Google** decides what your page is about by reading your structure.
- **CSS** can only style things properly if they are labelled properly.

When you use the wrong tag to get a look you want, you break all three.

## 3. Tags, elements, attributes

```html
<a href="https://example.com">Click me</a>
```

- `<a>` is the **opening tag**
- `</a>` is the **closing tag**, note the slash
- `Click me` is the **content**
- The whole thing is an **element**
- `href="https://example.com"` is an **attribute**, extra information about the element

Most elements have an opening and closing tag. A few do not, because they have no content to wrap:

```html
<img src="cat.jpg" alt="A ginger cat asleep on a keyboard">
```

`<img>` is self-closing. There is nothing to put inside it.

## 4. Nesting

Elements go inside other elements, like boxes inside boxes:

```html
<ul>
  <li>First thing</li>
  <li>Second thing</li>
</ul>
```

**The rule: what opens last must close first.** This is correct:

```html
<p>Some <strong>bold</strong> text</p>
```

This is broken, even though browsers will try to guess what you meant:

```html
<p>Some <strong>bold</p></strong>
```

Indentation is how you see nesting. It does nothing to the page, but it is how you avoid going mad.

## 5. The skeleton every page has

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>Shows in the browser tab</title>
  </head>
  <body>
    <!-- everything the user sees goes here -->
  </body>
</html>
```

- `<!DOCTYPE html>` tells the browser to use modern rules. It is not really a tag. Just always write it.
- `<html lang="en">` wraps everything. The `lang` matters for screen readers and translation.
- `<head>` is information **about** the page. The user does not see it.
- `<body>` is the page itself. Everything visible lives here.

**Head versus body is the thing beginners mix up most.** Title, character set, links to stylesheets go in the head. Text, images, buttons go in the body.

## 6. Headings are a hierarchy, not sizes

```html
<h1>Main title of the page</h1>
  <h2>A major section</h2>
    <h3>A subsection of that section</h3>
  <h2>Another major section</h2>
```

Think of it as a table of contents. `h1` is the book title, `h2` are chapters, `h3` are sections within a chapter.

Rules:
- **One `h1` per page.** It is the page's name.
- **Never skip levels.** An `h3` should not follow an `h1` directly.
- **Never pick a heading level because of its size.** If you want big text, that is CSS's job, coming in week 2.

## 7. Semantic tags

"Semantic" just means "the name says what it is."

Compare:

```html
<div>My navigation</div>
<nav>My navigation</nav>
```

Both look identical on screen. But `<div>` means "a box, no idea what of" and `<nav>` means "this is the navigation." A screen reader can offer to skip `<nav>`. It cannot do anything with a `<div>`.

Useful ones: `<header>`, `<nav>`, `<main>`, `<section>`, `<article>`, `<aside>`, `<footer>`.

Rule of thumb: **use `<div>` only when nothing more specific fits.**

## 8. Alt text

```html
<img src="photo.jpg" alt="Contestants lined up on stage at the Nakuru pageant">
```

`alt` is what shows if the image fails to load, and what a screen reader says out loud. It is not optional and it is not decoration.

Write what the image **shows**, not what it is. "Photo" and "image1.jpg" are useless. Describe it as if to someone on the phone.

One exception: if an image is purely decorative and carries no meaning, use `alt=""`, empty but present. That tells screen readers to skip it.

## 9. Comments

```html
<!-- This is a comment. It does not show on the page. -->
```

Use them to leave notes for yourself.

---

## Check yourself

Can you answer these without scrolling up?

1. What is the difference between `<head>` and `<body>`?
2. Why is it wrong to pick `<h3>` because you want smaller text?
3. What does `alt` do, and when should it be empty?
4. What is the difference between a tag and an element?
5. Why use `<nav>` instead of `<div>` when they look the same?

If any answer is shaky, that is exactly what your `NOTES.md` is for.
