---
layout: page
title: "How to Format a Chinese Official Document (GB/T 9704) in Word"
date: 2026-11-08
permalink: /gbt9704-official-document-word/
---

# How to Format a Chinese Official Document (GB/T 9704) in Word

If you work with Chinese government or state-owned-enterprise documents, you have met GB/T 9704. It is the national standard for the layout of official documents （党政机关公文格式） — and it is very specific: red header lines, exact margins, a document number in a fixed position, and a seal that has to sit in exactly the right place. Word does not ship with any of this built in.

Here is what the standard actually requires, how to set it up by hand, and the shortcut if you would rather click once.

## What GB/T 9704 requires

The standard (GB/T 9704-2012, the version most offices still use) fixes the page and the layout:

- **Page:** A4 (210 × 297 mm). Margins: 37 mm top, 35 mm bottom, 28 mm left and right.
- **Body text:** FangSong （仿宋） 16pt (三号）, fixed line spacing of 28pt. First line indent of 2 characters.
- **Headings:** Heiti （黑体） — first-level headings in small-2 （小二）, second-level in 3 （三号）, third-level in FangSong bold.
- **Header （版头）:** the issuing authority name in large red Songti （大标宋体， 22pt) centered at the top, with a red rule below it (0.5pt red line, with a 1.5pt red line above the document number area on formal red-headed documents — 红头文件）.
- **Document number （发文字号）:** below the red rule, centered or left-aligned depending on the document type, in FangSong 16pt.
- **Title （标题）:** Songti 22pt (二号）, centered, one or two lines.
- **Signature and seal （落款与印章）:** the issuing unit name at bottom right, the seal centered over it — the standard says the seal should cover the unit name, centered on it, so the name is half-visible under the red seal. This is the detail most people get wrong.
- **Page numbers:** bottom, outside edge — odd pages bottom right, even pages bottom left, in Songti 14pt (四号）.

The most common reason a document gets sent back is not the content. It is a margin that is off by a few millimetres, a body font that is SimSun instead of FangSong, or a seal stamped in the wrong place.

## Doing it by hand in Word

### 1. Set the page first

Page Layout → Margins → Custom Margins: top 3.7 cm, bottom 3.5 cm, left 2.8 cm, right 2.8 cm. Then Page Setup → Layout → set the header/footer distance so the red rule sits where the standard expects it. Get this wrong and every other step inherits the error.

### 2. Build the red header as a header, not as body text

Double-click the header area. Type the authority name, set it to large Songti, 22pt, red (RGB 255, 0, 0), centered. Then add the red rule with a bottom border on the header paragraph — do not draw a line shape, because a shape will drift when the text changes. The border belongs to the paragraph, so it stays put.

### 3. Set up Styles before you type a word

Modify **Normal**: FangSong, 16pt, fixed line spacing 28pt, first-line indent 2 characters. Then set Heading 1/2/3 to Heiti in the sizes above. If you format by hand instead of using Styles, you will re-do the whole document every time the text changes.

### 4. The seal is the hard part

There is no honest shortcut inside Word for a real seal — a seal is a physical stamp or a certified electronic seal image, and a fake one is a legal problem, not a formatting problem. What you can do in Word: leave the signature block exactly where the standard puts it (unit name right-aligned, date below it), and place the seal image anchored to that paragraph so it moves with the text instead of floating free. If your office uses electronic seals, insert the certified image; never draw one.

### 5. Page numbers on the outside edge

Insert a section break if the document has a cover page. In the footer, use different odd/even pages (Page Setup → Layout → Different odd and even) and put the number bottom-right on odd pages, bottom-left on even pages. Typing numbers by hand breaks the moment you add a page.

## The shortcut: format it in one click

If you would rather not spend an afternoon on margins and Styles, I packaged the setup I actually use into a small toolkit: pick your file, pick the official-document preset, click once, and fonts, spacing, margins, and page numbers are set to the standard. It also batch-converts .docx to TXT, Markdown, HTML, and PDF, and does find-and-replace across the body, tables, headers, and footers.

It runs entirely on your computer — no upload, no account, no subscription. One payment, yours forever.

**Word Formatting Toolkit — $19:** https://zhgaleaf.gumroad.com/l/mcarwk

## A checklist before you send it up

- [ ] Margins are exactly 37 / 35 / 28 / 28 mm
- [ ] Body text is FangSong 16pt, 28pt fixed line spacing, first-line indent 2 characters
- [ ] Red header is in the header area with a paragraph border, not a drawn line
- [ ] Document number is in the right position and format
- [ ] Title is Songti 22pt, centered
- [ ] Signature block sits bottom-right with room for the seal over the unit name
- [ ] Page numbers are on the outside edge (odd right, even left)

Formatting is the least interesting part of an official document. Get it right once, in Styles, and never think about it again.
