# Networking Concepts

> **Self-Study Prerequisite** | Estimated Time: 2–3 Hours | No Prior Knowledge Required

---

## Learning Objectives

By the end of this self-study module, you should be able to:

- Explain what a computer network is and name the common types
- Understand IP addresses and how devices find each other on a network
- Describe the basic protocols that make the internet work (TCP, UDP, HTTP)
- Understand how DNS converts website names to numeric addresses

---

## 1. What Is a Computer Network?

A **computer network** is a group of computers connected together so they can **share data and resources**.

### Real-World Analogy

Think of a network like the **Indian postal system**:
- Each house has an **address** → Each computer has an **IP address**
- Letters travel through **post offices** → Data travels through **routers**
- The **postal service** ensures delivery → **Network protocols** ensure data arrives correctly

### Why Do We Need Networks?

| Purpose | Example |
|---------|---------|
| **Sharing files** | Sending a document to your friend's computer |
| **Internet access** | Browsing websites, watching YouTube |
| **Communication** | Email, WhatsApp Web, video calls |
| **Shared resources** | Using one printer for all lab computers |
| **Online services** | Google Docs, online banking, UPI payments |

---

## 2. Types of Networks

| Network Type | Full Form | Range | Example |
|-------------|-----------|-------|---------|
| **PAN** | Personal Area Network | ~10 meters | Bluetooth headphones connected to your phone |
| **LAN** | Local Area Network | A building or campus | Your university computer lab |
| **MAN** | Metropolitan Area Network | A city | Jio/Airtel network across Mandsaur city |
| **WAN** | Wide Area Network | Countries/continents | The Internet itself |

### How Your University Lab Network Works

```
Internet (WAN)
      |
  [ University Router / Gateway ]
      |
  [ Lab Switch ]
      |
  ┌───┼───┬───┬───┬───┐
  PC1 PC2 PC3 PC4 PC5 ... (Lab Computers — LAN)
```

All the computers in your lab are connected to a **switch**, which connects to the university's **router**, which connects to the **internet**.

---

## 3. IP Addresses — The Address of Every Device

An **IP Address** (Internet Protocol Address) is a unique number assigned to every device on a network — just like every house has a unique postal address.

### IPv4 Addresses

The most common type. It looks like four numbers separated by dots:

```
192.168.1.105
```

Each number can be **0 to 255**.

