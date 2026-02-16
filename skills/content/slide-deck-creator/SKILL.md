---
name: slide-deck-creator
description: HTML slide decks with consistent design system. Use when creating presentations, pitch decks, or slide-based content.
---

Create a slide deck about: $ARGUMENTS

## Overview

Create HTML slide files (.mockup.html) that match the Nimbalyst brand style guide. Each slide is an individual mockup file at 720pt x 405pt (16:9).

## Style Guide Reference

Before creating slides, read the style guide at `nimbalyst-local/designs/slide-style-guide.mockup.html` to understand the full design system. The key tokens are summarized below.

## Design Tokens

### Colors
```
Electric Blue:     #382DCF  (headers, accents, buttons, borders)
Electric Hover:    #2B22A6
Electric Pressed:  #211A80
Midnight Blue:     #241D71  (title slide bg, body text on light)
Midnight Deep:     #1C165E  (cards on dark, footer borders)
Blue Light:        #B8B0F0  (subtitles on dark, card headers on dark)
Blue Wash:         #E0DEF5  (badges, pills)
Blue Tint:         #EEEDFA  (card backgrounds, callouts, section bgs)
White:             #FFFFFF  (content slide bg, text on dark)
Ice:               #E8EEFF  (body text on dark navy)
Sky Blue:          #6E95FF  (lighter accent, highlights, links)
Slate Blue:        #394F79  (muted text, descriptions, footer)
Cool Slate:        #5571A3  (author, metadata on dark)
```

### Gradients
```
Title text:        linear-gradient(135deg, #382DCF, #6E95FF)  (background-clip: text)
Section bg:        linear-gradient(180deg, #FFFFFF 0%, #EEEDFA 100%)  (with optional dot pattern)
```

### Typography
```
Font:              'Euclid Circular A', 'Inter', Arial, sans-serif
H1:                42pt / Bold / 120%    (title slides)
H2:                28pt / Bold / 120%    (section headers)
H3:                22pt / Bold / 120%    (subsection headers)
H4:                14pt / SemiBold / 130% (card titles)
Body:              12pt / Regular / 140%  (content text)
Body Medium:       12pt / Medium / 120%   (emphasized body)
Caption:           10pt / Regular / 140%  (footer, metadata)
```

### Spacing
```
Slide size:        720pt x 405pt
Content padding:   40pt horizontal, 25-30pt vertical
Header padding:    25pt 40pt
Card radius:       8pt
Card padding:      12-15pt
Column gap:        20pt
Accent bar:        8pt top (title slides only)
Left border:       6pt (key message), 4pt (questions)
Button radius:     100px (pill shape)
```

## Workflow

1. **Parse the request** - Understand the topic, audience, and slide count
2. **Plan the deck** - Outline which slides to create (title, content, closing)
3. **Create output directory** - Put slides in `nimbalyst-local/slides/` or a descriptive subdirectory
4. **Create slides in parallel** - Spin up one sub-agent per slide using the Task tool (`subagent_type: "general-purpose"`). Each sub-agent receives: the slide number, filename, template to use, content for that slide, the full design tokens, navigation config (SLIDES array and CURRENT index), and the output directory path. Launch all sub-agents concurrently in a single message for maximum parallelism.
5. **Verify visually** - Use `mcp__nimbalyst-mcp__capture_editor_screenshot` to check each slide renders correctly

## Slide Templates

### TEMPLATE 1: Title Slide (Dark)

Center-aligned title on dark midnight blue background with top accent bar.

