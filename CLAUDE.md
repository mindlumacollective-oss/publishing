# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository overview

This repository is a single self-contained static page: [index.html](index.html) — a marketing/advertising agency landing page ("Pulse & Co."). There is no build step, no package manager, no bundler, and no test suite. All HTML, CSS (in a `<style>` block), and JavaScript (in a `<script>` block) live in that one file. The only external dependency is the Google Fonts CDN (Space Grotesk + Inter).

## Working with this file

- There is no build/lint/test command — the site is opened directly in a browser (`Start-Process index.html` on Windows, or double-click).
- Preserve the single-file structure: CSS stays inline in `<style>`, JS stays inline in `<script>`, no external frameworks or build tooling should be introduced unless explicitly requested.
- CSS uses custom properties defined in `:root` for the palette (`--color-ink`, `--color-off-white`, `--color-accent`, `--color-grey`) and a spacing scale (`--space-1` through `--space-9`). Reuse these tokens rather than hardcoding new values.
- Section anchors (`#work`, `#testimonials`, `#contact`) are used by both the nav links and in-page CTAs — keep `id`s and hrefs in sync if sections are renamed or reordered.
- The JS is wrapped in a single IIFE at the bottom of the file, organized into clearly commented blocks (sticky nav, mobile hamburger, scroll-reveal via `IntersectionObserver`, hero stat counters, testimonial carousel dots, form validation/submit, footer year). Keep new behavior in this same pattern rather than adding separate script tags.
- `prefers-reduced-motion` is respected in both CSS (media query disabling the hero gradient animation and `.reveal` transitions) and JS (skipping counter/scroll animations) — any new animation should follow the same guard.
- The enquiry form (`#enquiry-form`) does client-side-only validation and simulates submission with `setTimeout`; there is no backend. The success panel is built with DOM APIs (`createElement`/`textContent`), not `innerHTML` string interpolation, since form values are user-supplied — keep that pattern for any similar dynamic content to avoid introducing an XSS vector.
- No `localStorage`/`sessionStorage` is used; don't introduce it without checking with the user first, per the original build constraints for this page.
