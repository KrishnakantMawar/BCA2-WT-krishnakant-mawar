# Day 23 — External CSS, Classes, IDs & Specificity

📖 **Type:** Theory Session
🕐 **Duration:** 2 Hours
📚 **Unit:** 4 — CSS

---

## Learning Objectives

By the end of this session, students will be able to:
- Create and link external CSS files
- Use classes and IDs effectively
- Understand CSS specificity and cascading rules
- Use advanced selectors (child, sibling, pseudo-class, pseudo-element)

---

## 1. External CSS Workflow

### File Structure

```
project/
├── index.html
├── about.html
├── contact.html
└── css/
    └── style.css
```

> **Code Explanation:**
> - The project folder contains three HTML pages (`index.html`, `about.html`, `contact.html`) and a `css/` subfolder
> - The `style.css` file inside the `css/` folder contains all shared styles
> - This structure keeps files organized — CSS files in their own folder, HTML files at the root
> - All three HTML pages will link to the same `css/style.css` file

### Linking CSS

```html
<!-- index.html -->
<head>
    <link rel="stylesheet" href="css/style.css">
</head>
```

> **Code Explanation:**
> - `<link>` goes inside `<head>` — it loads the external CSS before the page content renders
> - `rel="stylesheet"` tells the browser this link is a CSS file
> - `href="css/style.css"` is the relative path — go into the `css/` folder, then find `style.css`
> - This same `<link>` tag goes in ALL three HTML pages — change the CSS file once, all pages update

> **Benefit:** Change `style.css` once → every page updates automatically. Perfect for multi-page websites.

---

## 2. Advanced Selectors

### Combinator Selectors

| Selector | Example | Selects |
|----------|---------|---------|
| Descendant | `div p` | `<p>` anywhere inside `<div>` |
| Child | `div > p` | `<p>` direct child of `<div>` |
| Adjacent sibling | `h2 + p` | First `<p>` right after `<h2>` |
| General sibling | `h2 ~ p` | All `<p>` after `<h2>` (same parent) |

```css
/* Only paragraphs DIRECTLY inside article */
article > p { color: #333; }

/* First paragraph after any heading */
h2 + p { font-size: 1.1em; font-weight: 600; }
```

> **Code Explanation:**
> - `article > p { color: #333; }` — the `>` means "direct child only." A `<p>` inside a `<div>` inside `<article>` would NOT be selected
> - `h2 + p { font-size: 1.1em; font-weight: 600; }` — the `+` means "immediately next sibling." Only the first `<p>` right after an `<h2>` gets styled, not all paragraphs

### Attribute Selectors

```css
/* Input with type="email" */
input[type="email"] { border: 2px solid #1565C0; }

/* Links that open in new tab */
a[target="_blank"] { color: #E91E63; }

/* Links starting with https */
a[href^="https"] { color: green; }

/* Links ending with .pdf */
a[href$=".pdf"]::after { content: " 📄"; }
```

> **Code Explanation:**
> - `input[type="email"]` selects only email input fields — useful for giving different field types different styles
> - `a[target="_blank"]` selects links that open in a new tab — you might want to style them differently to warn users
> - `a[href^="https"]` — the `^=` means "starts with" — selects secure links
> - `a[href$=".pdf"]::after { content: " 📄"; }` — the `$=` means "ends with" — adds a PDF icon after PDF links automatically

### Pseudo-Class Selectors

```css
/* Mouse hover */
a:hover { color: #E91E63; text-decoration: underline; }

/* Currently focused input */
input:focus { border-color: #1565C0; outline: none; box-shadow: 0 0 5px rgba(21,101,192,0.3); }

/* First and last child */
li:first-child { font-weight: bold; }
li:last-child { border-bottom: none; }

/* Every odd row (zebra striping) */
tr:nth-child(odd) { background: #f5f5f5; }
tr:nth-child(even) { background: white; }

/* Empty elements */
p:empty { display: none; }
```