```html
<!DOCTYPE html>
<html>
<head>
<style>
html { background: #ffffff; }
body {
  width: 720pt; height: 405pt; margin: 0; padding: 0;
  background: #241D71; font-family: 'Euclid Circular A', 'Inter', Arial, sans-serif;
  display: flex; flex-direction: column; justify-content: center; align-items: center;
  text-align: center; position: relative;
}
.accent-bar {
  position: absolute; top: 0; left: 0; width: 100%; height: 8pt;
  background: #382DCF;
}
.badge {
  display: inline-block; font-size: 11pt; font-weight: 600;
  color: #B8B0F0; background: rgba(56, 45, 207, 0.25);
  padding: 5pt 16pt; border-radius: 100pt; margin-bottom: 20pt;
}
h1 {
  color: #FFFFFF; font-size: 42pt; font-weight: 700;
  line-height: 120%; margin: 0 40pt 16pt;
}
.subtitle {
  color: #B8B0F0; font-size: 18pt; font-weight: 400;
  line-height: 150%; margin: 0 60pt;
}
.author {
  color: #5571A3; font-size: 12pt; margin-top: 30pt;
}
</style>
</head>
<body>
<div class="accent-bar"></div>
<div class="badge">Category Label</div>
<h1>Presentation Title</h1>
<p class="subtitle">A concise subtitle describing the presentation</p>
<p class="author">Author Name</p>
</body>
</html>
```

### TEMPLATE 2: Section Divider

Full-width blue background for section breaks.

```html
<!DOCTYPE html>
<html>
<head>
<style>
html { background: #ffffff; }
body {
  width: 720pt; height: 405pt; margin: 0; padding: 0;
  background: #382DCF; font-family: 'Euclid Circular A', 'Inter', Arial, sans-serif;
  display: flex; flex-direction: column; justify-content: center; align-items: center;
  text-align: center;
}
.section-number {
  font-size: 14pt; font-weight: 600; color: #B8B0F0;
  margin-bottom: 12pt; letter-spacing: 1pt;
}
h1 {
  color: #FFFFFF; font-size: 36pt; font-weight: 700;
  line-height: 120%; margin: 0 60pt 12pt;
}
.subtitle {
  color: #B8B0F0; font-size: 16pt; font-weight: 400;
  line-height: 150%; margin: 0 80pt;
}
</style>
</head>
<body>
<div class="section-number">01</div>
<h1>Section Title</h1>
<p class="subtitle">Brief description of what this section covers</p>
</body>
</html>
```

### TEMPLATE 3: Header + Text Content

Blue header bar with body text content. The workhorse slide.

```html
<!DOCTYPE html>
<html>
<head>
<style>
html { background: #ffffff; }
body {
  width: 720pt; height: 405pt; margin: 0; padding: 0;
  background: #FFFFFF; font-family: 'Euclid Circular A', 'Inter', Arial, sans-serif;
  display: flex; flex-direction: column;
}
.header {
  background: #382DCF; padding: 25pt 40pt;
}
.header h1 {
  color: #FFFFFF; font-size: 28pt; margin: 0; font-weight: 700;
}
.header p {
  color: #B8B0F0; font-size: 14pt; margin: 5pt 0 0 0;
}
.content {
  padding: 25pt 40pt; flex: 1;
}
.key-message {
  background: #EEEDFA; border-left: 6pt solid #382DCF;
  padding: 16pt 20pt; margin: 0 0 20pt 0; border-radius: 0 8pt 8pt 0;
}
.key-message p {
  color: #241D71; font-size: 16pt; margin: 0; font-weight: 700;
  line-height: 140%;
}
.points {
  margin: 0; padding: 0 0 0 20pt;
}
.points li {
  color: #241D71; font-size: 14pt; margin: 0 0 10pt 0;
  line-height: 150%;
}
.points li strong {
  color: #382DCF;
}
</style>
</head>
<body>
<div class="header">
  <h1>Slide Title</h1>
  <p>2 minutes</p>
</div>
<div class="content">
  <div class="key-message">
    <p>The main insight or thesis for this slide</p>
  </div>
  <ul class="points">
    <li><strong>Key point one</strong> - supporting detail</li>
    <li><strong>Key point two</strong> - supporting detail</li>
    <li><strong>Key point three</strong> - supporting detail</li>
  </ul>
</div>
</body>
</html>
```

### TEMPLATE 4: Text + Image (Side by Side)

Two-column layout with text on left, image placeholder on right.

