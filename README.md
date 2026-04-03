# T(h)reehouse +EC Demonstrator

This Markdown file is the authoritative source for the demonstrator page in `index.html`.

Current build method: manual rendering from this Markdown source, the local SVG assets, and `tokens.css`.

## Intent

The demonstrator translates the corporate design blueprint into a live web page that can be inspected in use.

It is meant to feel like a specimen sheet rather than a marketing landing page: restrained, legible, and explicit about what is maintained versus what remains open to correction.

## What the page demonstrates

### Maintained reference

Reference elements use the `--sea` role sparingly for labels, links, and points of orientation rather than decorative fills.

### Readable structure

Body copy stays in Crimson Pro, labels and navigation stay in IBM Plex Mono, and the content measure remains within the blueprint's stated reading width.

### Correction gate

Signal red appears only where the design system marks a correction lens or repair channel. It is present, but not dominant.

## Component patterns

The page demonstrates:

- a lockup using the existing emblem and full wordmark
- a compact 32px header lockup
- a mobile header that auto-hides on downward scroll and returns on upward scroll
- the section rule
- a layer stack with a gate row
- a research callout
- a responsive table with a stacked mobile fallback
- accessible navigation with a skip link and a keyboard-safe menu toggle

## Table sample

The responsive table in `index.html` shows source-level compliance with the blueprint's table rules:

- mono headers and serif body cells
- open edges with horizontal separators only
- preserved header context on mobile through `data-label`
- keyboard-focusable scroll wrapper

## Status

Built against the current blueprint and token set already present in this repository.
