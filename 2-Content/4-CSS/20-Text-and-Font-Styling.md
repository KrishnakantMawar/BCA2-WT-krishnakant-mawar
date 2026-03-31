# Day 20 — CSS Text & Font Styling

📖 **Type:** Theory Session
🕐 **Duration:** 2 Hours
📚 **Unit:** 4 — CSS

---

## Learning Objectives

By the end of this session, students will be able to:
- Style text using various CSS text properties
- Use web-safe fonts and Google Fonts
- Apply font shorthand property
- Understand CSS units (px, em, rem, %, vw/vh)

---

## 1. CSS Font Properties

> **Analogy:** Choosing fonts is like choosing **handwriting on a poster**. A wedding invitation uses elegant script. A tech startup uses clean sans-serif. The same text feels completely different just by changing the font.

### Font Family

```css
/* Font stack: browser tries first font, falls back to next */
body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

h1 {
    font-family: Georgia, 'Times New Roman', Times, serif;
}

code {
    font-family: 'Courier New', Courier, monospace;
}
```

> **Code Explanation:**
> - `body` uses 'Segoe UI' as first choice — a clean Windows font. If not available, it tries Tahoma, Geneva, Verdana, and finally any `sans-serif` font
> - `h1` uses Georgia (a serif font) for headings — serif fonts feel traditional and authoritative, like a newspaper
> - `code` uses 'Courier New' (monospace) — every character takes equal width, making code easier to read and align
> - Each declaration has a **font stack** — multiple fonts separated by commas as fallbacks

### Web-Safe Fonts

These fonts are available on almost every computer:

| Serif | Sans-Serif | Monospace |
|-------|-----------|-----------|
| Times New Roman | Arial | Courier New |
| Georgia | Verdana | Lucida Console |
| Garamond | Tahoma | Consolas |

### Why Font Stacks Matter (Font Fallback System)

When you write `font-family: 'Poppins', Arial, sans-serif;`, you're creating a **font stack** — a priority list of fonts.

```
Browser checks: Do I have 'Poppins'?
   ├── YES → Use Poppins ✅
   └── NO  → Do I have Arial?
                ├── YES → Use Arial ✅
                └── NO  → Use any sans-serif font on this device ✅
```

> **Analogy:** It's like ordering food at a restaurant in Mandsaur. Your first choice is Paneer Tikka. If it's not available, you ask for Paneer Butter Masala. If that's also not available, you say "any paneer dish." The font stack works the same way — first choice, backup, and generic fallback.

**Important Rules for Font Stacks:**

| Rule | Explanation | Example |
|------|------------|---------|
| Always end with generic family | Every system has at least one `serif`, `sans-serif`, or `monospace` font | `font-family: 'Poppins', sans-serif;` |
| Multi-word names need quotes | Font names with spaces must be in quotes | `'Times New Roman'` not `Times New Roman` |
| Put preferred font first | Browser uses the first available font | `'Poppins', Arial, sans-serif` |

### Google Fonts (Free Custom Fonts)

```html
<head>
    <!-- Load Poppins font from Google in 4 weights: 300, 400, 600, 700 -->
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&display=swap" rel="stylesheet">
    <style>
        /* Use Poppins as primary font, sans-serif as fallback */
        body { font-family: 'Poppins', sans-serif; }
    </style>
</head>
```

> **Code Explanation:**
> - The `<link>` tag loads the **Poppins** font from Google's servers in weights 300, 400, 600, and 700
> - `display=swap` tells the browser: "Show text in a fallback font immediately, then swap to Poppins when it loads"
> - `font-family: 'Poppins', sans-serif;` uses Poppins as first choice with sans-serif as fallback

### Font Loading Behavior — FOUT and FOIT

When using custom fonts (like Google Fonts), the browser must download the font file. During this download, two things can happen:

| Behavior | Full Name | What Happens | User Experience |
|----------|-----------|-------------|----------------|
| **FOUT** | Flash of Unstyled Text | Text shows in fallback font first, then switches to custom font | Text is always visible ✅ but "flashes" when font loads |
| **FOIT** | Flash of Invisible Text | Text is hidden until custom font loads | Page looks "blank" briefly ❌ |

**The `font-display` Property (controls this behavior):**

```css
@font-face {
    font-family: 'MyFont';
    src: url('myfont.woff2') format('woff2');  /* Custom font file location */
    font-display: swap; /* Show fallback immediately, swap when ready */
}
```