| Part | Meaning |
|------|---------|
| `192.168.1` | The **network** part (which network you're on) |
| `.105` | The **host** part (which specific device on that network) |

### Types of IP Addresses

| Type | Range Example | Used For |
|------|---------------|---------|
| **Private** | `192.168.x.x`, `10.x.x.x` | Your home/lab network (not visible on internet) |
| **Public** | `203.0.113.50` | Visible on the internet (your router's external address) |
| **Localhost** | `127.0.0.1` | Your own computer talking to itself |

### How to Find Your IP Address on Windows

1. Press `Win + R` → Type `cmd` → Press Enter
2. Type `ipconfig` and press Enter
3. Look for **"IPv4 Address"** — that's your IP on the LAN

```
IPv4 Address. . . . . . . . . . . : 192.168.1.105
Subnet Mask . . . . . . . . . . . : 255.255.255.0
Default Gateway . . . . . . . . . : 192.168.1.1
```

---

## 4. How Do Devices Communicate? — Protocols

A **protocol** is a set of rules for how devices communicate — like how there are rules for writing and sending a letter.

### Key Protocols You Should Know

| Protocol | Full Name | What It Does | Analogy |
|----------|-----------|-------------|---------|
| **TCP** | Transmission Control Protocol | Reliable data delivery | Registered post (delivery guaranteed) |
| **UDP** | User Datagram Protocol | Fast but unreliable delivery | Dropping a letter in a postbox (no guarantee) |
| **IP** | Internet Protocol | Addressing and routing | The address on the envelope |
| **HTTP** | HyperText Transfer Protocol | Loading web pages | Asking a librarian for a book |
| **HTTPS** | HTTP Secure | Secure web page loading | Asking a librarian in a private room |
| **DNS** | Domain Name System | Converts names to IPs | A phone book |
| **FTP** | File Transfer Protocol | Uploading/downloading files | Courier service for parcels |
| **SMTP** | Simple Mail Transfer Protocol | Sending emails | The postal delivery system |

### TCP vs UDP — When to Use What?

| Feature | TCP | UDP |
|---------|-----|-----|
| Reliable? | ✅ Yes — checks if data arrived | ❌ No guarantee |
| Speed | Slower (checks every packet) | Faster (just sends) |
| Order? | ✅ Data arrives in order | ❌ May arrive out of order |
| Used for | Web pages, email, file downloads | Video calls, live streaming, gaming |

### Real-World Comparison

**TCP** is like a **phone call**:
- You dial → other person picks up → you confirm they can hear you → you talk → you say goodbye
- This is called the **3-way handshake** (SYN → SYN-ACK → ACK)

**UDP** is like **shouting in a crowd**:
- You shout your message → you hope someone heard it → you don't check

---

## 5. DNS — The Phone Book of the Internet

When you type `www.google.com` in your browser, your computer doesn't understand words — it only understands numbers (IP addresses).

**DNS** (Domain Name System) converts human-readable names to IP addresses:

```
www.google.com  →  142.250.77.46
www.mu.ac.in    →  (Some IP address)
```

### How DNS Works (Step by Step)

1. You type `www.mu.ac.in` in Chrome
2. Your computer asks your **ISP's DNS server**: "What is the IP for `www.mu.ac.in`?"
3. The DNS server looks it up and replies: "It's `103.XX.XX.XX`"
4. Your browser connects to that IP address
5. The website loads on your screen

### Real-World Analogy

**DNS = Phone book / Contact list on your phone**

- You don't memorize phone numbers. You search for "Dad" and your phone finds `+91-98765-43210`
- Similarly, you don't memorize `142.250.77.46`. You type `google.com` and DNS finds the IP

---

## 6. How Data Travels on the Internet

When you open a website, here's what happens behind the scenes:

### The Journey of a Web Request

```
Step 1: You type www.example.com in Chrome

Step 2: DNS converts it to 93.184.216.34

Step 3: Your browser sends an HTTP request:
        "Hey server at 93.184.216.34, send me the homepage!"

Step 4: The request travels through:
        Your PC → Router → ISP → Internet backbone → Destination server

Step 5: The server sends back the HTML page

Step 6: Your browser renders (displays) the page
```

### Data Packets

Your data doesn't travel as one big chunk. It gets broken into small **packets** (like cutting a letter into pieces):

- Each packet has the **sender's address** (your IP), **receiver's address** (server IP), and a **piece of data**
- Packets may take different routes through the internet
- TCP reassembles them in the correct order at the destination

---

## 7. Ports — Doors on a Computer

An **IP address** identifies a computer. A **port number** identifies a specific **service** running on that computer.

### Analogy

Think of an IP address as a **building address** and a port as a **room number**:
- Building: `192.168.1.1` (the computer)
- Room 80: HTTP (web server)
- Room 443: HTTPS (secure web server)
- Room 21: FTP (file transfer)

### Common Port Numbers

| Port | Protocol | What It Does |
|------|----------|-------------|
| **80** | HTTP | Normal web traffic |
| **443** | HTTPS | Secure web traffic |
| **21** | FTP | File transfer |
| **25** | SMTP | Sending email |
| **53** | DNS | Domain name resolution |
| **3306** | MySQL | Database connections |

When you visit `http://www.google.com`, your browser secretly adds `:80` at the end:
```
http://www.google.com:80
```

When you visit `https://www.google.com`, it uses port `:443`:
```
https://www.google.com:443
```

---

## 8. Useful Network Commands on Windows

Open **Command Prompt** (press `Win + R` → type `cmd` → Enter):

### `ipconfig` — See Your Network Details
```
ipconfig
```
Shows your IP address, subnet mask, and gateway.

### `ping` — Check if a Server Is Reachable
```
ping www.google.com
```
Sends small packets to Google and measures how long the reply takes (in milliseconds).

### `tracert` — Trace the Route to a Server
```
tracert www.google.com
```
Shows every router your data passes through on the way to Google.

### `nslookup` — DNS Lookup
```
nslookup www.mu.ac.in
```
Shows the IP address for a domain name.

---

## 9. Client-Server Model

Most of the internet works on the **Client-Server model**:

| Role | What It Is | Example |
|------|-----------|---------|
| **Client** | The device that **requests** data | Your laptop running Chrome |
| **Server** | The device that **provides** data | Google's data center |

```
[Client: Your Browser] ──── Request ────→ [Server: Website]
                        ←── Response ────
```

- When you search on Google, your browser (client) sends a **request**
- Google's server processes it and sends back a **response** (the search results page)
- This is the **request-response cycle** — the foundation of the web

---

## Self-Assessment Questions

1. What is the difference between LAN and WAN? Give one example of each.
2. What is an IP address? What is the IP address for your own computer (localhost)?
3. Explain the difference between TCP and UDP using a real-world analogy.
4. What does DNS do? Why is it needed?
5. What port number is used for HTTP? What about HTTPS?
6. Open Command Prompt and run `ipconfig`. What is your IPv4 address?
7. What is the client-server model? Identify the client and server when you open YouTube.

---

## Quick Summary

| Topic | Key Takeaway |
|-------|-------------|
| Network | Computers connected to share data |
| LAN | Local network (your lab) |
| WAN | Wide network (the Internet) |
| IP Address | Unique number for each device (e.g., `192.168.1.105`) |
| TCP | Reliable delivery (web pages, email) |
| UDP | Fast delivery (video calls, gaming) |
| DNS | Converts names to IPs (`google.com` → `142.250.77.46`) |
| Port | Identifies a service on a computer (80 = HTTP, 443 = HTTPS) |
| Client-Server | Browser requests → Server responds |

---

*This is a self-study prerequisite for the Web Technology (25BCA060) course at Mandsaur University.*
