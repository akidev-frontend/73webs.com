# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

Static marketing site for 73webs (Spanish, `es`), a one-person web-building service for small businesses/PYMEs. No build system, no package manager, no framework — plain HTML/CSS/JS served as-is. No test suite, no lint config, no CI.

## Working directory vs. real repo

**This directory is a staging/edit copy, not the git repo.** The actual git repository lives at `C:\Users\micro\Documents\GitHub\73webs.com`. `.claude/settings.local.json` shows the sync pattern: after editing files here, they get copied over with `cp -rf` per top-level item (`404.html`, `aviso-legal.html`, `index.html`, `politica-cookies.html`, `politica-privacidad.html`, `robots.txt`, `sitemap.xml`, `skills-lock.json`, `terminos-condiciones.html`, `clientes/`, `css/`, `fonts/`, `img/`) into the GitHub folder. When a task is meant to ship, ask whether to sync to the GitHub copy rather than assuming it happens automatically.

## Structure

- `index.html` — the entire landing page (~2300 lines). All CSS is inlined in a `<style>` block in `<head>`; there is no separate stylesheet in active use for this page.
- `css/style.css` — exists but is minimal/legacy (76 lines); the live styling is the inline `<style>` in `index.html`.
- `js/main.js` — empty stub (`DOMContentLoaded` listener with no logic yet).
- `aviso-legal.html`, `politica-cookies.html`, `politica-privacidad.html`, `terminos-condiciones.html` — legal pages (aviso legal, cookies policy, privacy policy, T&C), each a standalone HTML document following the same head/meta pattern as `index.html`.
- `404.html` — error page.
- `clientes/` — currently empty, reserved for client-specific pages.
- `robots.txt`, `sitemap.xml` — SEO plumbing; sitemap lists the root + four legal pages (not 404 or clientes).

## Page architecture (index.html)

Single-page layout built from stacked `<section>` blocks, in order: `hero` → `pain` (`#pain`) → `build` → `solution` (`#solucion`) → `features` (`#incluye`) → `objection` (`#objecion`) → `final` (`#final`). Copy follows a consistent narrative: pain of relying on rented platforms (Instagram/social) → the fix (own website + WhatsApp contact + Google Business listing) → objection handling → CTA.

Design tokens are CSS custom properties on `:root` in the inline `<style>` block — two semantic color pairs are used throughout:
- `--cold*` tones for "rented platform" (social media dependency) moments
- `--gold*` tones for "your home" (owning your own site) moments

Fonts: Plus Jakarta Sans (display), Asap (body), JetBrains Mono (mono), loaded from Google Fonts.

## Conventions to follow when editing

- Keep new page-specific styles inline in the page's own `<style>` block, matching the existing pattern, rather than introducing a new shared stylesheet unless asked.
- Keep the `--cold` / `--gold` semantic meaning intact when touching color usage (rented-platform vs. own-site framing).
- All copy is in Spanish (`es`, `es_ES` locale) — keep new content in Spanish unless told otherwise.
- Legal pages and `sitemap.xml` should stay in sync: if a new page is added under the root, add it to `sitemap.xml`; `clientes/` and `404.html` are intentionally excluded from the sitemap.