```html
<!DOCTYPE html>
<html>
<head>
<style>
html { background: #ffffff; }
body {
  width: 720pt; height: 405pt; margin: 0; padding: 0;
  background: #FFFFFF; font-family: 'Euclid Circular A', 'Inter', Arial, sans-serif;
  display: flex; flex-direction: column;
}
.header {
  background: #382DCF; padding: 25pt 40pt;
}
.header h1 {
  color: #FFFFFF; font-size: 28pt; margin: 0; font-weight: 700;
}
.header p {
  color: #B8B0F0; font-size: 14pt; margin: 5pt 0 0 0;
}
.content {
  padding: 20pt 40pt; flex: 1; display: flex; gap: 24pt;
}
.text-col {
  flex: 1; display: flex; flex-direction: column; justify-content: center;
}
.text-col p {
  color: #241D71; font-size: 13pt; line-height: 160%; margin: 0 0 12pt 0;
}
.text-col .highlight {
  color: #382DCF; font-weight: 700;
}
.image-col {
  flex: 1; display: flex; align-items: center; justify-content: center;
}
.image-placeholder {
  width: 100%; height: 100%;
  background: linear-gradient(180deg, #FFFFFF 0%, #EEEDFA 100%);
  border: 1px solid #E5E7EB; border-radius: 12pt;
  display: flex; flex-direction: column; align-items: center; justify-content: center;
  position: relative; overflow: hidden;
}
.image-placeholder::after {
  content: '';
  position: absolute; inset: 0;
  background-image: radial-gradient(circle, #9CA3AF 1px, transparent 1px);
  background-size: 20pt 20pt;
  opacity: 0.12;
}
.image-placeholder span {
  position: relative; z-index: 1;
  font-size: 12pt; color: #394F79; font-weight: 500;
}
.image-placeholder .icon {
  position: relative; z-index: 1;
  font-size: 28pt; color: #B8B0F0; margin-bottom: 8pt;
}
</style>
</head>
<body>
<div class="header">
  <h1>Slide Title</h1>
</div>
<div class="content">
  <div class="text-col">
    <p><span class="highlight">Key concept</span> with supporting explanation that gives context and detail.</p>
    <p>Additional paragraph with more detail about the topic being discussed.</p>
  </div>
  <div class="image-col">
    <div class="image-placeholder">
      <div class="icon">&#9634;</div>
      <span>Screenshot or diagram</span>
    </div>
  </div>
</div>
</body>
</html>
```

### TEMPLATE 5: Feature Cards (2-up or 3-up)

Cards for comparing features, showing demos, or grouping concepts.

```html
<!DOCTYPE html>
<html>
<head>
<style>
html { background: #ffffff; }
body {
  width: 720pt; height: 405pt; margin: 0; padding: 0;
  background: #FFFFFF; font-family: 'Euclid Circular A', 'Inter', Arial, sans-serif;
  display: flex; flex-direction: column;
}
.header {
  background: #382DCF; padding: 25pt 40pt;
}
.header h1 {
  color: #FFFFFF; font-size: 28pt; margin: 0; font-weight: 700;
}
.header p {
  color: #B8B0F0; font-size: 14pt; margin: 5pt 0 0 0;
}
.content {
  padding: 20pt 40pt; flex: 1;
}
.tagline {
  color: #394F79; font-size: 13pt; margin: 0 0 16pt 0; font-style: italic;
  line-height: 150%;
}
.cards {
  display: flex; gap: 16pt;
}
.card {
  flex: 1; background: #EEEDFA; border-radius: 8pt; padding: 16pt;
}
.card h3 {
  color: #382DCF; font-size: 14pt; font-weight: 700;
  margin: 0 0 10pt 0;
}
.card p {
  color: #241D71; font-size: 11pt; line-height: 150%; margin: 0 0 8pt 0;
}
.card ul {
  margin: 0; padding: 0 0 0 16pt;
}
.card li {
  color: #241D71; font-size: 11pt; margin: 0 0 5pt 0; line-height: 140%;
}
</style>
</head>
<body>
<div class="header">
  <h1>Slide Title</h1>
  <p>5 minutes</p>
</div>
<div class="content">
  <p class="tagline">An optional tagline describing the cards below.</p>
  <div class="cards">
    <div class="card">
      <h3>Card Title A</h3>
      <ul>
        <li>First point</li>
        <li>Second point</li>
        <li>Third point</li>
      </ul>
    </div>
    <div class="card">
      <h3>Card Title B</h3>
      <ul>
        <li>First point</li>
        <li>Second point</li>
        <li>Third point</li>
      </ul>
    </div>
    <div class="card">
      <h3>Card Title C</h3>
      <ul>
        <li>First point</li>
        <li>Second point</li>
        <li>Third point</li>
      </ul>
    </div>
  </div>
</div>
</body>
</html>
```

