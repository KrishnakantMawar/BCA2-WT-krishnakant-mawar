# Day 24 — CSS Flexbox & Grid Layout

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 4 — CSS

---

## Learning Objectives

By the end of this session, students will be able to:
- Use CSS Flexbox for one-dimensional layouts
- Use CSS Grid for two-dimensional layouts
- Choose between Flexbox and Grid for different scenarios
- Build common layouts (navigation bar, card grid, holy grail)

---

## 1. CSS Flexbox

> **Analogy:** Flexbox is like arranging **chairs in a row** at a conference. You can space them evenly, push them all to one side, center them, or spread them out — all with simple commands to the "row organizer."

### Flex Container

```css
.container {
    display: flex;
}
```

> **Code Explanation:**
> - `display: flex` turns any element into a **flex container** — its direct children become flex items
> - By default, flex items arrange themselves in a **row** (left to right) and try to fit in one line
> - The flex container controls how items are positioned, aligned, and spaced

This turns the container into a **flex container** and its direct children into **flex items**.

### Flex Direction

```css
.row        { flex-direction: row; }           /* → (default) */
.row-rev    { flex-direction: row-reverse; }    /* ← */
.col        { flex-direction: column; }         /* ↓ */
.col-rev    { flex-direction: column-reverse; } /* ↑ */
```

> **Code Explanation:**
> - `row` (default): Items flow left to right →
> - `row-reverse`: Items flow right to left ← (useful for RTL languages like Urdu)
> - `column`: Items stack top to bottom ↓ (like a vertical list)
> - `column-reverse`: Items stack bottom to top ↑
> - Changing flex-direction changes which axis is "main" (for `justify-content`) and which is "cross" (for `align-items`)

### Justify Content (Main Axis)

```css
.start   { justify-content: flex-start; }    /* |■ ■ ■      | */
.end     { justify-content: flex-end; }      /* |      ■ ■ ■| */
.center  { justify-content: center; }        /* |   ■ ■ ■   | */
.between { justify-content: space-between; } /* |■    ■    ■| */
.around  { justify-content: space-around; }  /* | ■   ■   ■ | */
.evenly  { justify-content: space-evenly; }  /* |  ■  ■  ■  | */
```

> **Code Explanation:**
> - `flex-start`: Items pack to the start (left in a row) — like students sitting in the first few seats of a classroom
> - `flex-end`: Items pack to the end (right in a row)
> - `center`: Items group in the middle — perfect for centering content
> - `space-between`: First item at start, last at end, equal space between — like spacing chairs evenly along a wall
> - `space-around`: Equal space around each item — items have half-space at edges
> - `space-evenly`: Perfectly equal space everywhere — between items and at edges

### Align Items (Cross Axis)

```css
.top     { align-items: flex-start; }
.bottom  { align-items: flex-end; }
.center  { align-items: center; }
.stretch { align-items: stretch; }    /* Default — fill height */
```

> **Code Explanation:**
> - `flex-start`: Items align to the top of the container (in a row layout)
> - `flex-end`: Items align to the bottom
> - `center`: Items are vertically centered — the most commonly used value for vertical centering
> - `stretch` (default): Items stretch to fill the container's height — that's why flex items often appear taller than expected

### Flex Wrap

```css
.container {
    display: flex;
    flex-wrap: wrap;     /* Items wrap to next line */
    gap: 15px;           /* Space between items */
}
```

> **Code Explanation:**
> - `flex-wrap: wrap` allows items to move to the next line when they don't fit — without this, items would shrink to fit one line
> - `gap: 15px` adds space between items (both rows and columns) — cleaner than using margin on each item

### `align-content` — Controlling Multiline Flex Spacing

When flex items wrap to multiple lines, `align-content` controls the **space between the lines** (rows):

```css
.multi-row-container {
    display: flex;
    flex-wrap: wrap;           /* Items wrap to create multiple rows */
    height: 400px;             /* Container must have a fixed height */
    align-content: flex-start; /* All rows packed at the top */
}

/* Different align-content values: */
.pack-top      { align-content: flex-start; }    /* Rows at the top */
.pack-bottom   { align-content: flex-end; }      /* Rows at the bottom */
.pack-center   { align-content: center; }        /* Rows in the center */
.space-between { align-content: space-between; } /* First row at top, last at bottom */
.space-around  { align-content: space-around; }  /* Equal space around each row */
.stretch-rows  { align-content: stretch; }       /* Rows stretch to fill height (default) */
```

