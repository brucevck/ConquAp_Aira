# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repo is

A single self-contained static HTML file (`index.html`) — a scrollytelling presentation titled "Payment Integrity — De la limpieza manual a la contención inteligente." It tells the story of two internal automation initiatives at Pacífico Seguros (Costos y Optimización team):

- **ConquApp** — a Power Apps + SharePoint tool that validates concurrent-audit medical claim data at the point of entry (replacing manual Excel cleanup).
- **AIRA** (Agente de Ingreso y Registro de Alertas) — a Copilot Studio / AI Builder / Power Automate agent that ingests unstructured PDF/email case derivations and registers them into the same trazability flow ConquApp established.

There is no build system, package manager, framework, or test suite. Everything — HTML, CSS, and JS — lives inline in `index.html`. Content is in Spanish.

## Working with this file

There are no build/lint/test commands — this is a plain HTML file opened directly in a browser. To preview changes, open `index.html` in a browser (or use a simple static server if live-reload is desired).

Since the whole site is one file, prefer targeted edits over rewrites. When editing:
- CSS custom properties are defined once in `:root` (colors, fonts, `--rail-w`) — reuse these tokens rather than hardcoding new colors.
- Content is organized as sequential `<section class="chapter" id="chN">` blocks ("chapters"), each with a `data-label` attribute used to auto-generate the side rail nav dot and tooltip. Adding/removing/reordering a `<section class="chapter">` automatically updates the rail nav and chapter counter — no other JS changes needed.
- Chapters alternate visual treatments via modifier classes: `.chapter--dark` (magenta/purple gradient, white text) and `.chapter--tint` (light tint background); default is plain white.

## Structure of index.html

1. **`<style>`** — all CSS, organized in comment-delimited sections per chapter/component (rail nav, hero, chapter 01–11 components, responsive breakpoint at 900px at the bottom).
2. **`<body>`** — a fixed left-side `.rail` nav (auto-populated by JS from chapters), followed by `<main>` containing eleven `.chapter` sections telling the story in order (encargo → diagnóstico → números ocultos → solución/ConquApp → impacto → bridge → nace AIRA → demo → stack → resultados piloto → cierre).
3. **`<script>`** — three independent behaviors:
   - **Rail nav**: builds nav dots from `.chapter` elements, tracks scroll position to highlight the active dot and update the progress bar/counter.
   - **Chapter 08 demo autoplay**: a 6-step animated pipeline (`.demo-node` / `.demo-panel` pairs matched by `data-i` index) that auto-plays once when scrolled into view (via `IntersectionObserver`) and can be replayed via the "Reproducir de nuevo" button. Step timing is controlled by `STAGE_MS` (2200ms).
   - **Reveal-on-scroll**: simple opacity reveal for chapters via `IntersectionObserver` (currently a no-op visual effect since opacity is set to 1 immediately).

External dependencies are all CDN-loaded: Google Fonts (Bricolage Grotesque, Public Sans, JetBrains Mono) and Font Awesome 6.5.1 icons. No local assets.

Note: Chapter 10 ("Resultados piloto") contains a `.caveat` note flagging its stats as illustrative placeholders pending the official pilot report — check whether real figures should replace them before treating that section as final.
