# Day 25 — CSS Transitions, Animations & Transforms

📖 **Type:** Theory Session
🕐 **Duration:** 2 Hours
📚 **Unit:** 4 — CSS

---

## Learning Objectives

By the end of this session, students will be able to:
- Apply CSS transitions for smooth property changes
- Create keyframe animations
- Use 2D and 3D transforms (rotate, scale, translate, skew)
- Combine transitions, transforms, and animations for interactive effects

---

## 1. CSS Transitions

> **Analogy:** Without transitions, changing a property is like flipping a **light switch** — instant. With transitions, it's like a **dimmer switch** — smooth and gradual.

### Basic Syntax

```css
.box {
    background: #1565C0;
    width: 200px;
    height: 60px;
    transition: all 0.3s ease;
}

.box:hover {
    background: #E91E63;
    width: 300px;
    transform: scale(1.05);
}
```

> **Code Explanation:**
> - `.box` has a blue background, 200px width, and 60px height as its default state
> - `transition: all 0.3s ease` means "animate ALL property changes over 0.3 seconds with an ease curve"
> - `.box:hover` defines the new state when the mouse hovers — pink background, wider (300px), and slightly scaled up
> - Without the `transition`, these changes would happen instantly; with it, they animate smoothly
> - `all` means any property that changes will be animated — you can also specify individual properties

### Transition Properties

| Property | Values | Description |
|----------|--------|-------------|
| `transition-property` | `all`, `background`, `width`, etc. | What to animate |
| `transition-duration` | `0.3s`, `500ms` | How long |
| `transition-timing-function` | `ease`, `linear`, `ease-in`, `ease-out`, `ease-in-out` | Speed curve |
| `transition-delay` | `0.2s` | Wait before starting |

```css
/* Shorthand */
.box {
    transition: background 0.3s ease, width 0.5s ease-in-out;
}
```

> **Code Explanation:**
> - `transition: background 0.3s ease, width 0.5s ease-in-out` animates two properties with different durations
> - Background changes over 0.3s with `ease` (slow-fast-slow)
> - Width changes over 0.5s with `ease-in-out` (slow start and slow end)
> - Using a comma to separate multiple transitions gives you fine control over each property's animation

### Custom Timing with `cubic-bezier()`

The built-in timing functions (`ease`, `linear`, etc.) are actually `cubic-bezier()` values in disguise:

| Keyword | Cubic-Bezier Equivalent | Behavior |
|---------|------------------------|----------|
| `linear` | `cubic-bezier(0, 0, 1, 1)` | Constant speed — no acceleration |
| `ease` | `cubic-bezier(0.25, 0.1, 0.25, 1)` | Starts slow, speeds up, slows down |
| `ease-in` | `cubic-bezier(0.42, 0, 1, 1)` | Starts slow, speeds up at end |
| `ease-out` | `cubic-bezier(0, 0, 0.58, 1)` | Starts fast, slows down at end |
| `ease-in-out` | `cubic-bezier(0.42, 0, 0.58, 1)` | Slow at both ends, fast in middle |

**How `cubic-bezier(x1, y1, x2, y2)` Works:**

The four values define two control points on a curve:
- **(x1, y1)** = First control point — controls how the animation starts
- **(x2, y2)** = Second control point — controls how the animation ends
- x values must be between 0 and 1 (time: 0=start, 1=end)
- y values CAN go beyond 0-1 (creating "bounce" or "overshoot" effects!)

```css
/* Smooth deceleration — like a car braking gently */
.gentle-stop {
    transition: transform 0.5s cubic-bezier(0.25, 0.46, 0.45, 0.94);
}

/* Bouncy effect — element overshoots then comes back */
.bouncy {
    transition: transform 0.6s cubic-bezier(0.68, -0.55, 0.27, 1.55);
}

/* Snappy start — quick acceleration then gentle stop */
.snappy {
    transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
    /* This is Google Material Design's standard easing */
}
```