> **Code Explanation:**
> - `a:hover` changes the link style when the mouse hovers over it — essential for user feedback
> - `input:focus` styles the currently active input field — the blue border and shadow tell users "you're typing here"
> - `li:first-child` and `li:last-child` select the first and last items in a list — useful for removing borders or adding special styling
> - `tr:nth-child(odd)` and `tr:nth-child(even)` create **zebra striping** — alternating row colors in tables for easier reading
> - `p:empty` hides paragraphs with no content — prevents empty elements from taking up space

### The `:not()` Pseudo-Class — Select Everything EXCEPT

The `:not()` selector lets you exclude specific elements from a rule:

```css
/* Style all paragraphs EXCEPT those with class "skip" */
p:not(.skip) {
    color: #333;
    line-height: 1.8;
}

/* Style all inputs EXCEPT submit buttons */
input:not([type="submit"]) {
    border: 2px solid #ddd;
    padding: 10px;
    border-radius: 5px;
}

/* Style all list items EXCEPT the last one (no bottom border) */
li:not(:last-child) {
    border-bottom: 1px solid #eee;
    padding-bottom: 10px;
}

/* Style all links EXCEPT those with class "btn" */
a:not(.btn) {
    color: #1565C0;
    text-decoration: underline;
}
```

> **Code Explanation:**
> - `p:not(.skip)` selects all `<p>` elements that do NOT have the class "skip" — useful for excluding specific paragraphs from styling
> - `input:not([type="submit"])` styles all input fields except the submit button — so the submit button can have its own special styling
> - `li:not(:last-child)` adds a bottom border to all list items EXCEPT the last one — a very common pattern for menus and lists
> - `a:not(.btn)` styles regular links differently from button-styled links
> - `:not()` counts toward specificity — `:not(.skip)` adds the specificity of `.skip` (0-1-0), not of `:not()` itself

### Pseudo-Element Selectors

```css
/* First letter of paragraph */
p::first-letter {
    font-size: 2em;
    color: #1565C0;
    float: left;
    margin-right: 5px;
}

/* First line of paragraph */
p::first-line { font-weight: bold; }

/* Add content before/after */
.required::after {
    content: " *";
    color: red;
}

.external-link::after {
    content: " ↗";
}
```

> **Code Explanation:**
> - `p::first-letter` styles only the first letter — creating a "drop cap" effect like in newspapers and magazines
> - `p::first-line` styles only the first line — making it bold draws the reader's eye
> - `.required::after { content: " *"; color: red; }` adds a red asterisk after elements with class "required" — commonly used in forms to mark mandatory fields
> - `::before` and `::after` insert content via CSS without changing HTML — very useful for decorative elements
> - Note: pseudo-elements use `::` (double colon), while pseudo-classes use `:` (single colon)

---

## 3. CSS Specificity

> **Analogy:** Specificity is like a **priority system**. Imagine a chain of command in the military — a General's order (ID) overrides a Colonel's (class), which overrides a Soldier's (element).

### Specificity Calculation

| Selector Type | Weight | Example |
|-------------- |--------|---------|
| Inline style | 1000 | `style="color:red"` |
| ID | 100 | `#header` |
| Class, attribute, pseudo-class | 10 | `.highlight`, `:hover` |
| Element, pseudo-element | 1 | `p`, `::first-line` |

### Examples

```css
p { color: blue; }                    /* Specificity: 0-0-1 = 1 */
.text { color: green; }              /* Specificity: 0-1-0 = 10 */
#intro { color: red; }               /* Specificity: 1-0-0 = 100 */
p.text { color: orange; }            /* Specificity: 0-1-1 = 11 */
#intro p.text { color: purple; }     /* Specificity: 1-1-1 = 111 */
```

> **Code Explanation:**
> - `p` (one element) = specificity **0-0-1** — the weakest selector
> - `.text` (one class) = specificity **0-1-0** — beats any number of element selectors
> - `#intro` (one ID) = specificity **1-0-0** — beats any number of class selectors
> - `p.text` (one element + one class) = **0-1-1** — slightly more specific than just `.text`
> - `#intro p.text` (one ID + one class + one element) = **1-1-1** — the most specific rule here
> - The element with all these rules would use the color from the **highest specificity** rule