### TEMPLATE 6: Multi-Image / Screenshot Gallery

Multiple image placeholders in a grid. Good for showing UI screenshots, before/after, or product features.

```html
<!DOCTYPE html>
<html>
<head>
<style>
html { background: #ffffff; }
body {
  width: 720pt; height: 405pt; margin: 0; padding: 0;
  background: #FFFFFF; font-family: 'Euclid Circular A', 'Inter', Arial, sans-serif;
  display: flex; flex-direction: column;
}
.header {
  background: #382DCF; padding: 20pt 40pt;
}
.header h1 {
  color: #FFFFFF; font-size: 28pt; margin: 0; font-weight: 700;
}
.content {
  padding: 16pt 40pt; flex: 1; display: flex; gap: 16pt;
}
.image-frame {
  flex: 1; background: linear-gradient(180deg, #FFFFFF 0%, #EEEDFA 100%);
  border: 1px solid #E5E7EB; border-radius: 10pt;
  display: flex; flex-direction: column; overflow: hidden;
}
.image-area {
  flex: 1; display: flex; align-items: center; justify-content: center;
  position: relative;
}
.image-area::after {
  content: '';
  position: absolute; inset: 0;
  background-image: radial-gradient(circle, #9CA3AF 1px, transparent 1px);
  background-size: 18pt 18pt;
  opacity: 0.1;
}
.image-area span {
  position: relative; z-index: 1;
  font-size: 11pt; color: #394F79; font-weight: 500;
}
.image-caption {
  padding: 10pt 14pt;
  border-top: 1px solid #E5E7EB;
}
.image-caption h4 {
  color: #241D71; font-size: 11pt; font-weight: 700; margin: 0 0 3pt 0;
}
.image-caption p {
  color: #394F79; font-size: 9pt; margin: 0; line-height: 140%;
}
</style>
</head>
<body>
<div class="header">
  <h1>Slide Title</h1>
</div>
<div class="content">
  <div class="image-frame">
    <div class="image-area">
      <span>Screenshot 1</span>
    </div>
    <div class="image-caption">
      <h4>Feature Name</h4>
      <p>Brief description of what this shows</p>
    </div>
  </div>
  <div class="image-frame">
    <div class="image-area">
      <span>Screenshot 2</span>
    </div>
    <div class="image-caption">
      <h4>Feature Name</h4>
      <p>Brief description of what this shows</p>
    </div>
  </div>
</div>
</body>
</html>
```

### TEMPLATE 7: Two-Column Split (Content + Insight)

Left side has content/cards, right side has a dark insight/stat callout.

