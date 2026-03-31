# Day 21 — CSS Colors, Backgrounds & Borders

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 4 — CSS
🧪 **Lab Experiment:** 11

---

## Learning Objectives

By the end of this session, students will be able to:
- Use all CSS color formats (named, hex, rgb, rgba, hsl)
- Apply background colors, images, and gradients
- Style borders with different styles, widths, and radius
- Create CSS-only visual effects using backgrounds and borders

---

## 1. CSS Color Formats

| Format | Syntax | Example |
|--------|--------|---------|
| Named | `color: red;` | 147 named colors |
| Hex | `color: #FF0000;` | 6-digit hex |
| Hex shorthand | `color: #F00;` | 3-digit hex |
| RGB | `color: rgb(255, 0, 0);` | Red, Green, Blue (0–255) |
| RGBA | `color: rgba(255, 0, 0, 0.5);` | RGB + Alpha (opacity 0–1) |
| HSL | `color: hsl(0, 100%, 50%);` | Hue (0–360), Saturation, Lightness |

> **Analogy (HSL):** Think of a **color wheel** in art class. **Hue** is the position on the wheel (0 = red, 120 = green, 240 = blue). **Saturation** is how vivid the color is (0% = gray, 100% = pure). **Lightness** is brightness (0% = black, 50% = normal, 100% = white).

### Color Comparison

```css
.red-named { color: red; }
.red-hex   { color: #FF0000; }
.red-rgb   { color: rgb(255, 0, 0); }
.red-hsl   { color: hsl(0, 100%, 50%); }
/* All four look identical */

.semi-transparent { color: rgba(255, 0, 0, 0.5); }
```

> **Code Explanation:**
> - All four `.red-*` classes produce the **exact same red color** — just written in different formats
> - `red` (named) is easiest to read but limited to 147 predefined color names
> - `#FF0000` (hex) is the most commonly used format — FF=red, 00=green, 00=blue
> - `rgb(255, 0, 0)` is easy to understand — maximum red (255), no green, no blue
> - `hsl(0, 100%, 50%)` uses the color wheel — 0° = red, full saturation, medium lightness
> - `rgba(255, 0, 0, 0.5)` adds transparency — `0.5` means 50% see-through

### Color Accessibility — Making Text Readable for Everyone

Not all color combinations are easy to read. The **WCAG (Web Content Accessibility Guidelines)** define minimum contrast ratios to ensure text is readable:

| Level | Contrast Ratio | Applies To | Example |
|-------|---------------|-----------|---------|
| **AA (Minimum)** | **4.5:1** | Normal text (below 18px) | Dark text on light background ✅ |
| **AA (Large)** | **3:1** | Large text (18px+ bold, or 24px+) | Heading text |
| **AAA (Enhanced)** | **7:1** | Normal text (strictest standard) | For maximum readability |

**Good vs Bad Color Combinations:**

```css
/* ✅ GOOD contrast — easy to read */
.good-1 { color: #1a1a1a; background: #ffffff; }  /* Black on white — 16:1 ratio */
.good-2 { color: #ffffff; background: #1565C0; }  /* White on blue — 7.2:1 ratio */
.good-3 { color: #1a1a1a; background: #FFF9C4; }  /* Black on light yellow — 15:1 ratio */

/* ❌ BAD contrast — hard to read */
.bad-1 { color: #aaaaaa; background: #ffffff; }   /* Light gray on white — 2.3:1 ratio */
.bad-2 { color: #ffff00; background: #ffffff; }   /* Yellow on white — 1.1:1 ratio */
.bad-3 { color: #ff6666; background: #ff9999; }   /* Light red on lighter red — 1.5:1 ratio */
```

> **Code Explanation:**
> - Good contrast means dark text on light background (or vice versa) with a ratio of at least 4.5:1
> - Light gray (`#aaaaaa`) on white (`#ffffff`) has only 2.3:1 contrast — many users (especially elderly) will struggle to read it
> - Yellow on white is nearly invisible (1.1:1) — never use this combination
> - **Tip:** Use a free tool like [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) to test your color combinations

