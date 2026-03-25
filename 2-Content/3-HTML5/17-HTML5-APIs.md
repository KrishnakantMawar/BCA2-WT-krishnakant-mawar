# Day 17 — HTML5 APIs: Geolocation, Storage & Drag-and-Drop

📖 **Type:** Theory Session
🕐 **Duration:** 2 Hours
📚 **Unit:** 3 — HTML5

---

## Learning Objectives

By the end of this session, students will be able to:
- Use the Geolocation API to get user location
- Store and retrieve data using localStorage and sessionStorage
- Implement basic Drag and Drop functionality
- Understand the difference between cookies and Web Storage

---

## 1. Geolocation API

> **Analogy:** When you open Google Maps on your phone and it shows your location, that's the Geolocation API at work. It asks the device "Where am I?" and the browser asks the user for permission before sharing.

### Getting User Location

```html
<button onclick="getLocation()">📍 Get My Location</button>
<p id="location"></p>

<script>
function getLocation() {
    if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(showPosition, showError);
    } else {
        document.getElementById('location').textContent = 
            "Geolocation is not supported by this browser.";
    }
}

function showPosition(position) {
    const lat = position.coords.latitude;
    const lon = position.coords.longitude;
    document.getElementById('location').innerHTML = 
        `Latitude: ${lat}<br>Longitude: ${lon}<br>
         <a href="https://www.google.com/maps?q=${lat},${lon}" target="_blank">
             View on Google Maps
         </a>`;
}

function showError(error) {
    const messages = {
        1: "User denied the request for Geolocation.",
        2: "Location information is unavailable.",
        3: "The request to get location timed out."
    };
    document.getElementById('location').textContent = 
        messages[error.code] || "An unknown error occurred.";
}
</script>
```

### Position Object Properties

| Property | Description |
|----------|-------------|
| `coords.latitude` | Latitude (decimal degrees) |
| `coords.longitude` | Longitude (decimal degrees) |
| `coords.accuracy` | Accuracy in meters |
| `coords.altitude` | Altitude (if available) |
| `coords.speed` | Speed (if moving) |
| `timestamp` | When the position was determined |

---

## 2. Web Storage API

> **Analogy:** Think of **cookies** as sticky notes on a envelope — small, visible to everyone handling the envelope, and sent back and forth with every request. **Web Storage** is like a **desk drawer** — larger, private, and stays in the browser without being sent with requests.

### localStorage vs sessionStorage vs Cookies

| Feature | localStorage | sessionStorage | Cookies |
|---------|-------------|---------------|---------|
| **Capacity** | ~5-10 MB | ~5-10 MB | ~4 KB |
| **Lifetime** | Until manually deleted | Until tab closes | Configurable expiry |
| **Sent to server** | No | No | Yes (every request) |
| **Scope** | Same origin | Same tab + origin | Same origin |

### localStorage Example

```html
<h2>My Notes App</h2>
<textarea id="notepad" rows="5" cols="50" placeholder="Type your notes..."></textarea>
<br>
<button onclick="saveNote()">💾 Save</button>
<button onclick="loadNote()">📂 Load</button>
<button onclick="clearNote()">🗑️ Clear</button>

<script>
function saveNote() {
    const note = document.getElementById('notepad').value;
    localStorage.setItem('myNote', note);
    alert('Note saved!');
}

function loadNote() {
    const note = localStorage.getItem('myNote');
    if (note) {
        document.getElementById('notepad').value = note;
    } else {
        alert('No saved note found.');
    }
}

function clearNote() {
    localStorage.removeItem('myNote');
    document.getElementById('notepad').value = '';
    alert('Note cleared!');
}
</script>
```

### Web Storage Methods

| Method | Purpose |
|--------|---------|
| `setItem(key, value)` | Store a key-value pair |
| `getItem(key)` | Retrieve value by key |
| `removeItem(key)` | Remove a specific item |
| `clear()` | Remove ALL stored items |
| `key(index)` | Get key name by index |
| `length` | Number of stored items |