```html
<!DOCTYPE html>
<html>
<head>
<style>
html { background: #ffffff; }
body {
  width: 720pt; height: 405pt; margin: 0; padding: 0;
  background: #FFFFFF; font-family: 'Euclid Circular A', 'Inter', Arial, sans-serif;
  display: flex; flex-direction: column;
}
.header {
  background: #382DCF; padding: 20pt 40pt;
}
.header h1 {
  color: #FFFFFF; font-size: 28pt; margin: 0; font-weight: 700;
}
.header p {
  color: #B8B0F0; font-size: 14pt; margin: 5pt 0 0 0;
}
.content {
  padding: 16pt 40pt; flex: 1; display: flex; gap: 20pt;
}
.left-col { flex: 1; }
.tagline {
  color: #394F79; font-size: 12pt; margin: 0 0 12pt 0; font-style: italic;
}
.demo-section {
  background: #EEEDFA; border-radius: 8pt; padding: 12pt; margin: 0 0 10pt 0;
}
.demo-section h3 {
  color: #382DCF; font-size: 12pt; margin: 0 0 8pt 0; font-weight: 700;
}
.demo-section li {
  color: #241D71; font-size: 10pt; margin: 0 0 4pt 0; line-height: 140%;
}
.demo-section ul { margin: 0; padding: 0 0 0 16pt; }
.right-col { flex: 1; }
.key-point {
  background: #241D71; border-radius: 10pt; padding: 20pt; height: 100%;
  display: flex; flex-direction: column; justify-content: center;
}
.key-point .label {
  color: #B8B0F0; font-size: 10pt; font-weight: 700;
  text-transform: uppercase; letter-spacing: 0.5pt; margin: 0 0 10pt 0;
}
.key-point p {
  color: #FFFFFF; font-size: 14pt; margin: 0 0 10pt 0; line-height: 140%;
}
.key-point .stat {
  color: #382DCF; font-size: 36pt; font-weight: 700; margin: 12pt 0 0 0;
}
</style>
</head>
<body>
<div class="header">
  <h1>Slide Title</h1>
  <p>5 minutes</p>
</div>
<div class="content">
  <div class="left-col">
    <p class="tagline">Context or supporting tagline for the section.</p>
    <div class="demo-section">
      <h3>Topic A</h3>
      <ul>
        <li>Supporting detail</li>
        <li>Supporting detail</li>
      </ul>
    </div>
    <div class="demo-section">
      <h3>Topic B</h3>
      <ul>
        <li>Supporting detail</li>
        <li>Supporting detail</li>
      </ul>
    </div>
  </div>
  <div class="right-col">
    <div class="key-point">
      <div class="label">Key Insight</div>
      <p>The main takeaway or statistic for this section</p>
      <div class="stat">80%</div>
    </div>
  </div>
</div>
</body>
</html>
```

### TEMPLATE 8: Testimonials / Quotes

For social proof, customer quotes, or team feedback.

```html
<!DOCTYPE html>
<html>
<head>
<style>
html { background: #ffffff; }
body {
  width: 720pt; height: 405pt; margin: 0; padding: 0;
  background: linear-gradient(180deg, #FFFFFF 0%, #EEEDFA 100%);
  font-family: 'Euclid Circular A', 'Inter', Arial, sans-serif;
  display: flex; flex-direction: column;
  position: relative; overflow: hidden;
}
body::after {
  content: '';
  position: absolute; inset: 0;
  background-image: radial-gradient(circle, #9CA3AF 1px, transparent 1px);
  background-size: 24pt 24pt;
  opacity: 0.08;
}
.inner {
  position: relative; z-index: 1;
  padding: 30pt 40pt; flex: 1; display: flex; flex-direction: column;
}
.badge {
  display: inline-block; font-size: 10pt; font-weight: 600;
  color: #382DCF; background: #E0DEF5;
  padding: 4pt 14pt; border-radius: 100pt; margin-bottom: 16pt;
  align-self: center;
}
h1 {
  color: #241D71; font-size: 28pt; font-weight: 700;
  text-align: center; margin: 0 0 24pt 0;
}
.quotes {
  display: flex; gap: 16pt; flex: 1;
}
.quote-card {
  flex: 1; background: #FFFFFF; border: 1px solid #E5E7EB;
  border-radius: 10pt; padding: 16pt; display: flex; flex-direction: column;
}
.quote-card blockquote {
  color: #241D71; font-size: 11pt; line-height: 155%;
  margin: 0 0 12pt 0; font-style: italic; flex: 1;
}
.quote-card .attribution {
  border-top: 1px solid #E5E7EB; padding-top: 10pt;
}
.quote-card .name {
  color: #241D71; font-size: 10pt; font-weight: 600; margin: 0;
}
.quote-card .role {
  color: #394F79; font-size: 9pt; margin: 2pt 0 0 0;
}
</style>
</head>
<body>
<div class="inner">
  <div class="badge">Testimonials</div>
  <h1>Real Experiences, Real Results</h1>
  <div class="quotes">
    <div class="quote-card">
      <blockquote>"Quote text from the first person goes here. Keep it concise and impactful."</blockquote>
      <div class="attribution">
        <p class="name">Person Name</p>
        <p class="role">Title, Company</p>
      </div>
    </div>
    <div class="quote-card">
      <blockquote>"Quote text from the second person goes here. Keep it concise and impactful."</blockquote>
      <div class="attribution">
        <p class="name">Person Name</p>
        <p class="role">Title, Company</p>
      </div>
    </div>
    <div class="quote-card">
      <blockquote>"Quote text from the third person goes here. Keep it concise and impactful."</blockquote>
      <div class="attribution">
        <p class="name">Person Name</p>
        <p class="role">Title, Company</p>
      </div>
    </div>
  </div>
</div>
</body>
</html>
```

