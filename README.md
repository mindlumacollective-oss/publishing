# Pulse & Co.

A single-page marketing/advertising agency landing page, built as one self-contained `index.html` file — HTML, inline `<style>` CSS, and inline `<script>` JS, no build step, no package manager, no test suite. The only external dependency is the Google Fonts CDN (Space Grotesk + Inter).

![Pulse & Co. screenshot](screenshot.png)

**Live site:** https://mindlumacollective-oss.github.io/publishing/

## Running locally

Open `index.html` directly in a browser — no build or dev server required.

## Structure notes

- CSS custom properties live in `:root`: a color palette (`--color-ink`, `--color-off-white`, `--color-accent`, `--color-grey`) and a spacing scale (`--space-1` through `--space-9`). Reuse these tokens rather than hardcoding new values.
- Section anchors — `#work`, `#testimonials`, `#contact` — are shared between the nav links and in-page CTAs; keep `id`s and hrefs in sync if sections change.
- All JS is wrapped in a single IIFE at the bottom of the file, organized into commented blocks: sticky nav, mobile hamburger, scroll-reveal (`IntersectionObserver`), hero stat counters, testimonial carousel dots, form validation/submit, and footer year.
- `prefers-reduced-motion` is respected throughout — the hero gradient animation and `.reveal` transitions are disabled in CSS, and counter/scroll animations are skipped in JS.
- The enquiry form (`#enquiry-form`) is client-side only: it validates in the browser and simulates submission with `setTimeout`. There is no backend.

## Deployment

Pushes to `main` deploy automatically to GitHub Pages via the Actions workflow in [.github/workflows/deploy.yml](.github/workflows/deploy.yml).
