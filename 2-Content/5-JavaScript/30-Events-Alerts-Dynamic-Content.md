# Day 30 — JavaScript Events, Alerts & Dynamic Content

🔬 **Type:** Theory + Practical
🕐 **Duration:** 2 Hours
📚 **Unit:** 5 — JavaScript
🧪 **Lab Experiments:** 17 (contd.), Review of 18-21

---

## Learning Objectives

By the end of this session, students will be able to:
- Handle various JavaScript events
- Use alert, confirm, and prompt dialogs
- Manipulate dates with the Date object
- Build interactive dynamic pages combining all JS concepts

---

## 1. JavaScript Events

> **Analogy:** Events are like **doorbells** — when someone presses the button (user interaction), it triggers an action (a function runs).

### Common Events

| Event | Triggers When |
|-------|--------------|
| `click` | Element is clicked |
| `dblclick` | Element is double-clicked |
| `mouseover` | Mouse enters element |
| `mouseout` | Mouse leaves element |
| `keydown` | Key is pressed |
| `keyup` | Key is released |
| `focus` | Input receives focus |
| `blur` | Input loses focus |
| `change` | Select/checkbox value changes |
| `submit` | Form is submitted |
| `load` | Page finishes loading |
| `scroll` | User scrolls |

### Adding Event Listeners

```javascript
// Method 1: Inline (avoid)
// <button onclick="doSomething()">Click</button>

// Method 2: Property
document.getElementById('btn').onclick = function() {
    alert('Clicked!');
};

// Method 3: addEventListener (recommended)
document.getElementById('btn').addEventListener('click', function() {
    alert('Clicked!');
});
```

### The Event Object

```javascript
document.addEventListener('keydown', function(event) {
    console.log(`Key pressed: ${event.key}`);
    console.log(`Key code: ${event.code}`);
    
    if (event.key === 'Enter') {
        console.log('Enter was pressed!');
    }
});

document.getElementById('box').addEventListener('click', function(event) {
    console.log(`Clicked at X: ${event.clientX}, Y: ${event.clientY}`);
});
```

---

## 2. Dialog Boxes

### Alert (Information)

```javascript
alert('Welcome to the website!');
```

### Confirm (Yes/No Question)

```javascript
const answer = confirm('Are you sure you want to delete?');
if (answer) {
    console.log('User clicked OK — deleting...');
} else {
    console.log('User clicked Cancel — keeping...');
}
```

### Prompt (Get Input)

```javascript
const name = prompt('What is your name?', 'Student');
if (name !== null && name.trim() !== '') {
    alert(`Hello, ${name}!`);
}
```

---

## 3. Date Object

```javascript
const now = new Date();

console.log(now.getFullYear());     // 2026
console.log(now.getMonth());        // 0-11 (April = 3)
console.log(now.getDate());         // Day of month (1-31)
console.log(now.getDay());          // Day of week (0=Sun, 6=Sat)
console.log(now.getHours());        // 0-23
console.log(now.getMinutes());      // 0-59
console.log(now.getSeconds());      // 0-59

// Format date
console.log(now.toLocaleDateString('en-IN'));  // "28/4/2026"
console.log(now.toLocaleTimeString('en-IN'));  // "10:30:00 am"
```

### Timers

```javascript
// Run after 3 seconds (once)
setTimeout(() => {
    alert('3 seconds passed!');
}, 3000);

// Run every 1 second (repeating)
const timer = setInterval(() => {
    console.log(new Date().toLocaleTimeString());
}, 1000);

// Stop the interval
clearInterval(timer);
```

---