### TEMPLATE 9: Questions / Discussion

Vertically centered question items with blue left borders.

```html
<!DOCTYPE html>
<html>
<head>
<style>
html { background: #ffffff; }
body {
  width: 720pt; height: 405pt; margin: 0; padding: 0;
  background: #FFFFFF; font-family: 'Euclid Circular A', 'Inter', Arial, sans-serif;
  display: flex; flex-direction: column;
}
.header {
  background: #382DCF; padding: 25pt 40pt;
}
.header h1 {
  color: #FFFFFF; font-size: 28pt; margin: 0; font-weight: 700;
}
.content {
  padding: 30pt 40pt; flex: 1; display: flex; flex-direction: column;
  justify-content: center;
}
.question {
  color: #241D71; font-size: 18pt; margin: 0 0 22pt 0;
  padding: 0 0 0 24pt;
  border-left: 4pt solid #382DCF;
  line-height: 140%;
}
</style>
</head>
<body>
<div class="header">
  <h1>Questions for Discussion</h1>
</div>
<div class="content">
  <p class="question">First question or discussion topic?</p>
  <p class="question">Second question or discussion topic?</p>
  <p class="question">Third question or discussion topic?</p>
</div>
</body>
</html>
```

### TEMPLATE 10: Closing Slide (Dark)

Thank-you / closing slide matching the title slide style.

```html
<!DOCTYPE html>
<html>
<head>
<style>
html { background: #ffffff; }
body {
  width: 720pt; height: 405pt; margin: 0; padding: 0;
  background: #241D71; font-family: 'Euclid Circular A', 'Inter', Arial, sans-serif;
  display: flex; flex-direction: column; justify-content: center; align-items: center;
  text-align: center; position: relative;
}
.accent-bar {
  position: absolute; top: 0; left: 0; width: 100%; height: 8pt;
  background: #382DCF;
}
h1 {
  color: #FFFFFF; font-size: 36pt; font-weight: 700;
  margin: 0 0 12pt 0;
}
.subtitle {
  color: #B8B0F0; font-size: 16pt; margin: 0 0 30pt 0;
}
.cta {
  display: inline-block; background: #382DCF; color: #FFFFFF;
  font-size: 14pt; font-weight: 600; padding: 10pt 28pt;
  border-radius: 100pt;
}
.contact {
  color: #5571A3; font-size: 11pt; margin-top: 20pt;
}
</style>
</head>
<body>
<div class="accent-bar"></div>
<h1>Thank You</h1>
<p class="subtitle">Questions? Let's discuss.</p>
<div class="cta">Get Started</div>
<p class="contact">name@email.com</p>
</body>
</html>
```

## Rules