> **Real-world example:** The Indian government's accessibility guidelines (GIGW — Guidelines for Indian Government Websites) also require WCAG AA compliance. If you're building a website for a university, bank, or government office, contrast matters!

---

## 2. Background Properties

### Background Color

```css
body { background-color: #f4f4f4; }
.card { background-color: rgba(21, 101, 192, 0.1); }
```

> **Code Explanation:**
> - `background-color: #f4f4f4` gives the body a very light gray — not pure white, which is easier on the eyes
> - `rgba(21, 101, 192, 0.1)` is a blue color at only 10% opacity — creates a very subtle blue tint, perfect for cards

### Background Image

```css
.hero {
    background-image: url('campus.jpg');
    background-size: cover;          /* Fill entire element */
    background-position: center;     /* Center the image */
    background-repeat: no-repeat;    /* Don't tile */
    background-attachment: fixed;    /* Parallax effect */
    height: 400px;
}
```

> **Code Explanation:**
> - `background-image: url('campus.jpg')` loads an image as the background
> - `background-size: cover` scales the image to completely fill the element (may crop edges)
> - `background-position: center` centers the image so the most important part stays visible
> - `background-repeat: no-repeat` prevents the image from repeating/tiling
> - `background-attachment: fixed` creates a parallax effect — the image stays still while content scrolls over it
> - `height: 400px` gives the hero section a fixed height

| Property | Values |
|----------|--------|
| `background-size` | `cover`, `contain`, `100px 200px` |
| `background-position` | `center`, `top left`, `50% 50%` |
| `background-repeat` | `no-repeat`, `repeat`, `repeat-x`, `repeat-y` |
| `background-attachment` | `scroll` (default), `fixed` (parallax) |

### Background Shorthand

```css
.hero {
    background: url('campus.jpg') center/cover no-repeat fixed;
}
```

> **Code Explanation:**
> - This single line replaces 5 separate background properties
> - Format: `url('image')` `position`/`size` `repeat` `attachment`
> - The `/` separates position from size (like `center/cover`)
> - Shorthand is faster to write but can be harder to read for beginners

---

## 3. CSS Gradients

### Linear Gradient

```css
.gradient-1 {
    background: linear-gradient(to right, #667eea, #764ba2);
}
.gradient-2 {
    background: linear-gradient(135deg, #11998e, #38ef7d);
}
.gradient-3 {
    background: linear-gradient(to bottom, #FF9933, #FFFFFF, #138808); /* Indian flag */
}
```

> **Code Explanation:**
> - `linear-gradient(to right, #667eea, #764ba2)` creates a gradient that goes from left to right — starts purple-blue, ends purple
> - `linear-gradient(135deg, #11998e, #38ef7d)` creates a diagonal gradient at 135 degrees — top-left to bottom-right
> - `linear-gradient(to bottom, #FF9933, #FFFFFF, #138808)` uses three colors to create the Indian tricolor (saffron → white → green)

### Gradient Direction — How Degrees Work

The `linear-gradient()` direction can be specified using keywords or degrees:

```
                    0deg (to top)
                       ↑
                       |
   315deg (top-left)   |   45deg (top-right)
            ↖          |          ↗
              \        |        /
                \      |      /
  270deg (left) ←——— CENTER ———→ 90deg (to right)
                /      |      \
              /        |        \
            ↙          |          ↘
   225deg (bottom-left)|   135deg (bottom-right)
                       |
                       ↓
                  180deg (to bottom)
```

| Degree | Keyword | Direction |
|--------|---------|-----------|
| `0deg` | `to top` | Bottom → Top ↑ |
| `90deg` | `to right` | Left → Right → |
| `180deg` | `to bottom` | Top → Bottom ↓ (default) |
| `270deg` | `to left` | Right → Left ← |
| `45deg` | `to top right` | Bottom-left → Top-right ↗ |
| `135deg` | `to bottom right` | Top-left → Bottom-right ↘ |