### sessionStorage Example

```html
<script>
// Count page views in current session
let views = sessionStorage.getItem('pageViews') || 0;
views = parseInt(views) + 1;
sessionStorage.setItem('pageViews', views);

document.write(`<p>Page views this session: <strong>${views}</strong></p>`);
document.write(`<p><em>Close the tab and reopen — count resets!</em></p>`);
</script>
```

---

## 3. Drag and Drop API

> **Analogy:** Drag and drop on a webpage works just like **moving files on your desktop** — click, hold, drag to a new location, and release.

### Basic Drag and Drop

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Drag and Drop Demo</title>
    <style>
        .drop-zone {
            width: 300px;
            height: 200px;
            border: 3px dashed #aaa;
            margin: 20px;
            padding: 20px;
            text-align: center;
            display: inline-block;
            vertical-align: top;
        }
        .drop-zone.over {
            border-color: #4CAF50;
            background: #E8F5E9;
        }
        .drag-item {
            width: 100px;
            padding: 15px;
            margin: 10px;
            background: #1565C0;
            color: white;
            cursor: grab;
            display: inline-block;
            text-align: center;
        }
    </style>
</head>
<body style="font-family: Arial;">

    <h1>Drag and Drop Demo</h1>

    <div class="drag-item" draggable="true" ondragstart="drag(event)" id="item1">HTML</div>
    <div class="drag-item" draggable="true" ondragstart="drag(event)" id="item2">CSS</div>
    <div class="drag-item" draggable="true" ondragstart="drag(event)" id="item3">JS</div>

    <br>

    <div class="drop-zone" ondrop="drop(event)" ondragover="allowDrop(event)"
         ondragenter="this.classList.add('over')" ondragleave="this.classList.remove('over')">
        <p><strong>Drop Zone 1</strong></p>
        <p>Drop items here</p>
    </div>

    <div class="drop-zone" ondrop="drop(event)" ondragover="allowDrop(event)"
         ondragenter="this.classList.add('over')" ondragleave="this.classList.remove('over')">
        <p><strong>Drop Zone 2</strong></p>
        <p>Drop items here</p>
    </div>

    <script>
    function allowDrop(event) {
        event.preventDefault();
    }

    function drag(event) {
        event.dataTransfer.setData("text", event.target.id);
    }

    function drop(event) {
        event.preventDefault();
        event.target.classList.remove('over');
        const data = event.dataTransfer.getData("text");
        const element = document.getElementById(data);
        if (element) {
            event.currentTarget.appendChild(element);
        }
    }
    </script>

</body>
</html>
```

### Drag and Drop Events

| Event | Fires When |
|-------|-----------|
| `dragstart` | User starts dragging |
| `drag` | During dragging |
| `dragend` | Dragging ends |
| `dragenter` | Dragged item enters drop zone |
| `dragover` | Dragged item is over drop zone |
| `dragleave` | Dragged item leaves drop zone |
| `drop` | Item is dropped |

---

## Practice Exercise

Build a **"Favorite Colors" app** that:
1. Uses Geolocation to show the user's city (approximate)
2. Has a color picker (`<input type="color">`)
3. Saves favorite colors to localStorage
4. Displays saved colors as colored boxes
5. Has a "Clear All" button

---

## Summary

| API | Purpose | Key Methods/Events |
|-----|---------|-------------------|
| **Geolocation** | Get user's location | `getCurrentPosition()` |
| **localStorage** | Persistent browser storage | `setItem()`, `getItem()`, `removeItem()` |
| **sessionStorage** | Tab-scoped storage | Same methods, clears on tab close |
| **Drag and Drop** | Interactive move elements | `dragstart`, `dragover`, `drop` |

---

*Day 17 of 55 | Unit 3 — HTML5 | Web Technology (25BCA060)*
