# Markdown-to-Medium Converter

> 🗣 This project includes both an **English** and a **German** UI version. See file list below.

This project offers a browser-based HTML tool to convert standard Markdown into clean, Medium.com-compatible HTML — with accurate spacing, styling, and copy behavior.

🗣 **Language availability:**

-  🇩🇪 German UI version: `markdown-to-medium_DE.html`
-  🇬🇧 English UI version: `markdown-to-medium_EN.html`

...

## ✨ Features

-  Live Markdown input and HTML preview side by side
-  Accurate handling of:
   -  Headings (`#`, `##`, `###`)
   -  Bold, italic, and inline code
   -  Code blocks (`...`)
   -  Lists (ordered and unordered)
   -  Blockquotes and links
   -  Horizontal rules (`---`)
-  Removes spacing problems commonly found after headings when pasting into Medium
-  Special copy button optimized for **Chrome and Edge**
   -  Firefox/other users are instructed to copy manually

---

## 🧠 Technical Highlights

-  Clean HTML output via JavaScript-based Markdown parser
-  Live preview and copy-to-clipboard
-  Extensive regex logic to:
   -  Avoid `<br>` or `<p>` after `<h2>`, `<h3>`, `<h4>`
   -  Remove `<h3><br></h3>` situations that cause visual bugs in Medium
   -  Format lists into proper `<ul>` and `<ol>` elements
-  Fully responsive layout (max 1100px wide, height adapted to screen)

---

## 📁 Files

| File                              | Description                      |
| --------------------------------- | -------------------------------- |
| `markdown-to-medium_DE.html`      | German version, optimized layout |
| `markdown-to-medium_EN.html.html` | English version (UI only)        |
| `README.md`                       | This file                        |
| `LICENSE`                         | MIT-Licence                      |

---

## 📝 Usage

1. Open the HTML file in your browser
2. Enter or paste Markdown on the left
3. See the live HTML preview on the right
4. Click the green button to copy the HTML (in Chrome/Edge)
   -  Firefox users: select text manually and press CTRL+C

---

## 🔒 No Dependencies

-  No external libraries
-  No server, no upload — runs 100% locally in your browser
