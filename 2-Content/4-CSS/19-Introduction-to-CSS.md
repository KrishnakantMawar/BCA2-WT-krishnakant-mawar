# Day 19 — Introduction to CSS

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 4 — CSS (Cascading Style Sheets)
🧪 **Lab Experiment:** 10

---

## Learning Objectives

By the end of this session, students will be able to:
- Explain what CSS is and why it's needed
- Write CSS using all three methods: inline, internal, and external
- Understand CSS syntax (selectors, properties, values)
- Apply basic styling to HTML elements

---

## 1. What is CSS?

> **Analogy:** If HTML is the **skeleton** of a building (structure), CSS is the **paint, wallpaper, flooring, and furnishing** (appearance). The same skeleton can look completely different with different CSS — modern, traditional, minimalist, or colorful.

**CSS = Cascading Style Sheets**
- **Cascading**: Styles can come from multiple sources and are applied in a specific order of priority
- **Style Sheets**: Files/rules that define how HTML elements look

### Why CSS?

| Without CSS | With CSS |
|-------------|----------|
| Plain black text on white | Colors, fonts, spacing |
| No layout control | Multi-column layouts |
| Content and style mixed | Separation of concerns |
| Change style = change every page | Change one CSS file = change entire website |

### Understanding "Cascading" in CSS

The word **"Cascading"** means styles flow down from multiple sources, like a waterfall. When there's a conflict (e.g., two rules set different colors for the same element), the browser resolves it using this priority order:

| Priority | Source | Example |
|----------|--------|---------|
| 1 (Lowest) | **Browser defaults** | Browsers make `<h1>` large and bold by default |
| 2 | **External CSS** | Rules in a linked `.css` file |
| 3 | **Internal CSS** | Rules inside `<style>` in `<head>` |
| 4 (Highest) | **Inline CSS** | `style="..."` directly on the element |

> **Analogy:** Think of it like a **government order chain**. The Central Government (inline) overrides the State Government (internal), which overrides the Municipal Corporation (external), which overrides the default rules (browser).

**Example of Cascade:**
```css
/* External CSS file (priority 2) */
p { color: blue; }
```
```html
<!-- Internal CSS (priority 3) — overrides external -->
<style>
    p { color: green; }
</style>

<!-- Inline CSS (priority 4) — overrides everything -->
<p style="color: red;">This text will be RED</p>
```

> **Code Explanation:**
> - The external CSS sets all `<p>` text to blue
> - The internal CSS overrides it to green (higher priority)
> - The inline style overrides everything — the paragraph appears **red**
> - If you remove the inline style, the text becomes green; remove internal too, it becomes blue

### How the Browser Renders CSS

When you open a webpage, the browser follows these steps:

```
Step 1: Download HTML → Build the DOM (Document Object Model) tree
Step 2: Download CSS  → Build the CSSOM (CSS Object Model) tree
Step 3: Combine DOM + CSSOM → Create the Render Tree
Step 4: Calculate Layout (position, size of each element)
Step 5: Paint pixels on screen
```

> **Analogy:** It's like building a house:
> 1. **DOM** = The blueprint (structure)
> 2. **CSSOM** = The interior design plan (styles)
> 3. **Render Tree** = Combining both to know what to build and how it looks
> 4. **Layout** = Measuring and placing furniture
> 5. **Paint** = Actually painting the walls and placing everything

> **Why this matters:** If your CSS file is very large or loads slowly, the browser may show unstyled content briefly (called **FOUC — Flash of Unstyled Content**). That's why we put CSS links in the `<head>` — so styles load before content appears.

### CSS Reset — Starting with a Clean Slate

Different browsers have different default styles. For example:
- Chrome adds `8px` margin to `<body>`
- Firefox might render `<h1>` slightly differently than Edge

To make your website look the **same across all browsers**, developers use a CSS Reset:

```css
/* Universal CSS Reset — removes all browser defaults */
* {
    margin: 0;          /* Remove default margins */
    padding: 0;         /* Remove default padding */
    box-sizing: border-box; /* Include padding/border in width */
}
```

> **Code Explanation:**
> - `*` is the **universal selector** — it targets every single HTML element on the page
> - `margin: 0` removes the default spacing outside elements (e.g., the 8px body margin)
> - `padding: 0` removes the default spacing inside elements (e.g., padding in `<ul>` lists)
> - `box-sizing: border-box` changes how width is calculated — padding and border are included inside the width, making layout math much simpler

> **Tip:** Almost every professional website starts their CSS with this reset. You'll see it in every example in this course.

---

## 2. CSS Syntax

```css
selector {              /* Declaration block starts */
    property: value;    /* A style declaration */
    property: value;    /* Another style declaration */
}                       /* Declaration block ends */
```

> **Code Explanation:**
> - `selector` determines which HTML element(s) the style rules will apply to (e.g., `h1`, `.classname`, `#id`)
> - Inside the curly braces `{ }`, each line is a **declaration** consisting of a `property: value;` pair
> - The property is what you want to change (e.g., `color`, `font-size`), and the value is what you change it to
> - Each declaration must end with a semicolon (`;`)