### Step-by-Step Specificity Calculation

To calculate specificity, count the number of each selector type and write it as three numbers: **IDs - Classes - Elements**

**Walkthrough Example:**

```css
/* Selector: nav ul li a.active */

/* Step 1: Count IDs → 0 (no # symbols) */
/* Step 2: Count Classes/Attributes/Pseudo-classes → 1 (.active) */
/* Step 3: Count Elements/Pseudo-elements → 4 (nav, ul, li, a) */
/* Specificity: 0-1-4 */

/* Selector: #main-nav .menu li a:hover */

/* Step 1: Count IDs → 1 (#main-nav) */
/* Step 2: Count Classes/Pseudo-classes → 2 (.menu, :hover) */
/* Step 3: Count Elements → 2 (li, a) */
/* Specificity: 1-2-2 */

/* Selector: div#sidebar ul.nav-list li.active a */

/* Step 1: Count IDs → 1 (#sidebar) */
/* Step 2: Count Classes → 2 (.nav-list, .active) */
/* Step 3: Count Elements → 4 (div, ul, li, a) */
/* Specificity: 1-2-4 */
```

> **Code Explanation:**
> - **Rule:** Always count IDs first (worth the most), then classes/pseudo-classes, then elements
> - `nav ul li a.active` has 0 IDs, 1 class (`.active`), and 4 elements = **0-1-4**
> - `#main-nav .menu li a:hover` has 1 ID, 2 classes (`.menu` + `:hover`), and 2 elements = **1-2-2**
> - A selector with even one ID (1-0-0) will ALWAYS beat a selector with only classes (0-5-0), no matter how many classes
> - Think of it like Indian currency: 1 note of ₹100 beats 99 coins of ₹1

**Practice: Which Color Wins?**

```css
/* Scenario: A paragraph inside a div with class and ID */
/* <div id="content" class="main"> <p class="intro">Hello</p> </div> */

p { color: blue; }                    /* 0-0-1 → Lowest */
.intro { color: green; }              /* 0-1-0 → Higher than above */
div p { color: orange; }              /* 0-0-2 → Lower than .intro! */
.main .intro { color: pink; }         /* 0-2-0 → Higher than .intro */
#content .intro { color: red; }       /* 1-1-0 → Highest — RED wins! */
div.main p.intro { color: yellow; }   /* 0-2-2 → Still lower than #content rule */
```

> **Code Explanation:**
> - `p` has specificity 0-0-1 (just one element)
> - `.intro` has 0-1-0 — one class beats any number of elements
> - `div p` has 0-0-2 — two elements, but still less than one class (0-1-0)
> - `.main .intro` has 0-2-0 — two classes
> - `#content .intro` has 1-1-0 — **the ID makes this the winner** over everything else
> - `div.main p.intro` has 0-2-2 — even though it has more total "points," the ID rule still wins because 1-1-0 > 0-2-2
> - **The paragraph text will be RED**

### The Cascade Order

When multiple rules conflict, the browser resolves using:
1. **Importance** — `!important` wins (but avoid using it)
2. **Specificity** — Higher specificity wins
3. **Source Order** — Last rule wins (if specificity is equal)

```css
p { color: blue; }
p { color: red; }     /* Red wins — same specificity, later in file */

.text { color: green; }
p { color: red; }       /* Green wins — class (10) > element (1) */
```

> **Code Explanation:**
> - First example: Two `p` rules with identical specificity (0-0-1) — the **last one wins** because it comes later in the file, so text is red
> - Second example: `.text` (0-1-0) vs `p` (0-0-1) — class beats element selector, so text is green even though `p { color: red }` comes later
> - **Key rule:** Specificity always wins over source order. Source order is only the tiebreaker when specificities are equal

### Debugging Specificity — When Your Styles Don't Apply

