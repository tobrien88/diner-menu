# The Spallo'brien Diner — Project README

---

## Why: Background & Motivation

In anticipation of a new baby, a large batch of freezer-friendly meals was prepared ahead of time — think: lasagna, pulled pork, chicken marinades, breakfast sandwiches, and more. The goal was to have ready-made food available during the newborn weeks without having to think about cooking.

Rather than leaving a plain list on the fridge, this project turns that meal prep into a proper **retro diner menu** — something fun, functional, and family-worthy. The menu tells anyone reheating a meal exactly what's available, how it was prepped, and what to do with it.

**Aesthetic direction:** 1950s/60s American diner — bold display fonts, a sunburst background, checkerboard borders, and anthropomorphic "food character" illustrations (a breakfast sandwich, a dancing lasagna, a tropical chicken, and a cool pig chef) that give each section personality.

---

## What: The Menu

### Menu Sections

| Section | Items | Icon |
|---|---|---|
| **Breakfast Corner** | Bacon/Sausage Egg & Cheese English Muffins, Hashbrown Bacon Egg Bites | ★ |
| **Soups** | Butternut Squash Soup | ★ |
| **Pasta & Bakes** | Beef Lasagna & Garlic Bread, Pesto Chicken Meatballs, Chef's Pasta | ★ |
| **Chicken Plates** | Pineapple BBQ, Jerk, Pesto, Orange Teriyaki Chicken | ◆ |
| **Handhelds & Plates** | Beef Burritos, Turkey Meatloaf, Pulled Pork Sandwich | ★ |
| **Low & Slow** | Pulled Pork (in marinade) | ◆ |
| **Mama's Sauces** | Italian Red Sauce, Basil Pesto, Turkey Bolognese | ★ |

### Icon Legend
- **★ (star)** — Ready to Reheat: fully cooked, just warm and serve
- **◆ (flame)** — Take & Make: prepped but needs finishing at home (grill, slow cook, etc.)

### Characters
Each section has a character illustration that fits its food group:
- **Egg sandwich guy** — top-left, overlapping the left border (Breakfast Corner)
- **Dancing lasagna** — below Pasta & Bakes items
- **Tropical chicken** — above Chicken Plates header
- **Cool pig chef** — bottom-right corner, overlapping the right border (Handhelds/Low & Slow)

---

## How: Technical Implementation

### Workflow: From Idea to Finished Menu

This project followed a two-phase workflow:

**Phase 1 — Claude Artifacts (Prototyping)**
The initial menu layout, color palette, font choices, and overall structure were designed interactively using Claude's Artifacts feature (claude.ai). Artifacts allows you to build and preview HTML/CSS in real time in the browser, making it ideal for rapid visual iteration. The base layout — sunburst background, checkerboard border, three-column grid, section styling — was fully fleshed out here. Character illustrations were also added as base64-encoded images (embedded directly in the HTML) during this phase.

**Phase 2 — Claude Code (Refinement & Optimization)**
Once the design was validated, the project was ported to Claude Code (the CLI tool) for more precise, file-level work. This enabled:
- Extracting and optimizing image assets
- Running Python scripts for image processing
- Fine-tuning layout, positioning, and typography
- Deploying to GitHub Pages

---

### Technical Tools

#### HTML & CSS
The menu is a single `index.html` file. The layout uses **CSS Grid** (a modern web layout system) to arrange the three-column structure, with absolute positioning for the character illustrations that bleed into the decorative borders. No frameworks or dependencies — just standard web code.

**Fonts** (loaded from Google Fonts):
- *Pacifico* — section headers (retro rounded script)
- *Bangers* — body labels and accents (bold comic-book style)
- *Alfa Slab One* — menu item names (heavy serif)
- *Permanent Marker* — item descriptions and groovy labels (handwritten feel)

#### Python (Image Processing)
Several Python scripts were written and run during the project to process the character illustration PNGs. In plain terms:

- **Background removal (threshold method):** An early pass that identified near-white pixels and made them transparent. Works well for clean backgrounds but can accidentally remove white areas that are part of the illustration (gloves, hats, etc.).

- **Background removal (flood-fill method):** A smarter approach that starts from the image's outer edges and only removes pixels that are *reachable from the border* — meaning internal white areas (like a chef's white apron or egg yolk) are left intact. This is the same concept as Photoshop's "magic wand" tool, implemented from scratch.

- **Tight cropping:** After background removal, scripts calculated the bounding box of remaining visible pixels and cropped each image to the tightest possible frame. This reduced file sizes dramatically (one image went from 1408×736px down to 494×583px) and made sizing the characters in the layout much more predictable.

- **Library used:** [Pillow](https://pillow.readthedocs.io/) — the standard Python image processing library. Equivalent to having basic Photoshop operations available as code.

#### Image Hosting
Originally, all four character images were embedded directly in the HTML as **base64-encoded data** — essentially the entire image file converted to a long text string and pasted inline. This made the HTML file ~1.9MB and meant the browser had to download everything at once before showing anything.

The images were extracted to a dedicated `/images` folder and referenced normally (`<img src="images/cool-pig.png">`), reducing the HTML from **1.9MB to 13KB** — a 99.3% reduction.

#### GitHub Pages
The menu is hosted on **GitHub Pages** — a free static site hosting service built into GitHub. Any HTML/CSS/image files pushed to the repository are automatically served as a live webpage. No server setup, no cost.

---

### File Structure

```
diner-menu/
├── index.html        # The entire menu (layout, styles, content)
├── images/
│   ├── sunny-bfast-sandwich.png   # Egg sandwich character
│   ├── dancing-lasagna.png        # Lasagna character
│   ├── trop-chicken.png           # Tropical chicken character
│   └── cool-pig.png               # Pig chef character
└── README.md
```

---

*Built with Claude Artifacts + Claude Code. Deployed on GitHub Pages.*