**Example:**
```css
h1 {
    color: blue;         /* Change text color to blue */
    font-size: 24px;     /* Set text size to 24 pixels */
    text-align: center;  /* Center the text horizontally */
}
```

> **Code Explanation:**
> - `h1` is the **selector** — it targets all `<h1>` heading elements on the page
> - `color: blue;` changes the text color to blue
> - `font-size: 24px;` sets the text size to 24 pixels
> - `text-align: center;` centers the text horizontally within its container
> - Each declaration ends with a semicolon (`;`)
> - All declarations are wrapped inside curly braces `{ }`

| Part | What It Means |
|------|---------------|
| `h1` | Selector — which elements to style |
| `color` | Property — what aspect to change |
| `blue` | Value — what to change it to |
| `{ }` | Declaration block |
| `;` | End of each declaration |

---

## 3. Three Ways to Add CSS

### 1. Inline CSS (on the element itself)

```html
<!-- Inline CSS: style attribute applied directly on each element -->
<h1 style="color: red; font-size: 30px;">Hello World</h1>
<p style="background-color: yellow; padding: 10px;">Styled paragraph</p>
```

> **Code Explanation:**
> - `style="color: red; font-size: 30px;"` applies CSS directly on the `<h1>` element
> - `style="background-color: yellow; padding: 10px;"` gives the paragraph a yellow background with 10px inner spacing
> - Inline styles have the **highest priority** but are hard to maintain — imagine changing the color on 100 elements!

**Pros:** Quick for testing
**Cons:** Repetitive, hard to maintain, mixes content and style

### 2. Internal CSS (in the `<head>` with `<style>`)

```html
<head>
    <style>
        /* Styles for all h1 elements on this page */
        h1 {
            color: navy;        /* Dark blue heading text */
            text-align: center; /* Center-aligned headings */
        }
        /* Styles for all p elements on this page */
        p {
            font-size: 16px;   /* Readable text size */
            line-height: 1.6;  /* Comfortable line spacing */
        }
    </style>
</head>
```

> **Code Explanation:**
> - The `<style>` tag goes inside `<head>` — it contains CSS rules for this page only
> - `h1 { color: navy; text-align: center; }` makes all `<h1>` elements navy blue and centered
> - `p { font-size: 16px; line-height: 1.6; }` makes paragraphs 16px with 1.6× line spacing for readability
> - This approach keeps styles separate from HTML content, but only works for one page

**Pros:** Styles for one page in one place
**Cons:** Must repeat on every page

### 3. External CSS (separate .css file) ✅ **Best Practice**

**style.css:**
```css
/* Styles for all h1 elements */
h1 {
    color: navy;         /* Dark blue heading text */
    text-align: center;  /* Center-aligned headings */
}
/* Styles for all p elements */
p {
    font-size: 16px;     /* Readable text size */
    line-height: 1.6;    /* Comfortable line spacing */
}
```

> **Code Explanation:**
> - This is a separate file called `style.css` containing the same rules as internal CSS
> - Any HTML page that links to this file will get these styles automatically
> - If you change `color: navy` to `color: green` here, ALL linked pages update at once

**index.html:**
```html
<head>
    <!-- Link to external CSS file for styling -->
    <link rel="stylesheet" href="style.css">
</head>
```

> **Code Explanation:**
> - `<link>` tells the browser to load an external resource
> - `rel="stylesheet"` means "this is a CSS file"
> - `href="style.css"` is the path to the CSS file (relative to the HTML file)
> - This single line connects the HTML page to the external stylesheet

**Pros:** One file styles the entire website; clean separation
**Cons:** Extra HTTP request (minimal impact)

---

## 4. CSS Selectors

| Selector | Example | Selects |
|----------|---------|---------|
| Element | `p { }` | All `<p>` elements |
| Class | `.highlight { }` | Elements with `class="highlight"` |
| ID | `#header { }` | Element with `id="header"` |
| Universal | `* { }` | All elements |
| Group | `h1, h2, h3 { }` | Multiple elements |
| Descendant | `div p { }` | `<p>` inside `<div>` |

### Class vs ID

```html
<!-- Class: reusable (can apply to many elements) -->
<p class="highlight">This is highlighted</p>
<p class="highlight">This too</p>

<!-- ID: unique (one per page) -->
<div id="header">Only one header</div>
```

> **Code Explanation:**
> - `class="highlight"` is applied to two `<p>` elements — classes can be reused on multiple elements
> - `id="header"` is applied to one `<div>` — IDs must be unique, used only once per page
> - Think of class as a "category" (like all BCA students) and ID as a "roll number" (unique to one student)

```css
.highlight { background-color: yellow; }  /* Class: dot prefix */
#header { background-color: navy; }        /* ID: hash prefix */
```

