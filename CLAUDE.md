# shirgoldbird.github.io

## About Shir

Product Manager at DeepL, former engineer. Builds API products for developers. The blog covers product thinking, developer experience, and side projects. Audience is developers and PMs.

## How to Work on This Repo

**Ask before guessing.** For anything requiring judgment (blog tone, design choices, content decisions), ask clarifying questions rather than assuming. Mechanical tasks (reformatting, fixing a CSS bug) are fine to just do.

**Always reread files before responding to feedback.** Shir edits files directly between messages (in a text editor, not in the conversation). The version in conversation context is often stale. Don't wait to be told "reread the file."

**Default to writing out to a file** when producing anything of meaningful length. This enables back-and-forth iteration. Don't keep drafts in conversation.

**Tone:** Direct but warm. Be concise. No filler, no preamble, no "Great question!" energy. Don't be overly formal or overly casual. Professional but human.

**At the end of each session, propose any updates to this CLAUDE.md** based on patterns, corrections, or preferences that emerged. Surface them explicitly so Shir can approve.

## Tech Stack

- **Static site generator:** Lektor (Python-based)
- **Styling:** SCSS compiled via lektor-scss plugin, output to `assets/css/theme.css`. **NEVER edit `assets/css/theme.css` directly — it is auto-generated. Always edit `assets/scss/theme.scss` instead.**
- **Fonts:** Google Fonts (Nunito for body, Shrikhand for display headings)
- **Icons:** FontAwesome (loaded via kit in layout.html)
- **Hosting:** GitHub Pages via `gh-pages` branch, custom domain `shirgoldberg.com`
- **Deployment:** GitHub Actions workflow in `.github/workflows/main.yml`

## Project Structure

- `content/` — All page content as `contents.lr` files (Lektor's format)
- `models/` — Lektor model definitions (`.ini` files defining fields per content type)
- `templates/` — Jinja2 templates, including `macros/child.html` (renders both index cards and full post views)
- `assets/scss/theme.scss` — All styles (single file)
- `website.lektorproject` — Project config, packages, markdown extensions

## Content Format

Lektor uses `.lr` files with `---` separated fields. Blog posts use the `blog-post` model:

```
_model: blog-post
---
title: Post Title
---
subtitle: Optional subtitle shown as summary on index
---
pub_date: YYYY-MM-DD
---
draft: true
---
ai_usage: none
---
body:

Markdown content here...
```

### ai_usage field values
- `none` — No AI used
- `edited` — Shir wrote first draft, AI edited
- `written` — AI wrote first draft, Shir edited

### Attachments
Files placed in a blog post's directory (e.g. `content/blog/my-post/image.png`) are served as attachments. Reference them in markdown with relative paths: `![alt](image.png)`. HTML files can be embedded via `<iframe src="demo.html">`.

**Important:** The template auto-renders attachment images only for `project` type pages. Blog posts handle images inline via markdown.

### Markdown extensions
Footnotes are enabled (`[^1]` inline, `[^1]: text` for definition). Requires colon + space in the definition.

## Key Gotchas

- `a:visited` styles can override nav link colors. Nav links explicitly set `a, a:visited` to prevent visited-link color leakage.
- The `a.blog-post` wrapper on index cards inherits link color on hover. The `all: unset` + explicit color rules on `.index.card` children prevent this.
- Blog post full-view background (`div.blog-post:not(.index)`) must use `div` selector to avoid matching the `<a class="blog-post">` wrappers on index cards.
- The AI gauge tooltip wrapper needs `display: block` to take vertical margin.
- Lektor's `position: fixed` elements in HTML attachments work relative to the iframe viewport, not the parent page. Modals in embedded demos should use `position: absolute` on a `position: relative` body.
- HTML files embedded in blog posts must have complete closing tags (`</script></body></html>`) or JS won't execute.

## SCSS Variables

```scss
$base-color: #5E3A98;      // Purple — headings, nav active
$header-color: #FFC75F;    // Gold/yellow — h3, accents
$link-color: #FF9671;      // Coral/orange — links
$font-color: #212529;      // Near-black — body text
$body-font-weight: 300;    // Light (Nunito)
```

## Writing Blog Posts for Shir

### Voice
Shir is a former engineer turned PM. The writing should be direct, warm, technically credible, and concise. Think "smart friend explaining something at a coffee shop" not "thought leader posting on LinkedIn."

### What I learned from Shir's edits to my drafts

**Cut the structure, keep the story.** My original draft had formal section headers like "Smart extensions:" with bullet points. Shir collapsed these into flowing prose. Bullet points are for reference docs, not blog posts.

**Don't over-explain the concept.** I wrote detailed explanations of every feature (representative sampling, confidence indicators, adaptive sizing) as separate items. Shir wove the important ones into the narrative and dropped the rest. The reader doesn't need an exhaustive feature list.

**Be more personal and less formal.** My draft: "This anxiety is everywhere in software." Shir's edit: "This anxiety is everywhere in software (or at least, I hope it's not just me)." The parenthetical makes it human. Shir adds asides, self-deprecating humor, and direct addresses to the reader.

**Use concrete scenarios, not abstractions.** My draft opened with a generic "you're closing a position." Shir's edit: "You just hired a candidate and are about to close the position in your ATS. You're hovering over the 'Archive all' button." More specific, more vivid.

**Shorter "What I Learned" sections.** My draft had bolded topic sentences with multi-sentence explanations. Shir used a numbered list where each item is 1-2 sentences max. The insight is the sentence, not a topic header followed by explanation.

**The subtitle IS the summary.** On the blog index, the subtitle replaces the auto-truncated body excerpt. Write subtitles as one-line summaries that tell the reader what the post is about, not as clever taglines.

**Disclaimers should be brief.** My original disclaimer was a full paragraph hedging about AI tooling changing. Shir's: one sentence in a blockquote.

**Avoid "generated" as a label.** The AI usage tiers are `none`, `edited`, `written`. Not `generated`. The word "generated" implies zero human involvement. "Written" (AI wrote the draft, human edited) is more honest about the actual workflow.

**Footnotes for tangents.** When there's a point that's interesting but interrupts the flow (like addressing common objections), use footnotes rather than inline parentheticals or separate sections.

### Things to avoid
- Em-dashes (use commas, periods, parentheses)
- Bullet point lists in blog prose (weave into text)
- "Great question!" energy or filler preamble
- Walls of text (3-4 line paragraphs max)
- Generic intros/conclusions
- Emoji in post content
- Over-structured formatting (bold headers for every point)
