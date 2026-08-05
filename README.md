# Mindluma Collective

A single-page landing page for an author-services / self-publishing collective, built as one self-contained `index.html` file — HTML, inline `<style>` CSS, and inline `<script>` JS, no build step, no package manager, no test suite. The only external dependency is the Google Fonts CDN (Fraunces + Inter). `robots.txt` and `sitemap.xml` sit alongside it at the repo root for basic technical SEO.

![Mindluma Collective screenshot](screenshot.png)

**Live site:** https://mindlumacollective-oss.github.io/publishing/

## Running locally

Open `index.html` directly in a browser — no build or dev server required. (If you're driving it with browser-automation tooling, serve it over `http://localhost` instead of `file://`, since some tooling blocks the `file:` protocol.)

## Structure notes

- CSS custom properties live in `:root`: a color palette (`--color-ink`, `--color-ink-soft`, `--color-paper`, `--color-white`, `--color-off-white`, `--color-lime`, `--color-lime-text`, `--color-lime-soft`, `--color-grey`) and a spacing scale (`--space-1` through `--space-9`). `--color-lime` (bright) is for dark backgrounds and icon chips; `--color-lime-text` (deep olive) is the accessible variant for text/links on light backgrounds. Reuse these tokens rather than hardcoding new values.
- Section anchors — `#services`, `#process`, `#roadmap`, `#testimonials`, `#contact` — are shared between the nav links and in-page CTAs; keep `id`s and hrefs in sync if sections change.
- All JS is wrapped in a single IIFE at the bottom of the file, organized into commented blocks: sticky nav, mobile hamburger, scroll-reveal (`IntersectionObserver`), hero stat counters, testimonial carousel dots, shared field-error helpers, the lead-magnet form, the enquiry form, the WhatsApp widget, and footer year.
- `prefers-reduced-motion` is respected throughout — the hero gradient, hero-shelf/book-mock float animations, `.reveal` transitions, and the WhatsApp toggle's pulse/panel animations are disabled in CSS, and counter/scroll animations are skipped in JS.
- There are two forms, both client-side only (validate in the browser, simulate submission with `setTimeout` — no backend): the lead-magnet opt-in (`#roadmap-form`) and the consultation enquiry (`#enquiry-form`).
- A floating WhatsApp widget (`#wa-widget`, bottom-right) opens a panel with suggested quick-reply prompts and a "Start Chat" CTA, all linking out to `wa.me` with a prefilled message — styled with the same ink/lime icon-chip pattern used elsewhere on the page (`.service-icon`, `.avatar`, `.step-badge`), not WhatsApp's default brand green.
- Contact details, the canonical/OG URLs, and the JSON-LD business info in `<head>` are realistic-looking placeholders — swap them for real values before launch.

## Deployment

Pushes to `main` deploy automatically to GitHub Pages via the Actions workflow in [.github/workflows/deploy.yml](.github/workflows/deploy.yml).
