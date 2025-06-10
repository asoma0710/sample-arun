# `filldisk.js` – Abuse HTML5 localStorage to Fill a User's Disk

## Overview

`filldisk.js` is a proof-of-concept that demonstrates how a malicious site can exploit HTML5 `localStorage` to rapidly consume a user's hard drive space. It works on Chrome, Safari (including iOS), and Internet Explorer by repeatedly storing large data chunks across numerous subdomains.

This script is intended for educational purposes to raise awareness about improper storage limit enforcement.

Read the full explanation here:  
[👉 Blog Post: How to Fill a Disk](http://feross.org/fill-disk/)

---

## Features

- Rapidly fills disk space on Chrome, Safari, and IE
- About **1 GB every 16 seconds** on SSD machines
- Causes full browser crashes on 32-bit systems
- Firefox resists this technique due to better storage policies
- Includes a "Stop the madness" button to reclaim space

---

## How It Works

The HTML5 `localStorage` API allows web pages to store up to 5–10 MB of data per origin. But many browsers do **not enforce limits across subdomains**.

This script generates many subdomains like:

1.filldisk.com
2.filldisk.com
3.filldisk.com
...

yaml
Copy
Edit

Each subdomain gets its own `localStorage` space, bypassing origin-based limits and accumulating gigabytes of data until disk space is exhausted.

### Browser limits (as per spec):

- Chrome: 2.5MB per origin (in theory)
- Firefox: 5MB per origin (enforced correctly ✅)
- IE: 10MB per origin
- Safari: 5MB per origin

However, in practice, **Chrome, Safari, and IE do not block this subdomain abuse.**

---

## How to Run This

> ⚠️ Warning: This can lock up your browser or system. Use only in a test environment or sandboxed browser.

1. Clone or download the project files.
2. Host the files locally:

```bash
python -m http.server 8080
Visit the site in Chrome or Safari:


http://localhost:8080
Observe your storage fill up quickly.

To simulate full abuse, you'll need to test on actual subdomains — either by using ngrok, a wildcard DNS setup, or a hosted server with multiple subdomains.

How to Reclaim Disk Space
Chrome
Go to:
Settings > Privacy and Security > Site Settings > View permissions and data stored across sites

Search for your local server or subdomain

Click "Clear data"

Safari
Go to:
Preferences > Privacy > Manage Website Data

Find and delete the storage entries

Or use the "Stop the madness" button in the UI (if enabled).