```css
/* Common gradient directions */
.top-to-bottom { background: linear-gradient(180deg, #FF9933, #138808); }  /* Default direction */
.left-to-right { background: linear-gradient(90deg, #FF9933, #138808); }   /* Horizontal */
.diagonal      { background: linear-gradient(45deg, #FF9933, #138808); }   /* Corner to corner */
.custom-angle  { background: linear-gradient(200deg, #1565C0, #E91E63); }  /* Any angle you want */
```

> **Code Explanation:**
> - `180deg` goes from top to bottom (this is the default if you don't specify a direction)
> - `90deg` goes from left to right — like reading a line of text
> - `45deg` goes diagonally from bottom-left to top-right
> - You can use any degree value from 0 to 360 for fine control over the gradient angle

### Radial Gradient

```css
.radial {
    background: radial-gradient(circle, #667eea, #764ba2);
}
```

> **Code Explanation:**
> - `radial-gradient(circle, ...)` creates a gradient that radiates outward from the center in a circular shape
> - The first color (`#667eea`) appears at the center, and the second (`#764ba2`) at the edges
> - You can also use `ellipse` (default) instead of `circle` for an oval gradient

---

## 4. Border Properties

### Border Syntax

```css
.box {
    border: 2px solid #333;        /* Shorthand: width style color */
}

/* Individual sides */
.box {
    border-top: 3px solid #1565C0;
    border-right: 1px dashed #ccc;
    border-bottom: 3px solid #1565C0;
    border-left: 1px dashed #ccc;
}
```

> **Code Explanation:**
> - `border: 2px solid #333` is shorthand — sets width, style, and color in one line
> - You can style each side independently — useful for creating visual accents (like a colored left border on articles)
> - `border-top` and `border-bottom` are solid blue, while `border-right` and `border-left` are dashed gray — mixing styles creates unique designs

### Border Styles

| Style | Appearance |
|-------|-----------|
| `solid` | ─────── |
| `dashed` | - - - - |
| `dotted` | · · · · |
| `double` | ══════ |
| `groove` | 3D groove |
| `ridge` | 3D ridge |
| `inset` | 3D inset |
| `outset` | 3D outset |
| `none` | No border |

### Border Radius (Rounded Corners)

```css
.rounded    { border-radius: 10px; }          /* All corners */
.pill       { border-radius: 50px; }          /* Pill shape */
.circle     { border-radius: 50%; }           /* Perfect circle */
.custom     { border-radius: 10px 30px 10px 30px; } /* TL TR BR BL */
```

> **Code Explanation:**
> - `border-radius: 10px` rounds all four corners equally
> - `border-radius: 50px` on a wide element creates a **pill shape** (used for buttons)
> - `border-radius: 50%` creates a **perfect circle** (element must be equal width and height)
> - `border-radius: 10px 30px 10px 30px` sets each corner individually: Top-Left, Top-Right, Bottom-Right, Bottom-Left (clockwise from top-left)

---

## 5. Box Shadow

```css
.card {
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    /* x-offset  y-offset  blur  color */
}

.card-hover {
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);
}

/* Inner shadow */
.inset {
    box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.2);
}
```

> **Code Explanation:**
> - `.card` has a subtle shadow: `0` horizontal offset, `4px` down, `6px` blur — creates a gentle "floating" effect
> - `.card-hover` has a bigger shadow (`8px` down, `25px` blur) — typically used on `:hover` to make cards "lift up"
> - `inset` keyword puts the shadow **inside** the element instead of outside — looks like the element is pressed inward
> - `rgba(0, 0, 0, 0.1)` means black at 10% opacity — always use semi-transparent shadows for natural-looking depth

### Understanding Box Shadow — The Spread Radius

The full `box-shadow` syntax actually has **5 values** (not just 4):

```css
box-shadow: x-offset  y-offset  blur-radius  spread-radius  color;

/* Without spread radius */
.shadow-no-spread {
    box-shadow: 5px 5px 10px rgba(0, 0, 0, 0.3);
    /* Shadow is same size as element, just blurry */
}

/* With positive spread — shadow grows LARGER */
.shadow-spread {
    box-shadow: 5px 5px 10px 5px rgba(0, 0, 0, 0.3);
    /* Shadow extends 5px beyond element on all sides */
}

/* With negative spread — shadow shrinks SMALLER */
.shadow-shrink {
    box-shadow: 0 10px 20px -5px rgba(0, 0, 0, 0.3);
    /* Shadow is 5px smaller than element — creates a "floating" effect */
}

/* Popular card shadow — used on most modern websites */
.card-shadow {
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1),    /* Main shadow */
                0 2px 4px -2px rgba(0, 0, 0, 0.1);     /* Secondary subtle shadow */
}
```

> **Code Explanation:**
> - **x-offset**: Horizontal shadow position. Positive = right, negative = left
> - **y-offset**: Vertical shadow position. Positive = down, negative = up
> - **blur-radius**: How blurry the shadow is. `0` = sharp edge, `20px` = very soft
> - **spread-radius**: How much the shadow grows or shrinks. Positive = bigger, negative = smaller than the element
> - **Two shadows** can be combined with a comma — the card uses a main shadow and a subtle secondary shadow for depth
> - The "floating card" effect (negative spread) is extremely popular on modern websites like Google, Flipkart, and Zomato

| Value | Effect | Common Use |
|-------|--------|-----------|
| Positive spread (`5px`) | Shadow is larger than element | Glowing effect |
| Zero spread (`0`) | Shadow matches element size | Standard shadow |
| Negative spread (`-5px`) | Shadow is smaller than element | Floating card effect |

---

## Practical Session

### 🧪 Lab Experiment 11: Colors, Backgrounds & Borders

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS Colors, Backgrounds & Borders</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        
        body {
            font-family: 'Segoe UI', sans-serif;
            background: #f0f0f0;
        }

        /* Hero section with gradient */
        .hero {
            background: linear-gradient(135deg, #1565C0 0%, #0D47A1 50%, #002171 100%);
            color: white;
            text-align: center;
            padding: 60px 20px;
        }
        .hero h1 {
            font-size: 2.5em;
            text-shadow: 2px 2px 8px rgba(0,0,0,0.3);
        }
        .hero p {
            margin-top: 10px;
            font-size: 1.2em;
            opacity: 0.9;
        }

        /* Card container */
        .cards {
            max-width: 900px;
            margin: 30px auto;
            padding: 0 20px;
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
            justify-content: center;
        }

        /* Card styles */
        .card {
            width: 260px;
            background: white;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
        }
        .card-header {
            padding: 20px;
            color: white;
            text-align: center;
        }
        .card-body {
            padding: 20px;
        }
        .card-body p { color: #555; font-size: 14px; }

        /* Different colored cards */
        .card:nth-child(1) .card-header { background: linear-gradient(135deg, #667eea, #764ba2); }
        .card:nth-child(2) .card-header { background: linear-gradient(135deg, #11998e, #38ef7d); }
        .card:nth-child(3) .card-header { background: linear-gradient(135deg, #ee0979, #ff6a00); }

        /* Border showcase */
        .border-demo {
            max-width: 900px;
            margin: 30px auto;
            padding: 20px;
        }
        .border-box {
            display: inline-block;
            width: 120px;
            height: 80px;
            margin: 10px;
            padding: 10px;
            text-align: center;
            line-height: 60px;
            font-size: 12px;
            background: white;
        }
        .b-solid  { border: 3px solid #1565C0; }
        .b-dashed { border: 3px dashed #E91E63; }
        .b-dotted { border: 3px dotted #4CAF50; }
        .b-double { border: 4px double #FF9800; }
        .b-groove { border: 4px groove #9C27B0; }
        .b-ridge  { border: 4px ridge #009688; }

        /* Rounded corners showcase */
        .radius-demo {
            max-width: 900px;
            margin: 30px auto;
            padding: 20px;
            text-align: center;
        }
        .shape {
            display: inline-block;
            width: 100px;
            height: 100px;
            margin: 10px;
            line-height: 100px;
            text-align: center;
            color: white;
            font-size: 12px;
        }
        .square   { background: #1565C0; border-radius: 0; }
        .rounded  { background: #E91E63; border-radius: 15px; }
        .more-rounded { background: #4CAF50; border-radius: 30px; }
        .circle   { background: #FF9800; border-radius: 50%; }

        /* Footer */
        footer {
            background: #333;
            color: white;
            text-align: center;
            padding: 15px;
            margin-top: 30px;
        }
    </style>
</head>
<body>

    <div class="hero">
        <h1>CSS Visual Styling</h1>
        <p>Colors, Backgrounds, Gradients, Borders & Shadows</p>
    </div>

    <div class="cards">
        <div class="card">
            <div class="card-header"><h3>HTML</h3></div>
            <div class="card-body"><p>Structure and content of web pages using semantic markup.</p></div>
        </div>
        <div class="card">
            <div class="card-header"><h3>CSS</h3></div>
            <div class="card-body"><p>Styling and layout — colors, fonts, spacing, and animations.</p></div>
        </div>
        <div class="card">
            <div class="card-header"><h3>JavaScript</h3></div>
            <div class="card-body"><p>Interactivity and dynamic behavior on the client side.</p></div>
        </div>
    </div>

    <div class="border-demo">
        <h2 style="text-align:center; margin-bottom:15px;">Border Styles</h2>
        <div style="text-align:center;">
            <div class="border-box b-solid">Solid</div>
            <div class="border-box b-dashed">Dashed</div>
            <div class="border-box b-dotted">Dotted</div>
            <div class="border-box b-double">Double</div>
            <div class="border-box b-groove">Groove</div>
            <div class="border-box b-ridge">Ridge</div>
        </div>
    </div>

    <div class="radius-demo">
        <h2 style="margin-bottom:15px;">Border Radius</h2>
        <div class="shape square">0px</div>
        <div class="shape rounded">15px</div>
        <div class="shape more-rounded">30px</div>
        <div class="shape circle">50%</div>
    </div>

    <footer>
        <p>&copy; 2026 Mandsaur University — BCA Semester II</p>
    </footer>

</body>
</html>
```

> **Code Explanation:**
> - **Universal Reset:** `* { box-sizing: border-box; margin: 0; padding: 0; }` removes all default spacing for consistent layout
> - **Hero Section:** Uses a 3-stop gradient (`#1565C0` → `#0D47A1` → `#002171`) for a rich blue header with white centered text
> - **Cards Container:** `display: flex; flex-wrap: wrap; gap: 20px;` creates a responsive card layout that wraps to new lines
> - **Card Design:** White background, `border-radius: 12px` for rounded corners, and `box-shadow` for depth — a common modern card pattern
> - **nth-child Gradients:** Each card gets a different gradient using `:nth-child(1)`, `:nth-child(2)`, `:nth-child(3)` — avoids adding extra classes
> - **Border Showcase:** Six boxes demonstrate different border styles (solid, dashed, dotted, double, groove, ridge) — each in a different color for visual distinction
> - **Radius Demo:** Four shapes show increasing `border-radius` — from 0px (square) to 50% (perfect circle) — demonstrating how the property works progressively
> - **Footer:** Dark background (`#333`) with white centered text — a standard footer pattern seen on most websites

---

## Summary

| Property | Purpose | Example |
|----------|---------|---------|
| `color` | Text color | `#1565C0`, `rgba(0,0,0,0.8)` |
| `background-color` | Element background | `#f4f4f4` |
| `background-image` | Background image/gradient | `url()`, `linear-gradient()` |
| `border` | Border shorthand | `2px solid #333` |
| `border-radius` | Rounded corners | `10px`, `50%` |
| `box-shadow` | Drop shadow | `0 4px 6px rgba(0,0,0,0.1)` |

---

*Day 21 of 55 | Unit 4 — CSS | Web Technology (25BCA060)*