> **Code Explanation:**
> - `align-content` only works when there are **multiple rows** (i.e., `flex-wrap: wrap` is set) AND the container has extra vertical space
> - `flex-start` packs all rows to the top — any extra space goes to the bottom
> - `space-between` distributes rows evenly — first row touches the top, last row touches the bottom
> - **Common confusion:** `align-items` aligns items within a single row; `align-content` distributes space between multiple rows
> - If you only have one row of items, `align-content` has no effect

| Property | Controls | Works On |
|----------|---------|----------|
| `justify-content` | Space along **main axis** (horizontal in row) | Single or multi-row |
| `align-items` | Alignment of items in **cross axis** (within one row) | Each row individually |
| `align-content` | Space between **multiple rows** | Only multi-row (flex-wrap) |

### Flex Item Properties

```css
.item {
    flex-grow: 1;     /* How much to grow (ratio) */
    flex-shrink: 0;   /* Don't shrink */
    flex-basis: 200px; /* Starting width */
}

/* Shorthand */
.item { flex: 1; }              /* grow:1, shrink:1, basis:0 */
.item { flex: 0 0 200px; }      /* Fixed 200px, no grow/shrink */
```

> **Code Explanation:**
> - `flex-grow: 1` means the item will grow to fill available space. If two items both have `flex-grow: 1`, they share the space equally
> - `flex-shrink: 0` prevents the item from shrinking when the container is too small — useful for fixed-width sidebars
> - `flex-basis: 200px` sets the item's starting width before growing/shrinking — like a "preferred" width
> - `flex: 1` is shorthand for `flex-grow: 1; flex-shrink: 1; flex-basis: 0` — the item will grow and shrink freely
> - `flex: 0 0 200px` means "don't grow, don't shrink, stay at 200px" — useful for fixed-width columns

### Flex Item Order

The `order` property changes the **visual order** of flex items without changing the HTML:

```css
/* Default order is 0 for all items */
.item-1 { order: 3; }  /* Appears last visually */
.item-2 { order: 1; }  /* Appears first visually */
.item-3 { order: 2; }  /* Appears in the middle */

/* Practical example: Move a "Featured" course to the front */
.course-card { order: 0; }               /* All cards: default order */
.course-card.featured { order: -1; }      /* Featured card appears first! */
```

> **Code Explanation:**
> - By default, all flex items have `order: 0` — they appear in the same order as the HTML
> - Lower `order` values appear first, higher values appear last
> - `order: -1` places an item before all items with `order: 0` — useful for "pinning" important items to the front
> - The HTML source order doesn't change — this is purely visual. Screen readers still read in HTML order
> - Think of it like a queue at SBI bank — the VIP counter (order: -1) gets served first regardless of when they arrived

### Flexbox Navigation Bar

```css
nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: #1565C0;
    padding: 15px 30px;
}
nav .logo { color: white; font-size: 1.5em; font-weight: bold; }
nav .links { display: flex; gap: 20px; }
nav a { color: white; text-decoration: none; }
```

> **Code Explanation:**
> - `display: flex` on `nav` arranges the logo and links in a row
> - `justify-content: space-between` pushes the logo to the left and links to the right
> - `align-items: center` vertically centers everything — important when logo and links have different heights
> - `.links { display: flex; gap: 20px; }` makes the links container also a flex container, spacing links 20px apart
> - `text-decoration: none` removes underlines from links — standard practice for navigation menus

---

## 2. CSS Grid

> **Analogy:** If Flexbox is for arranging items in a **single row/column** (like seats in a row), Grid is for arranging items in a **spreadsheet** — rows AND columns simultaneously (like a seating chart for an entire theater).

### Grid Container

```css
.grid {
    display: grid;
    grid-template-columns: 200px 1fr 200px;    /* 3 columns */
    grid-template-rows: auto 1fr auto;          /* 3 rows */
    gap: 20px;
}
```

> **Code Explanation:**
> - `display: grid` activates Grid layout — children are placed into rows and columns
> - `grid-template-columns: 200px 1fr 200px` creates 3 columns: first and last are 200px, middle takes remaining space (`1fr` = 1 fraction)
> - `grid-template-rows: auto 1fr auto` creates 3 rows: first and last size to content, middle fills remaining space
> - `gap: 20px` adds 20px of space between all grid cells (both rows and columns)