> **Code Explanation:**
> - `cubic-bezier(0.25, 0.46, 0.45, 0.94)` creates a smooth deceleration — fast at start, gentle at end
> - `cubic-bezier(0.68, -0.55, 0.27, 1.55)` — the y values `-0.55` and `1.55` go beyond the 0-1 range, creating a "bounce" where the element overshoots its destination then springs back
> - `cubic-bezier(0.4, 0, 0.2, 1)` is Google's Material Design easing — used on Android phones and Google apps
> - **Tip:** Use [cubic-bezier.com](https://cubic-bezier.com/) to visually create custom timing curves — you can drag the control points and see the animation live

---

## 2. CSS Transforms

### 2D Transforms

```css
.translate { transform: translate(50px, 20px); }    /* Move */
.rotate    { transform: rotate(45deg); }              /* Rotate */
.scale     { transform: scale(1.5); }                 /* Resize */
.scale-xy  { transform: scale(2, 0.5); }              /* Stretch */
.skew      { transform: skew(10deg, 5deg); }          /* Slant */

/* Combine multiple transforms */
.combo {
    transform: translate(20px, 0) rotate(10deg) scale(1.1);
}
```

> **Code Explanation:**
> - `translate(50px, 20px)` moves the element 50px right and 20px down from its original position — the original space is preserved
> - `rotate(45deg)` rotates the element 45 degrees clockwise — use negative values for counter-clockwise
> - `scale(1.5)` makes the element 1.5× its original size (150%) — both width and height
> - `scale(2, 0.5)` stretches horizontally (2×) and squishes vertically (0.5×)
> - `skew(10deg, 5deg)` slants the element — like italicizing a shape
> - Multiple transforms can be combined in one line — they apply right to left (last one first)

| Function | Effect | Example |
|----------|--------|---------|
| `translate(x, y)` | Move element | `translate(50px, 20px)` |
| `rotate(angle)` | Rotate | `rotate(45deg)` |
| `scale(x, y)` | Resize | `scale(1.5)` |
| `skew(x, y)` | Slant | `skew(10deg)` |

### `transform-origin` — Changing the Rotation Point

By default, transforms happen from the **center** of the element. `transform-origin` lets you change this:

```css
/* Default: center of element */
.rotate-center {
    transform: rotate(45deg);
    transform-origin: center;         /* Same as 50% 50% */
}

/* Rotate from top-left corner */
.rotate-corner {
    transform: rotate(45deg);
    transform-origin: top left;       /* Same as 0% 0% */
}

/* Rotate from bottom-right */
.rotate-bottom-right {
    transform: rotate(45deg);
    transform-origin: bottom right;   /* Same as 100% 100% */
}

/* Custom point: 20% from left, 80% from top */
.rotate-custom {
    transform: rotate(45deg);
    transform-origin: 20% 80%;
}
```

> **Code Explanation:**
> - `transform-origin: center` (default) — the element rotates around its center point, like spinning a coin on a table
> - `transform-origin: top left` — the element rotates around its top-left corner, like opening a book
> - `transform-origin: bottom right` — rotates from the bottom-right, like a clock hand anchored at the corner
> - You can use keywords (`top`, `left`, `center`, `bottom`, `right`), percentages, or pixel values
> - **Analogy:** Think of a **ceiling fan** — the `transform-origin` is where the fan is attached to the ceiling. The blades (element) rotate around that fixed point. Moving the origin is like moving the fan's mounting point

### 3D Transforms

```css
.rotate-x { transform: rotateX(45deg); }   /* Flip forward */
.rotate-y { transform: rotateY(45deg); }   /* Turn sideways */
.rotate-z { transform: rotateZ(45deg); }   /* Same as rotate() */

/* For 3D effect, parent needs perspective */
.parent {
    perspective: 800px;
}
```

> **Code Explanation:**
> - `rotateX(45deg)` rotates the element around the horizontal axis — like tilting a book forward toward you
> - `rotateY(45deg)` rotates around the vertical axis — like opening a door sideways
> - `rotateZ(45deg)` rotates around the Z axis (toward/away from screen) — same effect as `rotate(45deg)`
> - `perspective: 800px` on the parent creates a 3D space — smaller values = more dramatic 3D effect, larger values = subtler

### Working 3D Transform Example — Card Flip Effect

```html
<!-- 3D Card Flip Effect -->
<div style="perspective: 800px; width: 250px; height: 150px; margin: 30px auto;">
    <div style="
        width: 100%;
        height: 100%;
        position: relative;
        transform-style: preserve-3d;
        transition: transform 0.6s ease;
    " onmouseover="this.style.transform='rotateY(180deg)'" 
       onmouseout="this.style.transform='rotateY(0deg)'">
        
        <!-- Front face of card -->
        <div style="
            position: absolute; width: 100%; height: 100%;
            backface-visibility: hidden;
            background: linear-gradient(135deg, #1565C0, #0D47A1);
            color: white; display: flex; align-items: center; 
            justify-content: center; border-radius: 10px;
            font-family: Arial, sans-serif; font-size: 18px;
        ">
            🏛️ Mandsaur University
        </div>
        
        <!-- Back face of card (rotated 180deg) -->
        <div style="
            position: absolute; width: 100%; height: 100%;
            backface-visibility: hidden;
            transform: rotateY(180deg);
            background: linear-gradient(135deg, #4CAF50, #2E7D32);
            color: white; display: flex; align-items: center;
            justify-content: center; border-radius: 10px;
            font-family: Arial, sans-serif; font-size: 16px;
        ">
            BCA - Web Technology
        </div>
    </div>
</div>
```

> **Code Explanation:**
> - **`perspective: 800px`** on the outer container creates a 3D viewing space — without this, rotations look flat
> - **`transform-style: preserve-3d`** tells the inner container to keep its children in 3D space (not flatten them)
> - **`backface-visibility: hidden`** hides the back of each face — without this, you'd see a mirrored version when the card flips
> - **Front face:** Normal positioning, shown by default
> - **Back face:** Pre-rotated 180° with `rotateY(180deg)` — it starts facing away from you and becomes visible only when the card flips
> - **`transition: transform 0.6s ease`** makes the flip animation smooth
> - The `onmouseover`/`onmouseout` events trigger the 180° rotation on hover

---

## 3. CSS Animations (Keyframes)

> **Analogy:** Transitions are like a **single camera shot** from A to B. Animations are like a **full movie** — you define every scene (keyframe), and the browser plays through them.

### Basic Animation

```css
@keyframes slideIn {
    from {
        transform: translateX(-100%);
        opacity: 0;
    }
    to {
        transform: translateX(0);
        opacity: 1;
    }
}

.animated {
    animation: slideIn 0.5s ease forwards;
}
```

> **Code Explanation:**
> - `@keyframes slideIn` defines an animation named "slideIn" with two states: `from` (start) and `to` (end)
> - `from { transform: translateX(-100%); opacity: 0; }` — starts off-screen to the left and invisible
> - `to { transform: translateX(0); opacity: 1; }` — ends at normal position and fully visible
> - `.animated { animation: slideIn 0.5s ease forwards; }` applies the animation over 0.5 seconds
> - `forwards` keeps the element in its `to` state after the animation ends — without it, the element snaps back to `from`

### Multi-Step Animation

```css
@keyframes rainbow {
    0%   { background: #FF0000; }
    16%  { background: #FF9900; }
    33%  { background: #FFFF00; }
    50%  { background: #00FF00; }
    66%  { background: #0000FF; }
    83%  { background: #9900FF; }
    100% { background: #FF0000; }
}

.rainbow-box {
    animation: rainbow 4s linear infinite;
}
```

> **Code Explanation:**
> - `@keyframes rainbow` defines 7 color stops at different percentages of the animation timeline
> - `0%` and `100%` are both red — this creates a seamless loop when the animation repeats
> - `.rainbow-box { animation: rainbow 4s linear infinite; }` — plays the animation over 4 seconds, at constant speed, repeating forever
> - `linear` ensures each color transition takes equal time — `ease` would make some transitions faster than others

### Animation Properties

| Property | Values |
|----------|--------|
| `animation-name` | Name of `@keyframes` |
| `animation-duration` | `1s`, `500ms` |
| `animation-timing-function` | `ease`, `linear`, `ease-in-out` |
| `animation-delay` | `0.5s` |
| `animation-iteration-count` | `1`, `3`, `infinite` |
| `animation-direction` | `normal`, `reverse`, `alternate` |
| `animation-fill-mode` | `none`, `forwards`, `backwards`, `both` |

```css
/* Shorthand */
.box {
    animation: bounce 1s ease-in-out 0.2s infinite alternate;
    /* name | duration | timing | delay | count | direction */
}
```

> **Code Explanation:**
> - `animation: bounce 1s ease-in-out 0.2s infinite alternate` packs all animation properties into one line
> - `bounce` = animation name | `1s` = duration | `ease-in-out` = timing | `0.2s` = delay before starting | `infinite` = repeat forever | `alternate` = play forward, then backward, then forward...
> - `alternate` creates a "ping-pong" effect — great for breathing/pulsing animations
> - `forwards` fill mode keeps the final state; `backwards` applies the first keyframe during the delay period; `both` does both

### Accessibility: `prefers-reduced-motion`

Some users have **motion sensitivity** — animations can cause dizziness, headaches, or nausea. The `prefers-reduced-motion` media query lets you respect their operating system settings:

```css
/* Normal animation for most users */
.animated-element {
    animation: slideIn 0.5s ease forwards;
    transition: transform 0.3s ease;
}

/* Reduced motion for users who prefer it */
@media (prefers-reduced-motion: reduce) {
    .animated-element {
        animation: none;              /* Remove all animations */
        transition: none;             /* Remove all transitions */
    }
    
    /* Or provide a subtle alternative instead of removing completely */
    .fade-element {
        animation: none;
        opacity: 1;                   /* Just show the element instantly */
    }
}
```

> **Code Explanation:**
> - `@media (prefers-reduced-motion: reduce)` activates when the user has enabled "Reduce motion" in their OS settings (Windows: Settings → Accessibility → Visual Effects → Animation effects OFF)
> - `animation: none` removes all keyframe animations — elements appear in their final state instantly
> - `transition: none` removes smooth transitions — changes happen immediately
> - It's better to provide subtle alternatives (like a simple fade) rather than removing all motion completely
> - **This is an accessibility best practice** — always include this in production websites

> **Who benefits from this?**
> - People with **vestibular disorders** (balance-related conditions)
> - Users prone to **motion sickness**
> - People with **epilepsy** (some animations can trigger seizures)
> - Anyone who simply finds excessive animation distracting

**Best Practice — "Motion-Safe" Approach:**

```css
/* Start with NO animations (safe default) */
.card {
    opacity: 1;
    transform: none;
}

/* Only add animation if user is OK with motion */
@media (prefers-reduced-motion: no-preference) {
    .card {
        animation: fadeInUp 0.5s ease forwards;
    }
}
```

> **Code Explanation:**
> - Instead of adding animations and then removing them, this approach starts with NO animations as the default
> - Animations are only added if the user has NOT requested reduced motion (`no-preference`)
> - This is called the **"motion-safe" approach** — safer because new users and old browsers get the no-animation default

---

## 4. Practical: Interactive Button & Card Effects

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS Animations & Transitions</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body {
            font-family: 'Segoe UI', sans-serif;
            background: #f0f0f0;
            padding: 30px;
        }
        h1 { text-align: center; color: #1565C0; margin-bottom: 30px; }
        h2 { color: #333; margin: 30px 0 15px; text-align: center; }

        /* ===== BUTTON EFFECTS ===== */
        .btn-row {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }
        .btn {
            padding: 12px 30px;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            color: white;
            transition: all 0.3s ease;
        }
        .btn-grow:hover {
            transform: scale(1.1);
        }
        .btn-shadow:hover {
            box-shadow: 0 8px 25px rgba(0,0,0,0.3);
            transform: translateY(-3px);
        }
        .btn-slide {
            position: relative;
            overflow: hidden;
            z-index: 1;
        }
        .btn-slide::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: rgba(255,255,255,0.2);
            transition: left 0.3s ease;
            z-index: -1;
        }
        .btn-slide:hover::before {
            left: 0;
        }
        .btn-1 { background: #1565C0; }
        .btn-2 { background: #E91E63; }
        .btn-3 { background: #4CAF50; }

        /* ===== CARD HOVER EFFECTS ===== */
        .card-row {
            display: flex;
            justify-content: center;
            gap: 20px;
            flex-wrap: wrap;
        }
        .card {
            width: 250px;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .card:hover {
            transform: translateY(-10px);
            box-shadow: 0 12px 30px rgba(0,0,0,0.15);
        }
        .card-header {
            height: 120px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.5em;
            color: white;
        }
        .card-body {
            padding: 20px;
        }
        .card-body h3 { margin-bottom: 5px; }
        .card-body p { color: #777; font-size: 14px; }

        /* ===== LOADING SPINNER ===== */
        @keyframes spin {
            0%   { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        .spinner {
            width: 50px;
            height: 50px;
            border: 5px solid #e0e0e0;
            border-top: 5px solid #1565C0;
            border-radius: 50%;
            animation: spin 1s linear infinite;
            margin: 0 auto;
        }

        /* ===== PULSE EFFECT ===== */
        @keyframes pulse {
            0%   { transform: scale(1); opacity: 1; }
            50%  { transform: scale(1.05); opacity: 0.7; }
            100% { transform: scale(1); opacity: 1; }
        }
        .pulse {
            animation: pulse 2s ease-in-out infinite;
        }

        /* ===== FADE IN ON LOAD ===== */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        .fade-in {
            animation: fadeInUp 0.8s ease forwards;
        }
        .delay-1 { animation-delay: 0.1s; opacity: 0; }
        .delay-2 { animation-delay: 0.3s; opacity: 0; }
        .delay-3 { animation-delay: 0.5s; opacity: 0; }
    </style>
</head>
<body>

    <h1 class="fade-in">CSS Transitions & Animations</h1>

    <h2>Button Effects</h2>
    <div class="btn-row">
        <button class="btn btn-1 btn-grow">Grow</button>
        <button class="btn btn-2 btn-shadow">Shadow Lift</button>
        <button class="btn btn-3 btn-slide">Slide Shine</button>
    </div>

    <h2>Card Hover Effects</h2>
    <div class="card-row">
        <div class="card fade-in delay-1">
            <div class="card-header" style="background: linear-gradient(135deg, #667eea, #764ba2);">🌐</div>
            <div class="card-body">
                <h3>HTML5</h3>
                <p>Structure and semantics</p>
            </div>
        </div>
        <div class="card fade-in delay-2">
            <div class="card-header" style="background: linear-gradient(135deg, #11998e, #38ef7d);">🎨</div>
            <div class="card-body">
                <h3>CSS3</h3>
                <p>Styling and animations</p>
            </div>
        </div>
        <div class="card fade-in delay-3">
            <div class="card-header" style="background: linear-gradient(135deg, #ee0979, #ff6a00);">⚡</div>
            <div class="card-body">
                <h3>JavaScript</h3>
                <p>Interactivity and logic</p>
            </div>
        </div>
    </div>

    <h2>Loading Spinner</h2>
    <div class="spinner"></div>

    <h2>Pulse Effect</h2>
    <p style="text-align:center;">
        <span class="pulse" style="display:inline-block; background:#E91E63; color:white; padding:15px 30px; border-radius:50px; font-size:18px;">
            🔴 LIVE
        </span>
    </p>

</body>
</html>
```

> **Code Explanation:**
> - **Button Effects:**
>   - `.btn-grow:hover` uses `scale(1.1)` to make the button 10% larger on hover
>   - `.btn-shadow:hover` adds a large shadow and moves the button up 3px (`translateY(-3px)`) — creates a "lifting" effect
>   - `.btn-slide` uses a `::before` pseudo-element that slides in from the left on hover — a semi-transparent white overlay creates a "shine" effect
> - **Card Hover:** Cards move up 10px (`translateY(-10px)`) and get a bigger shadow on hover — this is the standard "card lift" effect used by sites like Flipkart and Amazon
> - **Loading Spinner:** A circle with one colored border side (`border-top: 5px solid #1565C0`) rotates 360° infinitely — the simplest loading animation
> - **Pulse Effect:** `scale(1)` → `scale(1.05)` → `scale(1)` with opacity changes creates a "breathing" effect — used for live indicators and notification badges
> - **Fade In:** `fadeInUp` moves elements from 30px below to their normal position while fading in — `.delay-1`, `.delay-2`, `.delay-3` stagger the animation so cards appear one after another
> - **`opacity: 0` on delay classes:** Elements start invisible; the animation fills `forwards` to make them visible — without initial `opacity: 0`, elements would flash before animating

---

## Summary

| Concept | Key Property | Purpose |
|---------|-------------|---------|
| Transitions | `transition: all 0.3s ease` | Smooth property changes |
| Transforms | `transform: rotate(45deg)` | Move, rotate, scale, skew |
| Animations | `@keyframes` + `animation` | Multi-step sequences |
| 3D | `perspective`, `rotateX/Y` | Depth effects |

**🎉 Unit 4 Complete!** Starting Day 26, we begin **Unit 5: JavaScript** — adding interactivity and dynamic behavior to our styled web pages.

---

*Day 25 of 55 | Unit 4 — CSS | Web Technology (25BCA060)*