If you wrote a CSS rule but it's not working, here's how to investigate:

**Step 1: Right-click the element → "Inspect" (opens DevTools)**

In Chrome/Edge DevTools, you'll see:
- All CSS rules applying to the selected element
- Rules that are **overridden** appear with a ~~strikethrough~~
- The winning rule appears at the top

**Step 2: Check These Common Issues:**

| Problem | Cause | Solution |
|---------|-------|----------|
| Style has ~~strikethrough~~ | Another rule has higher specificity | Increase your selector's specificity |
| Style doesn't appear at all | Selector doesn't match the element | Check for typos in class/ID names |
| Style appears but element looks wrong | Another property overrides it | Check for shorthand properties that reset values |
| `!important` is overriding your style | Someone used `!important` | Use `!important` back (bad) or increase specificity (good) |

**Step 3: Quick Fixes (in order of preference):**

```css
/* ❌ BAD: Using !important — creates maintenance nightmare */
p { color: red !important; }

/* ✅ BETTER: Add a class for more specificity */
p.my-text { color: red; }      /* 0-1-1 beats 0-0-1 */

/* ✅ BEST: Use a more specific selector */
.content p.my-text { color: red; }  /* 0-2-1 — even more specific */
```

> **Code Explanation:**
> - `!important` forces a style to win regardless of specificity — but it makes debugging harder and should be avoided
> - Adding a class (`.my-text`) increases specificity naturally — this is the recommended approach
> - Using a parent class (`.content p.my-text`) adds even more specificity without resorting to `!important`
> - **Rule of thumb:** If you need `!important`, your CSS structure probably needs rethinking

---

## 4. Organizing CSS

### Good Practices

```css
/* =========================
   1. Reset / Base Styles
   ========================= */
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: 'Segoe UI', sans-serif;
    font-size: 16px;
    line-height: 1.6;
    color: #333;
}

/* =========================
   2. Layout
   ========================= */
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
}

/* =========================
   3. Components
   ========================= */
.card {
    background: white;
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.btn {
    display: inline-block;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    font-size: 16px;
}
.btn-primary { background: #1565C0; color: white; }
.btn-success { background: #4CAF50; color: white; }

/* =========================
   4. Utility Classes
   ========================= */
.text-center { text-align: center; }
.mt-20 { margin-top: 20px; }
.mb-20 { margin-bottom: 20px; }
```

> **Code Explanation:**
> - **Section 1 (Reset):** Universal reset removes browser defaults; body sets base typography for the entire page
> - **Section 2 (Layout):** `.container` is a centered wrapper — `max-width: 1200px` prevents content from stretching too wide on large screens
> - **Section 3 (Components):** Reusable building blocks like `.card` and `.btn` — each can be used on any page
> - **`.btn-primary` and `.btn-success`:** Modifier classes that change the button's color — similar to how Bootstrap works
> - **Section 4 (Utility):** Single-purpose helper classes like `.text-center` — small, reusable, and can be combined with other classes
> - This organization follows the **ITCSS** (Inverted Triangle CSS) pattern — from general styles to specific components to tiny utilities

---

## Practice Exercise

1. Create a multi-page mini website (3 pages) sharing one external CSS file:
   - `index.html` — Home page
   - `about.html` — About page
   - `contact.html` — Contact page
   - `css/style.css` — Shared stylesheet

2. Use at least 5 different selector types: element, class, ID, pseudo-class, attribute.

3. Create a specificity challenge: write conflicting rules and predict which color wins.

---

## Summary

| Concept | Key Takeaway |
|---------|-------------|
| External CSS | One `.css` file, many HTML pages |
| Child selector | `div > p` — direct children only |
| Pseudo-class | `:hover`, `:nth-child()`, `:focus` |
| Pseudo-element | `::first-letter`, `::before`, `::after` |
| Specificity | ID (100) > Class (10) > Element (1) |
| Cascade | Last rule wins if specificity is equal |

---

*Day 23 of 55 | Unit 4 — CSS | Web Technology (25BCA060)*