> **Code Explanation:**
> - `@font-face` lets you define a custom font that isn't on the user's computer
> - `font-display: swap` prevents invisible text — the browser shows a fallback font, then swaps when the custom font downloads
> - Other values: `auto` (browser decides), `block` (hide text briefly), `fallback` (short block then swap), `optional` (use only if already cached)

| `font-display` Value | Behavior | Best For |
|----------------------|----------|----------|
| `swap` | Show fallback immediately, swap when ready | Most websites ✅ |
| `block` | Hide text for up to 3 seconds | Icon fonts |
| `fallback` | Very short hide, then fallback | Balanced approach |
| `optional` | Only use if already cached | Non-essential decorative fonts |

> **Tip:** When you use Google Fonts with `&display=swap` in the URL, it automatically adds `font-display: swap` for you. This is why the Google Fonts link includes `display=swap`.

---

## 2. Font Size & Weight

### Size Units

| Unit | Meaning | Example |
|------|---------|---------|
| `px` | Absolute pixels | `font-size: 16px;` |
| `em` | Relative to parent | `font-size: 1.5em;` (1.5× parent) |
| `rem` | Relative to root (`<html>`) | `font-size: 1.2rem;` |
| `%` | Percentage of parent | `font-size: 120%;` |
| `vw` | % of viewport width | `font-size: 3vw;` |

> **Rule of thumb:** Use `rem` for font sizes (consistent, accessible) and `px` for borders/shadows.

### Em vs Rem — The Compounding Problem

The key difference: `em` is relative to the **parent element**, while `rem` is always relative to the **root (`<html>`) element**.

```html
<html> <!-- Default: 16px -->
<body>
    <div style="font-size: 20px;">
        <!-- Parent is 20px -->
        <p style="font-size: 1.5em;">This is 30px (1.5 × 20px parent)</p>
        <div style="font-size: 1.5em;">
            <!-- Now parent is 30px (1.5 × 20px) -->
            <p style="font-size: 1.5em;">This is 45px! (1.5 × 30px parent)</p>
            <!-- em COMPOUNDS — each nesting multiplies -->
        </div>
    </div>
</body>
</html>
```

> **Code Explanation:**
> - The root `<html>` has a default font size of 16px
> - The outer `<div>` sets its font size to 20px
> - The first `<p>` uses `1.5em` = 1.5 × 20px (parent) = **30px**
> - The inner `<div>` also uses `1.5em` = 1.5 × 20px = **30px** — this becomes the new parent size
> - The nested `<p>` uses `1.5em` = 1.5 × 30px = **45px** — the size keeps growing!
> - This "compounding" effect makes `em` unpredictable in deeply nested HTML

**With `rem` — No Compounding:**

```html
<html style="font-size: 16px;">
<body>
    <div style="font-size: 20px;">
        <p style="font-size: 1.5rem;">This is 24px (1.5 × 16px root)</p>
        <div style="font-size: 1.5rem;">
            <p style="font-size: 1.5rem;">This is ALSO 24px (1.5 × 16px root)</p>
            <!-- rem always looks at root, never parent -->
        </div>
    </div>
</body>
</html>
```

> **Code Explanation:**
> - `1.5rem` always means 1.5 × root font size (16px) = **24px**
> - No matter how deep the nesting, `1.5rem` is always 24px
> - The parent's font size (20px) is completely ignored when using `rem`
> - This predictability is why `rem` is recommended for font sizes

**Quick Comparison:**

| Unit | Relative To | Nesting Behavior | Best For |
|------|------------|-----------------|----------|
| `em` | Parent element | Compounds (multiplies) | Padding/margin relative to font size |
| `rem` | Root `<html>` element | Always consistent | Font sizes (predictable) |
| `px` | Screen pixels | Always fixed | Borders, shadows, small details |

### Font Weight

```css
.light    { font-weight: 300; }
.normal   { font-weight: 400; }   /* same as: normal */
.semibold { font-weight: 600; }
.bold     { font-weight: 700; }   /* same as: bold */
.heavy    { font-weight: 900; }
```

> **Code Explanation:**
> - Font weight ranges from 100 (thinnest) to 900 (thickest), in increments of 100
> - `300` = Light — thin, elegant text
> - `400` = Normal — standard body text (same as writing `font-weight: normal`)
> - `600` = Semi-bold — slightly bolder than normal
> - `700` = Bold — same as writing `font-weight: bold`
> - `900` = Heavy/Black — the thickest weight available
> - Not all fonts support all weights — if you request 300 but the font only has 400 and 700, the browser picks the closest available weight

