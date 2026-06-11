# Michelle Vasquez Portfolio — Claude Handoff Document
**Last updated:** June 10, 2026
**Site file:** `/Users/michellevasquez/Desktop/portfolio/index.html` (849 lines, single file, no build step)
**Preview:** Open `index.html` directly in a browser, or run `python3 -m http.server 5500` from the portfolio folder and go to `localhost:5500/index.html`

---

## What This Site Is

A single-file HTML/CSS/JS personal design portfolio for Michelle Vasquez. It mimics a vintage macOS desktop — a title/landing screen styled as an early-2000s Safari browser window leads into a fake desktop with draggable Finder windows for each project.

**Stack:** Vanilla HTML + CSS + JS. Zero dependencies. No npm, no build step.
**Google Fonts used:** `Press Start 2P` (pixel font), `Dancing Script` (cursive)

---

## File & Asset Map

All assets live in `/Users/michellevasquez/Desktop/portfolio/`. Reference them in HTML as `./filename`.

| File | Role in site |
|------|-------------|
| `index.html` | The entire site |
| `wallpaper.png` | Desktop background (Tuscany hills) |
| `cursor.png` | Custom pixel cursor |
| `me!.mp4` | Michelle's face video, bottom-right corner |
| `fav music icon.png` | "Currently Listening" desktop icon (stickered CD) |
| `fav song.png` | Music player window content (Dominic Fike art + Winamp layout) |
| `regfolder.png` | Base folder icon — CSS-filtered to different colors per project |
| `toolsicon.png` | "Tools" desktop icon (pixel art wrench+screwdriver) |
| `pencil.png` | "Writing" desktop icon |
| `bookicon.png` | "Currently Reading" desktop icon |
| `aboutme.txt.png` | "About Me" desktop icon |
| `whentoolsclicked.png` | Tools window content (green circle of app logos) |
| `currentread.png` | Currently Reading window content (library card) |
| `linkedin.png` | LinkedIn logo in menu bar |
| `titlescreen.png` | Reference image for the title screen design |
| `landingpagepopulated.png` | Reference image for the desktop layout |
| `interface.png` | Reference image for the macOS interface style |
| `DIPS.pdf` | Project 3 PDF |
| `AI TA for Canvas.pdf` | Project 1 PDF |
| `Innovative Bag Design.pdf` | Project 2 PDF |
| `Modular Sneaker.pdf` | Project 4 PDF |
| `ELL Onboarding Protocol Reform.pdf` | Project 5 PDF |
| `SINGERS FYS-- Paper #1 (Draft).docx` | Writing folder item |
| `MV-- Stories from the Meth Capital_...pdf` | Writing folder item |
| `CRTW -- Story 1 (1) copy.pdf` | Writing folder item |
| `Michelle Vasquez- ZINE ENTRY.pdf` | Writing folder item |
| `MV -- FILM 47.28 FInal Project copy.pdf` | Writing folder item |

---

## Site Structure (HTML sections in order)

```
<body>
  #custom-cursor         ← pixel cursor div, follows mouse via JS
  #title-screen          ← full-page white overlay shown on load
    .browser-chrome      ← Safari-style browser window (88vw wide)
      .browser-titlebar  ← traffic lights + address bar + Google search
      .browser-bookmarks ← Apple .Mac Amazon eBay Yahoo! News
      .browser-content   ← stickers + "welcome to my" + PORTFOLIO + enter button
  #desktop               ← hidden until "enter" is clicked
    #menubar             ← dark bar: Apple SVG | MV Studio | Contact | eyes | LinkedIn | email | clock
    #desktop-bg          ← wallpaper.png as full background
    #icons-container     ← 10 absolutely positioned .desktop-icon divs
    #corner-character    ← speech bubble + face canvas (green-screened video)
  .finder-window × 11    ← all windows hidden by default, opened by icon click
  #win-aim               ← AIM decoration window (shown alongside contact)
```

### Window IDs and what opens them

| Window ID | Opened by clicking | Content |
|-----------|-------------------|---------|
| `win-music` | "currently listening" (CD icon) | `fav song.png` displayed as image |
| `win-about` | "aboutme.txt" (document icon) | 3-paragraph bio from PDF |
| `win-tools` | "tools" (pixel wrench) | `whentoolsclicked.png` displayed as image |
| `win-reading` | "currently reading" (book icon) | `currentread.png` displayed as image |
| `win-writing` | "writing" (pencil icon) | Finder list view of 5 writing files |
| `win-proj1` | "Project 1" (blue folder) | BLINKY — AI TA for Canvas |
| `win-proj2` | "Project 2" (coral folder) | The Blaggy — Bag Design |
| `win-proj3` | "Project 3" (light blue folder) | DIPS — Web Design |
| `win-proj4` | "Project 4" (lavender folder) | Modular Sneaker |
| `win-proj5` | "Project 5" (green folder) | ELL Onboarding |
| `win-comment` | "Contact" in menu bar | Windows Notepad + AIM side panel |

