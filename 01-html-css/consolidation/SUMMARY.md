# What I have learned: weeks 1 to 3

21 September to 7 October 2026. HTML and CSS.

This is taken from what is actually in my repo, not from what I was supposed to cover.

---

## HTML

### The document
- `<!DOCTYPE html>`, `<html lang>`, `<head>`, `<body>`
- `<meta charset="utf-8">` so characters do not turn into rubbish
- `<meta name="viewport">` so phones do not render a shrunken desktop page
- `<title>` for the browser tab
- `<link rel="stylesheet" href>` to attach CSS
- `<script src defer></script>` to attach JavaScript

### Text
- `<h1>` once per page, then `<h2>`, `<h3>` as a hierarchy, never for size
- `<p>` for paragraphs
- `<strong>` for importance, `<em>` for emphasis
- `<!-- comments -->`

### Lists
- `<ul>` when order does not matter
- `<ol>` when order does matter
- `<li>` for each item

### Links
- `<a href>`, absolute (`https://...`) and relative (`styles.css`, `../index.html`)
- Fragment links `href="#section-id"` pointing at an `id`
- `target="_blank"` with `rel="noopener noreferrer"`

### Images and media
- `<img src alt width height>`
- `alt` describes what the image shows, empty `alt=""` if purely decorative
- `<figure>` and `<figcaption>`
- `<video src autoplay loop muted>`

### Semantic structure
- `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`
- `<div>` only when nothing more specific fits

### Tables
- `<table>`, `<caption>`, `<thead>`, `<tbody>`
- `<th>` versus `<td>`
- `scope="col"`, `scope="row"`, `scope="rowgroup"`
- `colspan`, `rowspan`

### Forms
- `<form>`, `<label>`, `<input>`, `<button>`
- Different input types

---

## CSS

### How it works
- `selector { property: value; }`
- Three ways to attach it: external file, `<style>` in the head, inline
- **CSS fails silently.** A wrong property or value is thrown away with no error.
- The cascade: later rules win, more specific rules win

### Selectors
- Element: `h1`, `p`, `a`
- Class: `.feature`, `.grid`
- Universal: `*`
- Descendant: `nav ul`
- Pseudo-class: `a:hover`, `a:focus`
- Pseudo-element: `h1::before`, `::after` with `content`
- Attribute: `a[href^="http"]`

### The box model
- `box-sizing: border-box`, and why it makes sizing sane
- `margin`, `border`, `padding`, `width`, `height`
- `max-width`, `min-width`
- Shorthand order: one value all sides, two is vertical/horizontal, four is clockwise from top

### Colour and background
- Named colours, hex `#333333`, `rgb()`
- `color`, `background-color`
- `background-image`, `background-size`, gradients

### Typography
- `font-family`, `font-size`, `font-weight`, `font-style`
- `line-height`, `letter-spacing`, `text-align`, `text-indent`
- `text-transform`, `text-decoration`, `text-shadow`
- Web fonts from Google Fonts
- Units: `px`, `em`, `rem`, `%`, `vw`, and `calc()`

### Layout
- **Normal flow**, block versus inline
- **Flexbox**: `display: flex`, `justify-content`, `align-items`, `gap`
- **Grid**: `display: grid`, `grid-template-columns`, `fr` units, `gap`
- **Float**: `float: left` for text wrapping
- **Positioning**: `position: sticky` with `top: 0`
- Centring with `margin: 0 auto` and a `max-width`

### Responsive
- Mobile first: write the small screen, then add media queries upward
- `@media` queries
- `max-width: 100%` on images

### Nesting
- Modern CSS can nest rules
- Inside a nested rule, `&` means the parent
- Repeating the parent name makes a descendant selector instead, which usually matches nothing

---

## Bugs I have personally made, and what they taught me

| What happened | The lesson |
|---|---|
| `images/ Nebula.jpeg` had a hidden leading space | Filenames match exactly or not at all |
| `script.js` when the file was at `script/script.js` | Check the folder, not just the name |
| `style.css` when the file was `styles.css` | One letter is enough to break it |
| `markup.html` was 0 bytes while 33 lines sat unsaved | The editor and the disk are different places |
| `<style>` instead of `</style>` | A missing slash swallows everything after it |
| `overflow: content` | Property on the left, value on the right |
| `margin: right 20px` | Properties only accept certain value shapes |
| `h1::before` nested inside `h1` | Nested rules need `&`, not the repeated name |
| Deleted my notes file before copying it | Commit before you delete |

**The habit that catches most of these:** open the browser console. Right-click, Inspect, Console. A 404 tells you exactly which file the browser wanted and could not find.

---

## What I can do now that I could not on 21 September

- Write a complete HTML page from an empty file
- Choose tags based on what the content *is*
- Attach and debug a stylesheet
- Lay out a page with grid and flexbox
- Make a page work on a phone
- Read a browser console and find a broken path
- Use git: `status`, `add`, `commit`, `push`