## Practical Session: Interactive Dashboard

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive JS Dashboard</title>
    <style>
        * { box-sizing: border-box; margin: 0; padding: 0; }
        body { font-family: 'Segoe UI', sans-serif; background: #f0f0f0; }
        
        header {
            background: linear-gradient(135deg, #1565C0, #0D47A1);
            color: white; text-align: center; padding: 20px;
        }
        header h1 { font-size: 1.8em; }
        #clock { font-size: 2.5em; font-weight: 300; margin-top: 5px; }
        #date { opacity: 0.8; }

        .container { max-width: 800px; margin: 20px auto; padding: 0 20px; }
        
        .card {
            background: white; border-radius: 10px; padding: 25px;
            margin-bottom: 20px; box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }
        .card h3 { color: #1565C0; margin-bottom: 12px; }
        
        input { padding: 10px; border: 1px solid #ddd; border-radius: 5px;
                font-size: 15px; width: 100%; margin-bottom: 10px; }
        
        .btn {
            padding: 10px 20px; border: none; border-radius: 5px;
            cursor: pointer; color: white; font-size: 14px; margin: 3px;
        }
        .btn-blue { background: #1565C0; }
        .btn-green { background: #4CAF50; }
        .btn-red { background: #E91E63; }

        .counter-display {
            font-size: 4em; text-align: center; padding: 20px;
            color: #1565C0; font-weight: bold;
        }

        .event-log {
            background: #f9f9f9; padding: 10px; border-radius: 5px;
            max-height: 200px; overflow-y: auto; font-family: monospace;
            font-size: 13px;
        }
        .event-log p { padding: 3px 0; border-bottom: 1px solid #eee; }

        .typing-area {
            width: 100%; padding: 10px; border: 2px solid #ddd;
            border-radius: 5px; font-size: 15px; min-height: 80px;
            resize: vertical;
        }
        #charCount { color: #777; font-size: 14px; margin-top: 5px; }
        #keyOutput { margin-top: 10px; font-size: 1.5em; text-align: center;
                     padding: 15px; background: #f0f0f0; border-radius: 5px; }
    </style>
</head>
<body>

    <header>
        <h1>JavaScript Dashboard</h1>
        <div id="clock">--:--:--</div>
        <div id="date">Loading...</div>
    </header>

    <div class="container">

        <!-- 1. Counter with Events -->
        <div class="card">
            <h3>1. Counter (Click Events)</h3>
            <div class="counter-display" id="counter">0</div>
            <div style="text-align: center;">
                <button class="btn btn-red" id="decBtn">− Decrease</button>
                <button class="btn btn-blue" id="resetBtn">Reset</button>
                <button class="btn btn-green" id="incBtn">+ Increase</button>
            </div>
        </div>

        <!-- 2. Keyboard Events -->
        <div class="card">
            <h3>2. Keyboard Events</h3>
            <textarea class="typing-area" id="typingArea" placeholder="Start typing here..."></textarea>
            <div id="charCount">Characters: 0 | Words: 0</div>
            <div id="keyOutput">Press any key...</div>
        </div>

        <!-- 3. Mouse Events -->
        <div class="card">
            <h3>3. Mouse Event Logger</h3>
            <div id="mouseBox" 
                 style="height: 150px; background: linear-gradient(135deg, #667eea, #764ba2);
                        border-radius: 10px; display: flex; align-items: center;
                        justify-content: center; color: white; font-size: 1.2em; cursor: crosshair;">
                Move your mouse here!
            </div>
            <div class="event-log" id="eventLog"></div>
        </div>

        <!-- 4. Countdown Timer -->
        <div class="card">
            <h3>4. Countdown Timer</h3>
            <input type="number" id="timerInput" placeholder="Enter seconds (e.g., 10)" min="1" max="3600">
            <button class="btn btn-green" id="startTimer">▶ Start</button>
            <button class="btn btn-red" id="stopTimer">■ Stop</button>
            <div style="text-align: center; font-size: 3em; padding: 20px; color: #1565C0; font-weight: bold;"
                 id="timerDisplay">00:00</div>
        </div>
    </div>

    <script>
        // ===== LIVE CLOCK =====
        function updateClock() {
            const now = new Date();
            document.getElementById('clock').textContent = now.toLocaleTimeString('en-IN');
            
            const options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
            document.getElementById('date').textContent = now.toLocaleDateString('en-IN', options);
        }
        setInterval(updateClock, 1000);
        updateClock();

        // ===== 1. COUNTER =====
        let count = 0;
        const counterEl = document.getElementById('counter');
        
        document.getElementById('incBtn').addEventListener('click', () => {
            count++;
            counterEl.textContent = count;
        });
        document.getElementById('decBtn').addEventListener('click', () => {
            count--;
            counterEl.textContent = count;
        });
        document.getElementById('resetBtn').addEventListener('click', () => {
            count = 0;
            counterEl.textContent = count;
        });

        // ===== 2. KEYBOARD EVENTS =====
        const typingArea = document.getElementById('typingArea');
        
        typingArea.addEventListener('input', () => {
            const text = typingArea.value;
            const chars = text.length;
            const words = text.trim() === '' ? 0 : text.trim().split(/\s+/).length;
            document.getElementById('charCount').textContent = `Characters: ${chars} | Words: ${words}`;
        });
        
        typingArea.addEventListener('keydown', (e) => {
            document.getElementById('keyOutput').textContent = 
                `Key: "${e.key}" | Code: ${e.code}`;
        });

        // ===== 3. MOUSE EVENTS =====
        const mouseBox = document.getElementById('mouseBox');
        const eventLog = document.getElementById('eventLog');
        
        function logEvent(msg) {
            const p = document.createElement('p');
            p.textContent = `[${new Date().toLocaleTimeString()}] ${msg}`;
            eventLog.prepend(p);
            if (eventLog.children.length > 20) eventLog.lastChild.remove();
        }
        
        mouseBox.addEventListener('mousemove', (e) => {
            mouseBox.textContent = `X: ${e.offsetX}, Y: ${e.offsetY}`;
        });
        mouseBox.addEventListener('click', (e) => logEvent(`Click at (${e.offsetX}, ${e.offsetY})`));
        mouseBox.addEventListener('dblclick', () => logEvent('Double-click!'));
        mouseBox.addEventListener('mouseenter', () => logEvent('Mouse entered'));
        mouseBox.addEventListener('mouseleave', () => logEvent('Mouse left'));

        // ===== 4. COUNTDOWN TIMER =====
        let timerInterval = null;
        
        document.getElementById('startTimer').addEventListener('click', () => {
            clearInterval(timerInterval);
            let seconds = parseInt(document.getElementById('timerInput').value);
            if (isNaN(seconds) || seconds <= 0) { alert('Enter a valid number!'); return; }
            
            function updateTimer() {
                const mins = String(Math.floor(seconds / 60)).padStart(2, '0');
                const secs = String(seconds % 60).padStart(2, '0');
                document.getElementById('timerDisplay').textContent = `${mins}:${secs}`;
                
                if (seconds <= 0) {
                    clearInterval(timerInterval);
                    document.getElementById('timerDisplay').textContent = "⏰ TIME UP!";
                    return;
                }
                seconds--;
            }
            updateTimer();
            timerInterval = setInterval(updateTimer, 1000);
        });
        
        document.getElementById('stopTimer').addEventListener('click', () => {
            clearInterval(timerInterval);
        });
    </script>

</body>
</html>
```

---

## Summary

| Concept | Key Syntax |
|---------|-----------|
| addEventListener | `el.addEventListener('click', fn)` |
| Event object | `event.key`, `event.clientX` |
| alert / confirm / prompt | User dialogs |
| Date | `new Date()`, `.getHours()`, `.toLocaleString()` |
| setTimeout | One-time delay |
| setInterval | Repeating timer |

**🎉 Unit 5 Complete!** Starting Day 31, we begin **Unit 6: Bootstrap** — a CSS framework that makes responsive design fast and easy.

---

*Day 30 of 55 | Unit 5 — JavaScript | Web Technology (25BCA060)*