### Grid Template Columns

```css
/* Fixed widths */
.grid { grid-template-columns: 200px 300px 200px; }

/* Fractional units (flexible) */
.grid { grid-template-columns: 1fr 2fr 1fr; }
/* 1st: 25%, 2nd: 50%, 3rd: 25% */

/* Repeat */
.grid { grid-template-columns: repeat(3, 1fr); }
/* Three equal columns */

/* Auto-fit responsive */
.grid { grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); }
/* As many 250px+ columns as fit */
```

> **Code Explanation:**
> - `200px 300px 200px` creates three fixed-width columns — simple but not responsive
> - `1fr 2fr 1fr` uses **fractional units** — the total is 4fr, so column 1 gets 25%, column 2 gets 50%, column 3 gets 25%
> - `repeat(3, 1fr)` is shorthand for `1fr 1fr 1fr` — three equal columns
> - `repeat(auto-fit, minmax(250px, 1fr))` is the **responsive magic** — creates as many 250px+ columns as fit, automatically wrapping to new rows. No media queries needed!

### Placing Items

```css
.header  { grid-column: 1 / -1; }        /* Span full width */
.sidebar { grid-row: 2 / 4; }            /* Span 2 rows */
.main    { grid-column: 2 / 3; }
.footer  { grid-column: 1 / -1; }
```

> **Code Explanation:**
> - `grid-column: 1 / -1` — starts at column line 1, ends at the last line (`-1`) — spans full width
> - `grid-row: 2 / 4` — starts at row line 2, ends at row line 4 — spans 2 rows
> - Grid lines are numbered starting from 1 (left/top edge) — a 3-column grid has lines 1, 2, 3, 4
> - `-1` always means the last line — useful so you don't have to count columns

### `grid-template-areas` — Visual Layout with Named Areas

Instead of using line numbers, you can create a visual map of your layout using names:

```css
.page-layout {
    display: grid;
    grid-template-columns: 200px 1fr 200px;   /* Three columns */
    grid-template-rows: auto 1fr auto;         /* Three rows */
    grid-template-areas:
        "header  header  header"     /* Row 1: header spans all 3 columns */
        "sidebar content aside"      /* Row 2: three areas side by side */
        "footer  footer  footer";    /* Row 3: footer spans all 3 columns */
    min-height: 100vh;
    gap: 10px;
}

/* Assign elements to named areas */
.header  { grid-area: header;  background: #1565C0; color: white; padding: 20px; }
.sidebar { grid-area: sidebar; background: #f5f5f5; padding: 15px; }
.content { grid-area: content; background: white; padding: 20px; }
.aside   { grid-area: aside;   background: #f5f5f5; padding: 15px; }
.footer  { grid-area: footer;  background: #333; color: white; padding: 15px; }
```

> **Code Explanation:**
> - `grid-template-areas` lets you "draw" your layout using quoted strings — each string is one row, each word is a cell
> - `"header header header"` means the header occupies all three columns in row 1
> - `"sidebar content aside"` puts three different areas side by side in row 2
> - `grid-area: header` assigns an element to the named area — the browser places it automatically
> - This is much more readable than `grid-column: 1 / -1` — you can literally see the layout in your CSS!

> **Analogy:** Think of `grid-template-areas` like drawing a floor plan for a house in Mandsaur. You sketch "bedroom bedroom" on one row and "kitchen hall" on another — then each room knows exactly where it goes.

**Use `.` for Empty Cells:**

```css
.layout-with-gap {
    grid-template-areas:
        "header header header"
        "sidebar content ."          /* The dot creates an empty cell */
        "footer footer footer";
}
```

> **Code Explanation:**
> - A `.` (dot) in `grid-template-areas` creates an empty cell — no element is placed there
> - This is useful when you want a gap in your layout without using an empty `<div>`

---

## 3. Flexbox vs Grid

| Feature | Flexbox | Grid |
|---------|---------|------|
| **Dimension** | 1D (row OR column) | 2D (rows AND columns) |
| **Best for** | Navigation, card rows, alignment | Page layouts, dashboards |
| **Item sizing** | Based on content/flex | Based on track definition |
| **Use together?** | ✅ Yes — Grid for page, Flexbox for components |

### Responsive Layout Patterns

#### Pattern 1: Holy Grail Layout (Header + Sidebar + Content + Footer)