### Font Shorthand

```css
/* font: style weight size/line-height family; */
p {
    font: italic 600 18px/1.6 'Poppins', sans-serif;
}
```

> **Code Explanation:**
> - `font: italic 600 18px/1.6 'Poppins', sans-serif;` is shorthand for writing 5 separate properties in one line
> - `italic` = font-style | `600` = font-weight (semi-bold) | `18px` = font-size | `1.6` = line-height | `'Poppins', sans-serif` = font-family
> - The order matters! Size and family are **required**; style, weight, and line-height are optional
> - The `/` between `18px` and `1.6` separates font-size from line-height

---

## 3. Text Properties

### Text Alignment & Decoration

```css
.center     { text-align: center; }
.right      { text-align: right; }
.justify    { text-align: justify; }

.underline  { text-decoration: underline; }
.strike     { text-decoration: line-through; }
.no-line    { text-decoration: none; }           /* Remove link underline */

.upper      { text-transform: uppercase; }
.lower      { text-transform: lowercase; }
.cap        { text-transform: capitalize; }
```

> **Code Explanation:**
> - `text-align: center` centers text within its container (like centering a heading)
> - `text-align: justify` stretches text to fill the full width — common in newspapers and books
> - `text-decoration: none` removes the default underline from links — very commonly used
> - `text-decoration: line-through` draws a line through text (useful for showing discounted prices like ~~₹999~~ ₹499)
> - `text-transform: uppercase` converts all text to CAPITAL LETTERS regardless of how it's written in HTML
> - `text-transform: capitalize` makes the First Letter Of Each Word uppercase

### Text Shadow

```css
h1 {
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    /* horizontal vertical blur color */
}

/* Neon glow effect */
.neon {
    color: #fff;
    text-shadow: 0 0 10px #0ff, 0 0 20px #0ff, 0 0 40px #0ff;
}
```

> **Code Explanation:**
> - `text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);` creates a subtle shadow behind the text
>   - `2px` = horizontal offset (shadow moves right)
>   - `2px` = vertical offset (shadow moves down)
>   - `4px` = blur radius (higher = softer shadow)
>   - `rgba(0, 0, 0, 0.3)` = black at 30% opacity
> - The neon effect uses multiple shadows stacked: `0 0 10px`, `0 0 20px`, `0 0 40px` — each one bigger, creating a glow
> - `#0ff` is shorthand for cyan (`#00ffff`)

### Line Height & Spacing

```css
p {
    line-height: 1.8;         /* 1.8× font size */
    letter-spacing: 1px;      /* Space between letters */
    word-spacing: 3px;         /* Space between words */
    text-indent: 40px;         /* First line indent */
}
```

> **Code Explanation:**
> - `line-height: 1.8` sets the space between lines to 1.8 times the font size — makes paragraphs easier to read
> - `letter-spacing: 1px` adds 1px of extra space between each character — useful for headings
> - `word-spacing: 3px` adds extra space between words
> - `text-indent: 40px` indents the first line of a paragraph by 40px — like pressing Tab in a Word document

---