> **Code Explanation:**
> - `.highlight` uses a **dot (.)** prefix — this is how you write a class selector
> - `#header` uses a **hash (#)** prefix — this is how you write an ID selector
> - Classes can be reused on many elements; IDs should be unique (one per page)
> - Think of class as "category" (many students in BCA) and ID as "roll number" (unique to each student)

---

## 5. Common CSS Properties

### Text Properties

| Property | Values | Example |
|----------|--------|---------|
| `color` | Color name, hex, rgb | `color: #1565C0;` |
| `font-size` | px, em, rem, % | `font-size: 18px;` |
| `font-family` | Font names | `font-family: Arial, sans-serif;` |
| `font-weight` | normal, bold, 100-900 | `font-weight: bold;` |
| `font-style` | normal, italic | `font-style: italic;` |
| `text-align` | left, center, right, justify | `text-align: center;` |
| `text-decoration` | none, underline, line-through | `text-decoration: none;` |
| `text-transform` | uppercase, lowercase, capitalize | `text-transform: uppercase;` |
| `line-height` | Number, px | `line-height: 1.6;` |
| `letter-spacing` | px | `letter-spacing: 2px;` |

---

## Practical Session

### 🧪 Lab Experiment 10: CSS Styling

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS Styling Demo</title>
    <style>
        /* Universal reset */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, sans-serif;
            line-height: 1.6;
            color: #333;
            background-color: #f4f4f4;
        }

        /* Header styling */
        header {
            background-color: #1565C0;
            color: white;
            text-align: center;
            padding: 30px 20px;
        }
        header h1 {
            font-size: 32px;
            letter-spacing: 2px;
            text-transform: uppercase;
        }
        header p {
            font-size: 14px;
            margin-top: 5px;
            opacity: 0.8;
        }

        /* Navigation */
        nav {
            background-color: #0D47A1;
            padding: 12px;
            text-align: center;
        }
        nav a {
            color: white;
            text-decoration: none;
            margin: 0 15px;
            font-size: 16px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        /* Main content */
        main {
            max-width: 800px;
            margin: 30px auto;
            padding: 0 20px;
        }

        /* Article styling */
        article {
            background: white;
            padding: 25px;
            margin-bottom: 20px;
            border-left: 4px solid #1565C0;
        }
        article h2 {
            color: #1565C0;
            margin-bottom: 10px;
        }
        article p {
            font-size: 16px;
            color: #555;
        }

        /* Highlight class */
        .highlight {
            background-color: #FFF9C4;
            padding: 2px 8px;
            font-weight: bold;
        }

        /* Important class */
        .important {
            color: #C62828;
            font-weight: bold;
        }

        /* Footer */
        footer {
            background: #333;
            color: white;
            text-align: center;
            padding: 15px;
            font-size: 14px;
        }
    </style>
</head>
<body>

    <header>
        <h1>Mandsaur University</h1>
        <p>Department of Computer Applications</p>
    </header>

    <nav>
        <a href="#">Home</a>
        <a href="#">About</a>
        <a href="#">Courses</a>
        <a href="#">Contact</a>
    </nav>

    <main>
        <article>
            <h2>Welcome to BCA Program</h2>
            <p>The <span class="highlight">Bachelor of Computer Applications</span> 
               program prepares students for the IT industry with a blend of 
               theoretical knowledge and practical skills.</p>
        </article>

        <article>
            <h2>Web Technology Course</h2>
            <p>In this course, you will learn HTML, CSS, JavaScript, and Bootstrap.
               <span class="important">Attendance above 75% is mandatory.</span></p>
        </article>

        <article>
            <h2>CSS Styling</h2>
            <p>Today we learned three ways to add CSS:
               <span class="highlight">inline</span>, 
               <span class="highlight">internal</span>, and 
               <span class="highlight">external</span>.
               External CSS is the recommended approach.</p>
        </article>
    </main>

    <footer>
        <p>&copy; 2026 Mandsaur University. All Rights Reserved.</p>
    </footer>

</body>
</html>
```

> **Code Explanation:**
> - **Universal Reset (`*`):** Removes default margins/padding and sets `border-box` sizing for all elements
> - **Body:** Sets the base font to 'Segoe UI' with a fallback stack, light gray background (`#f4f4f4`), dark text (`#333`), and comfortable line spacing (1.6)
> - **Header:** Blue background (`#1565C0`) with white centered text, uppercase heading with letter spacing for a professional look
> - **Nav:** Darker blue (`#0D47A1`) with horizontal white links — `text-decoration: none` removes the default underline
> - **Main:** `max-width: 800px` limits content width; `margin: 30px auto` centers it horizontally on the page
> - **Article:** White background with a blue left border (`border-left: 4px solid`) acts as a visual accent; stacked with `margin-bottom: 20px`
> - **`.highlight` class:** Yellow background with bold text — used with `<span>` to highlight key phrases inline
> - **`.important` class:** Red bold text for warnings/notices
> - **Footer:** Dark background with centered white text — standard website footer pattern

---

## Summary

| Concept | Details |
|---------|---------|
| CSS | Cascading Style Sheets — controls appearance |
| Inline CSS | `style="..."` on element |
| Internal CSS | `<style>` in `<head>` |
| External CSS | Separate `.css` file linked with `<link>` |
| Selector | Targets elements: element, `.class`, `#id` |
| Declaration | `property: value;` |
| Best practice | Always use external CSS |

---

*Day 19 of 55 | Unit 4 — CSS | Web Technology (25BCA060)*