The "Holy Grail" is a classic web layout that was historically difficult to build. With Grid, it's simple:

```css
/* Holy Grail Layout using CSS Grid */
.holy-grail {
    display: grid;
    grid-template-areas:
        "header header header"       /* Full-width header */
        "nav    main   aside"        /* Three-column middle section */
        "footer footer footer";      /* Full-width footer */
    grid-template-columns: 200px 1fr 200px;  /* Fixed sidebars, flexible content */
    grid-template-rows: auto 1fr auto;       /* Header/footer auto, content fills remaining space */
    min-height: 100vh;                       /* Full viewport height */
}

.holy-grail > header { grid-area: header; }
.holy-grail > nav    { grid-area: nav; }
.holy-grail > main   { grid-area: main; }
.holy-grail > aside  { grid-area: aside; }
.holy-grail > footer { grid-area: footer; }

/* Responsive: Stack on mobile */
@media (max-width: 768px) {
    .holy-grail {
        grid-template-areas:
            "header"    /* Stack everything in one column */
            "nav"
            "main"
            "aside"
            "footer";
        grid-template-columns: 1fr;   /* Single column */
    }
}
```

> **Code Explanation:**
> - Desktop: Three columns (200px sidebar, flexible center, 200px aside) with header and footer spanning full width
> - `min-height: 100vh` ensures the layout fills the entire screen height
> - `grid-template-rows: auto 1fr auto` — header and footer take only the space they need, the middle section takes all remaining space
> - `@media (max-width: 768px)` activates on tablets/phones — layout switches to a single column stack
> - On mobile, all areas stack vertically with `grid-template-columns: 1fr` (one full-width column)

#### Pattern 2: Sticky Footer (Footer Always at Bottom)

A common problem: when page content is short, the footer floats in the middle of the screen. Flexbox fixes this:

```css
/* Sticky footer using Flexbox */
body {
    display: flex;
    flex-direction: column;    /* Stack children vertically */
    min-height: 100vh;         /* At least full viewport height */
    margin: 0;
}

main {
    flex: 1;                   /* Main content grows to fill available space */
}

footer {
    background: #333;
    color: white;
    padding: 20px;
    text-align: center;
}
/* Footer always stays at the bottom, whether content is long or short */
```

> **Code Explanation:**
> - `body { display: flex; flex-direction: column; }` turns the body into a vertical flex container
> - `min-height: 100vh` ensures the body is at least as tall as the screen
> - `main { flex: 1; }` makes the main content area expand to fill all remaining space
> - The footer naturally stays at the bottom because it comes after the expanded main section
> - If the content is taller than the viewport, the footer simply scrolls below — no overlap

---