## 4. Complete Text Styling Example

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600;700&family=Playfair+Display:wght@700&display=swap" rel="stylesheet">
    <title>Typography Showcase</title>
    <style>
        /* Base typography settings for the entire page */
        body {
            font-family: 'Poppins', sans-serif;
            font-size: 16px;
            line-height: 1.8;
            color: #333;
            max-width: 800px;
            margin: 40px auto;       /* Center the page content */
            padding: 0 20px;
        }

        /* Elegant serif heading with uppercase and letter spacing */
        h1 {
            font-family: 'Playfair Display', serif;
            font-size: 2.5rem;
            color: #1565C0;
            text-align: center;
            text-transform: uppercase;
            letter-spacing: 3px;
            margin-bottom: 5px;
        }

        /* Light-weight subtitle below the main heading */
        .subtitle {
            text-align: center;
            font-weight: 300;
            font-size: 1.1rem;
            color: #777;
            margin-bottom: 30px;
        }

        /* Section headings with a subtle bottom border */
        h2 {
            font-size: 1.5rem;
            color: #0D47A1;
            border-bottom: 2px solid #E3F2FD;  /* Very light blue border */
            padding-bottom: 5px;
            margin-top: 25px;
        }

        p {
            text-align: justify;
            margin-bottom: 15px;
        }

        /* Magazine-style large first letter effect */
        .drop-cap::first-letter {
            font-size: 3.5em;
            float: left;             /* Float letter so text wraps around it */
            line-height: 1;
            margin-right: 8px;
            color: #1565C0;
            font-weight: 700;
        }

        /* Marker highlight using gradient trick — transparent on top, yellow on bottom */
        .highlight {
            background: linear-gradient(to bottom, transparent 60%, #FFEB3B 60%);
            padding: 0 2px;
        }

        /* Styled quote block with blue left border bar */
        blockquote {
            font-style: italic;
            border-left: 4px solid #1565C0;
            padding: 10px 20px;
            margin: 20px 0;
            background: #F5F5F5;
            color: #555;
        }

        /* Classic formal text appearance */
        .small-caps {
            font-variant: small-caps;
            font-size: 1.1rem;
        }
    </style>
</head>
<body>

    <h1>Typography in CSS</h1>
    <p class="subtitle">Mastering the art of beautiful text on the web</p>

    <h2>The Power of Fonts</h2>
    <p class="drop-cap">Typography is the art and technique of arranging type to make 
    written language legible, readable, and visually appealing. In web design, 
    good typography can make or break a website's user experience.</p>

    <h2>Why Typography Matters</h2>
    <p>Studies show that <span class="highlight">95% of web content is text</span>. 
    Good typography improves readability, establishes visual hierarchy, and creates 
    emotional connections with the reader.</p>

    <blockquote>
        "Web design is 95% typography." — Oliver Reichenstein
    </blockquote>

    <h2>CSS Font Stack</h2>
    <p>Always provide a <span class="highlight">font stack</span> — a list of fonts 
    in order of preference. If the user's device doesn't have the first font, the 
    browser tries the next one, and so on.</p>

    <p class="small-caps">This text uses CSS small-caps variant for a classic look.</p>

</body>
</html>
```

> **Code Explanation:**
> - **Google Fonts:** Two fonts loaded — 'Poppins' (sans-serif for body) and 'Playfair Display' (serif for headings)
> - **Body:** Base font set to Poppins at 16px with 1.8 line spacing, max-width 800px centered with `margin: 40px auto`
> - **h1:** Uses Playfair Display serif font, 2.5rem size, uppercase with 3px letter spacing for an elegant heading
> - **`.subtitle`:** Light weight (300), gray color, centered — creates a secondary heading below the main title
> - **h2:** Blue color with a subtle bottom border using `#E3F2FD` (very light blue) — creates visual section separation
> - **`.drop-cap::first-letter`:** The `::first-letter` pseudo-element makes the first letter of the paragraph large (3.5em), floated left — like a magazine article opening
> - **`.highlight`:** Uses a creative gradient background — transparent on top 60%, yellow on bottom 40% — creating a "marker highlight" effect rather than a full background
> - **Blockquote:** Italic text with a blue left border bar and gray background — standard quote styling pattern
> - **`.small-caps`:** `font-variant: small-caps` converts lowercase letters to smaller capital letters — gives a classic, formal appearance

---

## Practice Exercise

Create a blog article page with:
1. A serif heading font (from Google Fonts)
2. A sans-serif body font
3. Drop cap on the first paragraph
4. Highlighted important phrases
5. A blockquote with special styling
6. Proper line-height, letter-spacing, and text-indent

---

## Summary

| Property | Purpose | Example |
|----------|---------|---------|
| `font-family` | Set typeface | `'Poppins', sans-serif` |
| `font-size` | Set text size | `16px`, `1.2rem` |
| `font-weight` | Bold/light | `400`, `700`, `bold` |
| `font-style` | Italic | `italic`, `normal` |
| `text-align` | Alignment | `center`, `justify` |
| `text-decoration` | Underline/strikethrough | `none`, `underline` |
| `text-transform` | Case | `uppercase`, `capitalize` |
| `text-shadow` | Shadow effect | `2px 2px 4px #000` |
| `line-height` | Vertical spacing | `1.6` |
| `letter-spacing` | Character spacing | `2px` |

---

*Day 20 of 55 | Unit 4 — CSS | Web Technology (25BCA060)*
