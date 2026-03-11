# Code Compare

A client-side code and text comparison tool built with React, TypeScript, Vite, and CodeMirror. The project is designed for static deployment on GitHub Pages and focuses on a clean Diffchecker-style workflow for comparing source code and plain text.

## Features

- Side-by-side and unified diff views
- Dual code editors powered by CodeMirror 6
- Myers and patience-lite comparison strategies
- Line, word, and character-level highlighting
- Syntax highlighting with automatic language detection
- Comparison filters:
  - Ignore whitespace
  - Ignore case
  - Trim lines
- Diff summary with next/previous change navigation
- Supported file import for common text and code formats
- Copy left pane, right pane, or unified diff output
- Local autosave with `localStorage`
- Light and dark themes
- GitHub Pages-ready build configuration

## Tech Stack

- React 19
- TypeScript
- Vite
- Vitest + Testing Library
- CodeMirror 6
- `diff` for text comparison primitives

## Project Goals

This project aims to provide a practical code comparison tool that works entirely in the browser without a backend. The current version prioritizes core comparison quality, usability, and deployability over backend features such as shared links or persistent server storage.

## Current Scope

Included in this version:

- Static hosting support
- Text/code comparison
- Syntax highlighting
- Local persistence
- File import for supported plain text formats
- Theme switching

Not included in this version:

- `.docx` or `.pdf` extraction
- URL fetching/scraping
- Export to PDF
- Shareable backend-generated links
- Multi-user collaboration

## Supported Import Types

The app currently supports importing these file extensions:

`txt`, `js`, `ts`, `tsx`, `jsx`, `py`, `json`, `html`, `css`, `md`, `xml`, `yml`, `yaml`, `java`, `c`, `cpp`, `cs`, `go`, `rs`, `php`, `sql`

## Diff Engine Overview

The comparison logic is organized around a small typed domain model in `src/types/diff.ts`.

Core concepts:

- `ComparisonOptions`
  - Comparison settings such as whitespace handling, granularity, view mode, and selected strategy
- `DiffStrategy`
  - Strategy interface used to generate a normalized diff document
- `DiffDocument`
  - Canonical output format used by all renderers and utilities
- `DiffBlock`
  - A grouped block of diff rows
- `DiffLine`
  - An aligned diff row with left/right line numbers, text, and token metadata
- `DiffToken`
  - Intraline highlight units for context, additions, and deletions

### Strategies

- `myers`
  - Uses array-based diffing for standard text comparison
- `patience-lite`
  - Uses unique-line anchors first to improve readability for code-like content, then falls back to Myers-style diffing inside unmatched regions

### Normalization

Before comparison, lines can be normalized according to active options:

- Remove all whitespace differences
- Trim leading/trailing whitespace
- Compare case-insensitively

This keeps rendering separate from comparison rules and makes it easier to extend later.

## UI Overview

The application is structured as a simple workbench:

- Toolbar
  - Language selection
  - Diff strategy
  - Granularity controls
  - View mode
  - Filters
  - Import/copy/swap/clear/theme actions
- Editor workspace
  - Original input
  - Modified input
- Summary bar
  - Additions, deletions, changes
  - Next/previous navigation
- Diff result panel
  - Side-by-side or unified rendering using the same normalized diff model

## Persistence

The app stores the following in `localStorage`:

- Left editor content
- Right editor content
- Comparison settings
- Selected language
- Theme

This is local-only persistence. No content is sent to a server.

## Getting Started

### Prerequisites

- Node.js 24 or newer
- npm 11 or newer

### Install

```bash
npm install
```

### Start the development server

```bash
npm run dev
```

### Run tests

```bash
npm test
```

### Create a production build

```bash
npm run build
```

## Deployment

This project is configured for GitHub Pages project-site deployment under:

`/code_compare/`

That base path is defined in `vite.config.ts`.

### Typical GitHub Pages flow

1. Build the app:

```bash
npm run build
```

2. Publish the `dist` directory using your preferred Pages workflow:

- GitHub Actions
- `gh-pages`
- manual Pages publishing

If you change the repository name or deploy to a custom domain root, update the Vite `base` setting accordingly.

## Testing

The project currently includes tests for:

- Diff engine behavior
- App-level user interactions
- Persistence and theme toggling
- Import flow
- Copy workflow

The test suite uses:

- Vitest
- Testing Library
- jsdom

## Repository Structure

```text
src/
  components/   UI building blocks
  hooks/        React hooks
  lib/          Diff engine, utilities, persistence, imports
  test/         Test setup
  types/        Shared domain types
```

## Design Notes

The UI intentionally avoids decorative dashboard styling and instead uses a restrained editor-like layout:

- low-radius surfaces
- subtle borders
- neutral palette
- practical spacing
- mobile-friendly stacking behavior

## Known Limitations

- The production build currently includes a large editor-related chunk due to language/editor dependencies.
- The app is optimized for typical code-review sized inputs, not extremely large files.
- File import is limited to browser-readable plain text formats.

## Future Improvements

- Better code splitting for editor/language packages
- Optional worker-based diff processing for larger documents
- Rich document import support
- Export formats
- Sharable URLs for lightweight sessions
- Better language detection heuristics

## License

No license has been added yet. If you plan to make this project public for reuse, consider adding a license file.