---

## JavaScript Functions Reference

```js
enterSite()              // fades out title screen, shows desktop
openWindow('win-id')     // shows a finder window; positions AIM next to contact
closeWindow('win-id')    // hides a finder window
startDrag(event, 'id')   // call in onmousedown on .finder-titlebar
updateClock()            // runs every 1s, formats MM.DD.YY
updateEyes(mx, my)       // googly eye tracking, called on mousemove
```

---

## Known Issues & How to Prompt Claude to Fix Them

Each section below describes an issue, the relevant code location, and a ready-to-use prompt.

---

### ISSUE 1 — PORTFOLIO title: plain text instead of objects-in-letters

**What's happening:** The title screen currently shows plain `PORTFOLIO` text in Press Start 2P font. The original design (`titlescreen.png`) shows objects (a ball, a bowling ball, a donut, etc.) embedded inside the letter shapes.

**Why it's plain text:** The individual ball/object images don't exist as separate files in the assets folder, so emojis (🎱🎳🍩) were used first, then removed at your request. The correct fix requires either: (a) providing image files for each object, or (b) using CSS shapes/SVGs to recreate them.

**Prompt to fix it (option A — provide image files):**
> In `/Users/michellevasquez/Desktop/portfolio/index.html`, find the `.portfolio-title` div (around line 245). The text currently reads "PORTFOLIO" as plain text. I have new image files: `ball1.png` (8-ball), `ball2.png` (pink bowling ball), `donut.png`. Replace the first O in PORTFOLIO with `<img src="./ball1.png" style="height:0.85em;width:auto;vertical-align:middle;">`, the second O with `<img src="./ball2.png" ...>`, and the third O with `<img src="./donut.png" ...>`. Keep the surrounding letters in Press Start 2P font at 56px.