1. **One mockup file per slide** - Named `slideNN-descriptor.mockup.html` (e.g., `slide01-title.mockup.html`)
2. **Always use fixed dimensions** - `width: 720pt; height: 405pt` on body
3. **Always set `html { background: #ffffff; }`** - Ensures clean rendering
4. **Use pt units only** - Not px, rem, or em
5. **Use the brand font stack** - `'Euclid Circular A', 'Inter', Arial, sans-serif`
6. **Stay within the color palette** - Only use colors from the design tokens above
7. **Pill-shaped buttons** - `border-radius: 100pt`
8. **No external dependencies** - All styling inline, no CDN links
9. **Max 6-7 bullet points per slide** - Keep content scannable
10. **Minimum body text size** - 11pt for readability
11. **Always include slide navigation** - Every slide gets the nav footer with prev/next links and slide counter (see Slide Navigation section)

## File Organization

```
nimbalyst-local/slides/[deck-name]/
  slide01-title.mockup.html
  slide02-intro.mockup.html
  slide03-research.mockup.html
  ...
  slide09-closing.mockup.html
```

## Image Placeholders

When creating slides with image placeholders:
- Use the gradient + dot pattern treatment (white to blue tint with radial dot overlay)
- Label with descriptive text (e.g., "Product screenshot", "Architecture diagram")
- When the user provides actual images later, replace placeholders with `<img>` tags
- All slide files use the `.mockup.html` extension so they render in Nimbalyst's mockup viewer

## Slide Navigation

Every slide MUST include a navigation footer so users can click through the deck. Add the navigation CSS and HTML to every slide.

### Navigation CSS (add inside `<style>`)
```css
.slide-nav {
  position: absolute; bottom: 0; left: 0; right: 0;
  display: flex; justify-content: space-between; align-items: center;
  padding: 8pt 20pt; z-index: 10;
}
.slide-nav a {
  font-family: 'Euclid Circular A', 'Inter', Arial, sans-serif;
  font-size: 9pt; font-weight: 600; color: #6E95FF;
  text-decoration: none; padding: 4pt 12pt;
  border-radius: 100pt; border: 1pt solid rgba(110, 149, 255, 0.3);
  transition: background 0.15s;
}
.slide-nav a:hover { background: rgba(110, 149, 255, 0.12); }
.slide-nav .counter {
  font-size: 8pt; font-weight: 500; color: #5571A3;
}
/* For dark slides, override nav colors */
.slide-nav.dark a { color: #6E95FF; border-color: rgba(110, 149, 255, 0.3); }
.slide-nav.dark a:hover { background: rgba(110, 149, 255, 0.15); }
.slide-nav.dark .counter { color: #5571A3; }
```

### Navigation HTML (add before `</body>`)

Update the `SLIDES` array and `CURRENT` index for each slide in the deck.

```html
<nav class="slide-nav">
  <a id="prev" href="#">&larr; Prev</a>
  <span class="counter" id="counter">1 / 10</span>
  <a id="next" href="#">Next &rarr;</a>
</nav>
<script>
// List all slide filenames in order
var SLIDES = [
  'slide01-title.mockup.html',
  'slide02-topic.mockup.html',
  // ... add all slides
];
var CURRENT = 0; // 0-indexed position of THIS slide
document.getElementById('counter').textContent = (CURRENT + 1) + ' / ' + SLIDES.length;
var prev = document.getElementById('prev');
var next = document.getElementById('next');
if (CURRENT === 0) { prev.style.visibility = 'hidden'; }
else { prev.href = SLIDES[CURRENT - 1]; }
if (CURRENT === SLIDES.length - 1) { next.style.visibility = 'hidden'; }
else { next.href = SLIDES[CURRENT + 1]; }
</script>
```

For dark slides (title, section divider, closing), add the `dark` class: `<nav class="slide-nav dark">`.

**Important**: The body must have `position: relative` for the nav to position correctly (already the case in most templates; add it if missing).

## Adapting Templates

Templates are starting points. Adapt them:
- Combine elements from different templates
- Adjust card counts (2-up vs 3-up)
- Swap left/right columns
- Add or remove the time label
- Use the key-message callout on any content slide
- Use the dark key-point box wherever a stat needs emphasis
