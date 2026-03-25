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

This turns the container into a **flex container** and its direct children into **flex items**.

### Flex Direction

```css
.row        { flex-direction: row; }           /* → (default) */
.row-rev    { flex-direction: row-reverse; }    /* ← */
.col        { flex-direction: column; }         /* ↓ */
.col-rev    { flex-direction: column-reverse; } /* ↑ */
```

### Justify Content (Main Axis)

```css
.start   { justify-content: flex-start; }    /* |■ ■ ■      | */
.end     { justify-content: flex-end; }      /* |      ■ ■ ■| */
.center  { justify-content: center; }        /* |   ■ ■ ■   | */
.between { justify-content: space-between; } /* |■    ■    ■| */
.around  { justify-content: space-around; }  /* | ■   ■   ■ | */
.evenly  { justify-content: space-evenly; }  /* |  ■  ■  ■  | */
```

### Align Items (Cross Axis)

```css
.top     { align-items: flex-start; }
.bottom  { align-items: flex-end; }
.center  { align-items: center; }
.stretch { align-items: stretch; }    /* Default — fill height */
```

### Flex Wrap

```css
.container {
    display: flex;
    flex-wrap: wrap;     /* Items wrap to next line */
    gap: 15px;           /* Space between items */
}
```

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

### Placing Items

```css
.header  { grid-column: 1 / -1; }        /* Span full width */
.sidebar { grid-row: 2 / 4; }            /* Span 2 rows */
.main    { grid-column: 2 / 3; }
.footer  { grid-column: 1 / -1; }
```

---

## 3. Flexbox vs Grid

| Feature | Flexbox | Grid |
|---------|---------|------|
| **Dimension** | 1D (row OR column) | 2D (rows AND columns) |
| **Best for** | Navigation, card rows, alignment | Page layouts, dashboards |
| **Item sizing** | Based on content/flex | Based on track definition |
| **Use together?** | ✅ Yes — Grid for page, Flexbox for components |

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