**Prompt to fix it (option B — CSS shapes):**
> In `/Users/michellevasquez/Desktop/portfolio/index.html`, find the `.portfolio-title` div. Replace the plain "PORTFOLIO" text with a flex row where: the first O is a 54px black circle (background:#111; border-radius:50%), the second O is a 54px pink circle (background:#ff69b4), and the third O is a 54px donut shape (use a radial-gradient or a circle with a 16px hole). Keep all other letters as spans in Press Start 2P 56px.

---

### ISSUE 2 — Title screen stickers: CSS approximations, not real images

**What's happening:** The stickers (penguin circle, "I ❤ NY", Italian stamp, Dartmouth pennant, Lorax circle, "G" for Curious George) are built entirely from CSS `div` elements — there are no actual sticker image files.

**Where they are in the code:** Inside `.browser-content` in `#title-screen`, the `.sticker` divs (`s-penguin`, `s-stamp`, `s-iny`, `s-george`, `s-dartmouth`, `s-lorax`). Their CSS is in the `<style>` block, class names `.s-*`.

**Prompt to add a real sticker image:**
> In `/Users/michellevasquez/Desktop/portfolio/index.html`, find the sticker with class `s-penguin` inside `#title-screen .browser-content`. Replace the entire `<div class="sticker s-penguin">...</div>` with `<img src="./penguin-sticker.png" class="sticker" style="position:absolute;left:-14px;top:40px;width:48px;height:48px;object-fit:contain;">`. Do the same for `s-george`: replace with `<img src="./george-sticker.png" class="sticker" style="position:absolute;bottom:10px;left:185px;width:52px;height:52px;">`.

---

### ISSUE 3 — Cursor: may still show default cursor on some interactive elements

**What's happening:** `cursor: none !important` is applied to all elements via `*{}` selector, and the custom pixel cursor `cursor.png` follows the mouse via JS. On some browsers or OS settings the default cursor may briefly flash on links/buttons.

**Where it's set:** `*{cursor:none!important;}` at the top of the `<style>` block. The cursor JS is at the very top of the `<script>` block.

**Prompt to fix flashing cursor:**
> In `/Users/michellevasquez/Desktop/portfolio/index.html`, find `*{cursor:none!important;}` in the style block. Add these additional rules directly after it to ensure every interactive element is covered:
> ```css
> a, button, input, textarea, select, [onclick], .desktop-icon, .finder-titlebar, .tl { cursor: none !important; }
> ```
> Also find the custom cursor JS at the top of the script tag and make sure the cursor div is shown from the very start (not only after first mouse move) by adding `cursor.style.display='block'` after the div is first referenced.

---

### ISSUE 4 — Face video: green fringe on edges of Michelle's hair/shoulders

**What's happening:** The canvas green-screen removal (`processFrame()` function in the `<script>` block) uses a threshold of `g > 100 && g > r*1.3 && g > b*1.3`. This removes most of the green background but may leave a green edge/halo around hair.

**Where the code is:** In the `<script>` block, look for `// ── GREEN SCREEN REMOVAL ──`. The threshold is on the line `if (g > 100 && g > r * 1.3 && g > b * 1.3)`.

**Prompt to tune the threshold:**
> In `/Users/michellevasquez/Desktop/portfolio/index.html`, find the green-screen removal function (look for `// ── GREEN SCREEN REMOVAL ──` in the script block). The current green detection is: `if (g > 100 && g > r * 1.3 && g > b * 1.3)`. Please also add a spill-suppression step after the threshold check: for pixels near the green threshold (where green is dominant but not fully transparent), reduce the green channel: `else if (g > 80 && g > r && g > b) { d[i+1] = Math.floor((r + b) / 2); }`. This replaces the green spill on the edges with a neutral tone.

**Prompt if the face is too dark/degraded:**
> In `/Users/michellevasquez/Desktop/portfolio/index.html`, find the green-screen canvas code. The face may be over-processed. Change the threshold from `g > r * 1.3` to `g > r * 1.5` and from `g > b * 1.3` to `g > b * 1.5` to be more conservative and only remove the purest green pixels.

---

### ISSUE 5 — Desktop icon labels: hard to read over certain wallpaper areas

**What's happening:** Icon labels use white text with a dark text-shadow. Over the sky portion of the wallpaper (light blue/white clouds) they can be hard to read.

**Where the CSS is:** `.icon-label` rule in the `<style>` block.

**Prompt to improve legibility:**
> In `/Users/michellevasquez/Desktop/portfolio/index.html`, find the `.icon-label` CSS rule. Replace the `text-shadow` value with a thicker, more opaque multi-layer shadow for better legibility: `text-shadow: 0 0 4px #000, 0 0 8px #000, 1px 1px 2px #000, -1px -1px 2px #000;`. Also add `background: rgba(0,0,0,0.25); border-radius:3px; padding:1px 3px;` to the rule to give labels a subtle dark pill background like classic macOS icon labels.

---

### ISSUE 6 — Project windows: content feels generic / needs real case-study writing

**What's happening:** Project windows (BLINKY, Blaggy, DIPS, Modular Sneaker, ELL) show placeholder content I wrote from the filenames and your PDF template. The PDF template's `{{your context}}` / `{{your problem statement}}` blocks were not yet filled in by you, so those sections use approximate descriptions.

**Where the HTML is:** Each project has its own `<div class="finder-window" id="win-projN">` block. The text lives inside `.proj-body p` elements and `.proj-meta div` elements.

**Prompt to update a specific project:**
> In `/Users/michellevasquez/Desktop/portfolio/index.html`, find the finder window with id `win-proj5` (Project 5 — ELL Onboarding). Inside `.finder-content`, replace all the text in the `.proj-body` div with the following paragraphs: [paste your actual case study text here]. Keep the surrounding HTML structure (`.proj-title`, `.proj-sub`, `.proj-tag`, `.proj-meta`, `.proj-divider`, `.pdf-link`) exactly as-is.

---

### ISSUE 7 — Windows open in fixed positions and may stack badly

**What's happening:** Each finder window has a hardcoded `top` and `left` in its style attribute. When multiple windows are open they can fully overlap.

**Where they're set:** Each `.finder-window` div has `style="width:Npx;top:X%;left:Y%;"`.

**Prompt to add cascade-open positioning:**
> In `/Users/michellevasquez/Desktop/portfolio/index.html`, find the `openWindow(id)` function in the script block. After `win.classList.add('open')`, add logic to cascade each new window slightly offset from the previous one:
> ```js
> const offset = (topZ - 200) * 22;
> win.style.left = (15 + (offset % 200)) + 'px';
> win.style.top  = (60 + (offset % 120)) + 'px';
> ```
> This makes each newly opened window appear 22px right and down from the last, cycling so they don't run off screen.

---

### ISSUE 8 — Title screen browser chrome looks slightly generic

**What's happening:** The `.browser-chrome` is built entirely in CSS with gradients approximating brushed-metal Safari. The reference image `titlescreen.png` shows the original design with more detail.

**Prompt to use titlescreen.png directly:**
> In `/Users/michellevasquez/Desktop/portfolio/index.html`, replace the entire `<div class="browser-chrome">...</div>` block with an image-map approach: show `titlescreen.png` as a large centered image using `<img src="./titlescreen.png" style="max-width:88vw;max-height:82vh;object-fit:contain;display:block;">`, then overlay a transparent `<button>` absolutely positioned over the "enter" button area in the image (approximately center-bottom of the image). The button should call `enterSite()` on click, have `background:transparent; border:none; width:180px; height:50px; position:absolute; bottom:18%; left:50%; transform:translateX(-50%);`.

---

### ISSUE 9 — Menu bar: "Contact" label feels out of place

**What's happening:** The menu bar shows `🍎  MV Studio  Contact`. "Contact" is a clickable item that opens the Notepad window. It works, but the wording may not fit the overall aesthetic.

**Where it is:** Inside `#menubar > .menu-left` in the HTML.

**Prompt to rename it:**
> In `/Users/michellevasquez/Desktop/portfolio/index.html`, find `<span class="menu-item" onclick="openWindow('win-comment')"` inside `#menubar`. Change the text content from `Contact` to whatever label you prefer (e.g., `say hi` or `write me`).

---

### ISSUE 10 — "Currently Listening" icon still shows the stickered CD

**What's happening:** The desktop icon for "currently listening" uses `fav music icon.png` (the stickered CD). The window that opens correctly shows `fav song.png` with the Dominic Fike artwork. But the icon itself is the CD, not the Dominic Fike art.

**Where the icon img is:** Inside `#icons-container`, the first `.desktop-icon` div, its `<img src="./fav music icon.png">`.

**Prompt to change the desktop icon:**
> In `/Users/michellevasquez/Desktop/portfolio/index.html`, find the first `.desktop-icon` inside `#icons-container` (the one with label "currently listening"). Change `<img src="./fav music icon.png"` to `<img src="./fav song.png" style="width:72px;height:72px;object-fit:cover;object-position:5% center;">`. This crops `fav song.png` to show just the Dominic Fike album art as the icon.

---

## General Tips for Prompting Claude

1. **Always give the file path:** Start with `In /Users/michellevasquez/Desktop/portfolio/index.html...`

2. **Name the exact element:** Say `find the .finder-window with id="win-proj3"` not just "find the DIPS window." Claude searches by CSS class/ID.

3. **Specify what to keep:** Say `keep the surrounding HTML structure exactly as-is` when you only want to change text content.

4. **Quote the old text to find/replace:** If changing a few words, quote the exact existing string: `Find the line that reads "BLINKY — Canvas AI Teaching Assistant" and change it to...`

5. **One issue at a time:** If you batch many changes in one message, errors in one can cascade. Fix one thing, verify it works, then move on.

6. **Reference the design images:** Claude has already seen `titlescreen.png` and `landingpagepopulated.png`. You can say "match the style visible in `titlescreen.png`" and it will know what you mean.

7. **Use the preview:** After any change, ask Claude: `Take a screenshot of localhost:5500/index.html at 1280×800 to confirm the fix looks right.`

8. **For content changes only:** If you just want to update text (bio paragraphs, project descriptions), you can paste the new text directly and say: `Replace the text inside #win-proj5 .proj-body with the following: [your text]`

---

## Current Content in the Site (for reference)

### About Me (3 paragraphs, from your PDF)
1. Systems/education reform — "I am drawn to designing and reworking systems and services, especially in the educational field..."
2. HCD/IDEO process — "My projects are based on the Human Centered Design principles and values..."
3. Writing/journaling — "Outside of design, I spend a lot of time writing..."

### Contact info baked in
- Email: `michelle.vasquez.28@dartmouth.edu`
- LinkedIn: `linkedin.com/in/michelle-vasquez-179975324`

### Project meta currently in the site
| Project | Role | Team | Timeline | Tools |
|---------|------|------|----------|-------|
| BLINKY (Proj 1) | Co-Designer | Michelle, Oscar, Paola | — | Canva, Google Slides |
| Blaggy (Proj 2) | Co-Designer | team .kom | — | — |
| DIPS (Proj 3) | Lead UI/UX | Solo | May–Jun 2026 | Claude Code, Canva |
| Modular Sneaker (Proj 4) | Co-Designer/Service | 2 HCD students | Apr 2026 (1 wk) | Gemini, Fuser, Slides |
| ELL Onboarding (Proj 5) | PM + Co-Designer | 5 students + 3 HSD partners | Oct–Nov 2025 | Miro, Canva, Slides |
