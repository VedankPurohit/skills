---
name: field-guide
description: "Field-guide HTML: turn a product, system, research document, plan, or dense explanation into a polished self-contained visual guide. Use when the user asks for guide.html, a visual explainer, an interactive document, a microsite that teaches something, or wants a text wall replaced by an understandable web page."
---

# Field Guide

Build a **field guide**: a self-contained HTML document that makes a complex subject graspable through hierarchy, visual metaphor, and one useful interaction. The artifact is documentation people can _feel_, not a landing page that merely advertises.

## 1. Read for the hidden product

Read the source material and surrounding project before choosing a layout. Extract:

- the one sentence the reader should remember tomorrow;
- the unusual mechanism that distinguishes this subject;
- the actors, objects, boundaries, and state changes;
- what the reader can try now;
- what is working, deferred, or uncertain.

Do not let the source document's heading structure dictate the page. Reconstruct the explanation around the reader's questions.

**Complete when:** one thesis, one distinguishing mechanism, and the reader's testing path are explicit.

## 2. Choose a concept, not a style preset

Find a visual world already latent in the subject: registry, field manual, control room, atlas, workshop, specimen cabinet, transit system, case file, or another content-native metaphor. Let it determine typography, marks, borders, labels, motion, and interaction.

Write a tiny art-direction brief before coding:

```text
Metaphor:
Emotional register:
Ink / paper / signal colors:
Display type / reading type / code type:
Signature visual:
Signature interaction:
```

Avoid generic AI-SaaS defaults: interchangeable cards, gratuitous gradients, glass panels, purple neon, fake metrics, feature-icon grids, and decoration unrelated to meaning. Beauty should come from conviction and coherence.

**Complete when:** removing the product name would still leave a visual language specific to the subject.

## 3. Storyboard understanding

Arrange the page as a teaching sequence. Adapt this spine rather than copying it mechanically:

1. **Promise** — the human outcome in one strong sentence.
2. **Mechanism** — a diagram of the system's unusual idea.
3. **Mental model** — three to five rules that explain the rest.
4. **Proof** — an interaction that lets the reader change state or inspect a boundary.
5. **Practice** — exact ways to test the real thing.
6. **Matrix or lifecycle** — make permissions, mappings, or transitions comparable.
7. **Boundaries** — distinguish working reality from future ambition.
8. **Vocabulary** — define only terms the reader must retain.

Prefer diagrams, matrices, timelines, and before/after states when relationships matter. Prefer prose when the idea is linear. Every section should answer a different question.

Set an information budget before coding. Choose the few sections and examples that carry the thesis; do not include every item in the spine merely because it is available. Put secondary detail into compact reference forms only when a reader will use it. A field guide should feel complete without feeling exhaustive.

**Complete when:** a reader can skim headings and reconstruct the whole argument.

## 4. Build one explanatory object

Give the page one memorable visual model and one interaction that exposes the underlying rules. Examples:

- move an item across a boundary and show which copies survive;
- switch personas and reveal exactly what each can see;
- step through a lifecycle and update the state diagram;
- adjust a small input and show the consequence immediately.

The interaction must teach something that static prose would make harder to understand. Keep the full state visible when that helps the reader compare it with the permitted or derived view. Label results in domain language, not generic success copy.

Do not add interaction merely to make the page feel dynamic.

Make every selectable state produce an observable, domain-specific consequence. Avoid controls whose initially selected or first reachable state is a no-op; a reader testing by keyboard should quickly see both the visual change and a textual explanation of what changed.

**Complete when:** using the interaction gives the reader evidence for the page's thesis.

## 5. Implement as a durable document

Unless the user requests a framework, create one portable `.html` file with semantic HTML, inline CSS, and minimal inline JavaScript. It should open from disk and work when served locally. Avoid external dependencies unless they materially improve the result and network access is part of the brief.

Use:

- a restrained palette with named semantic roles;
- fluid type via `clamp()` and a deliberate measure for reading;
- CSS grid or flex layouts that collapse cleanly;
- real buttons, links, tabs, tables, and headings;
- visible focus states and keyboard-operable interactions;
- `prefers-reduced-motion` for nonessential animation;
- copy buttons for commands or prompts when useful;
- meaningful empty, active, allowed, and denied states.

Keep content in the HTML rather than generating it from a large opaque script. Use JavaScript for state changes, not for rebuilding the entire document.

**Complete when:** the file has no required build step, its primary content remains readable without JavaScript, and every control has a clear purpose.

## 6. Edit like an exhibition

Inspect the full page and remove anything that does not clarify, orient, or reward attention. Tighten copy until labels can be understood at a glance. Vary scale and density so the document has rhythm: one commanding opening, quieter reading passages, compact evidence, and deliberate pauses.

Check especially for:

- repeated explanations;
- vague headings such as “Features” or “Overview”;
- visual components reused where a different form would explain better;
- long paragraphs that should become a diagram or comparison;
- ornamental UI that competes with the teaching path;
- claims that outrun what the reader can actually test.

Run a compression pass after the page is complete: remove the weakest section, merge repeated reference material, and shorten labels before shrinking type. Protect readable support text and contrast; density should come from hierarchy and editing, not tiny captions or faint ink.

**Complete when:** every visible element earns its space and the page feels authored rather than assembled.

## 7. Render, test, and leave it open

Serve the file when the project has a local server; otherwise open it directly. Use browser control for a render-and-fix pass:

1. Inspect the desktop viewport visually.
2. Exercise every interactive state and verify the resulting content.
3. Test near `390 × 844`; confirm there is no horizontal overflow.
4. Inspect a full-page phone screenshot for visible clipping or awkward reflow even when `scrollWidth` reports no overflow. Check long labels, tables, code blocks, sticky elements, and navigation at narrow widths.
5. Check the console for errors and warnings.
6. Verify keyboard focus, reduced-motion behavior, links, copy controls, text contrast, and the smallest supporting text at both viewports.
7. Fix defects and repeat the relevant checks.

When possible, leave the finished page open as the deliverable and provide both the live URL and absolute file path.

**Complete when:** desktop and phone layouts are legible, every interaction has been exercised, horizontal overflow is absent, and the console is clean.

## Quality bar

The document succeeds only if a new reader can:

- state the central idea after one minute;
- explain the distinguishing mechanism after using the interaction;
- find an exact path to test or apply the subject;
- separate current capability from aspiration;
- remember the visual metaphor after closing the page.

If any answer is no, return to the earliest step that failed. Do not polish around a missing mental model.