## Practical Session: Complete Layout

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Flexbox & Grid Layout</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: 'Segoe UI', sans-serif; }

        /* ========= FLEXBOX NAVBAR ========= */
        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #1565C0;
            padding: 15px 30px;
        }
        .logo {
            font-size: 1.4em;
            font-weight: bold;
            color: white;
        }
        .nav-links {
            display: flex;
            gap: 25px;
            list-style: none;
        }
        .nav-links a {
            color: white;
            text-decoration: none;
            font-size: 15px;
        }
        .nav-links a:hover {
            text-decoration: underline;
        }

        /* ========= GRID PAGE LAYOUT ========= */
        .page {
            display: grid;
            grid-template-columns: 250px 1fr;
            grid-template-rows: auto 1fr auto;
            min-height: calc(100vh - 55px);
        }

        .hero {
            grid-column: 1 / -1;
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            text-align: center;
            padding: 50px 20px;
        }
        .hero h1 { font-size: 2.5em; }
        .hero p { margin-top: 10px; opacity: 0.9; }

        .sidebar {
            background: #f5f5f5;
            padding: 20px;
            border-right: 1px solid #ddd;
        }
        .sidebar h3 {
            color: #1565C0;
            margin-bottom: 10px;
        }
        .sidebar ul { list-style: none; }
        .sidebar li {
            padding: 8px 0;
            border-bottom: 1px solid #eee;
        }
        .sidebar a { color: #333; text-decoration: none; }
        .sidebar a:hover { color: #1565C0; }

        .main-content {
            padding: 30px;
        }

        /* ========= GRID CARD LAYOUT ========= */
        .card-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 20px;
            margin-top: 20px;
        }
        .card {
            background: white;
            border: 1px solid #e0e0e0;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 2px 8px rgba(0,0,0,0.08);
        }
        .card-img {
            height: 120px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-size: 2em;
        }
        .card-body { padding: 15px; }
        .card-body h4 { color: #333; margin-bottom: 5px; }
        .card-body p { color: #777; font-size: 14px; }

        footer {
            grid-column: 1 / -1;
            background: #333;
            color: white;
            text-align: center;
            padding: 15px;
        }
    </style>
</head>
<body>

    <!-- FLEXBOX NAV -->
    <nav>
        <div class="logo">MU — BCA</div>
        <ul class="nav-links">
            <li><a href="#">Home</a></li>
            <li><a href="#">Courses</a></li>
            <li><a href="#">Faculty</a></li>
            <li><a href="#">Contact</a></li>
        </ul>
    </nav>

    <!-- GRID PAGE LAYOUT -->
    <div class="page">
        <div class="hero">
            <h1>Flexbox & Grid Layout</h1>
            <p>Building modern layouts with CSS</p>
        </div>

        <aside class="sidebar">
            <h3>Quick Links</h3>
            <ul>
                <li><a href="#">HTML Basics</a></li>
                <li><a href="#">CSS Fundamentals</a></li>
                <li><a href="#">JavaScript</a></li>
                <li><a href="#">Bootstrap</a></li>
                <li><a href="#">Projects</a></li>
            </ul>
        </aside>

        <main class="main-content">
            <h2>Our Courses</h2>
            <p>Explore the technology courses offered at BCA Department.</p>

            <div class="card-grid">
                <div class="card">
                    <div class="card-img" style="background: linear-gradient(135deg, #667eea, #764ba2);">🌐</div>
                    <div class="card-body">
                        <h4>Web Technology</h4>
                        <p>HTML, CSS, JS, Bootstrap</p>
                    </div>
                </div>
                <div class="card">
                    <div class="card-img" style="background: linear-gradient(135deg, #11998e, #38ef7d);">📊</div>
                    <div class="card-body">
                        <h4>Data Structures</h4>
                        <p>Arrays, Lists, Trees, Graphs</p>
                    </div>
                </div>
                <div class="card">
                    <div class="card-img" style="background: linear-gradient(135deg, #ee0979, #ff6a00);">🧮</div>
                    <div class="card-body">
                        <h4>Mathematics</h4>
                        <p>Discrete Math, Probability</p>
                    </div>
                </div>
            </div>
        </main>

        <footer>
            <p>&copy; 2026 Mandsaur University. All Rights Reserved.</p>
        </footer>
    </div>

</body>
</html>
```

> **Code Explanation:**
> - **Flexbox Navbar:** `nav` uses `display: flex` with `space-between` to push the logo left and links right; links themselves are also in a flex container with `gap: 25px`
> - **Grid Page Layout:** `.page` uses CSS Grid with a 250px sidebar and flexible main area; `min-height: calc(100vh - 55px)` fills the remaining screen after the navbar
> - **Hero Section:** `grid-column: 1 / -1` makes the hero span both sidebar and main content columns; gradient background creates visual appeal
> - **Sidebar:** Fixed 250px width (from the grid column), border-right separates it from content; links styled without underlines with blue hover color
> - **Card Grid:** `repeat(auto-fit, minmax(220px, 1fr))` creates responsive card columns — no media query needed, cards automatically reflow
> - **Card Design:** `overflow: hidden` ensures the colored header with `border-radius` doesn't spill outside the card's rounded corners
> - **Footer:** `grid-column: 1 / -1` spans full width at the bottom; dark background with white text
> - This layout combines **Grid for the page structure** and **Flexbox for component-level alignment** — this is the recommended approach for modern websites

---

## Summary

| Concept | Key Properties |
|---------|---------------|
| Flex container | `display: flex`, `justify-content`, `align-items` |
| Flex items | `flex-grow`, `flex-shrink`, `flex-basis`, `flex: 1` |
| Grid container | `display: grid`, `grid-template-columns/rows` |
| Grid items | `grid-column`, `grid-row` |
| Responsive grid | `repeat(auto-fit, minmax(250px, 1fr))` |
| Gap | `gap: 20px` (works in both Flex and Grid) |

---

*Day 24 of 55 | Unit 4 — CSS | Web Technology (25BCA060)*
