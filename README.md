# Code Compare

Client-side code and text diff tool for comparing files in the browser with editor-grade controls and static deployment support.

## Live Demo
Expected GitHub Pages path:
`https://sbdkim.github.io/code_compare/`

## Key Features
- Side-by-side and unified diff views
- Dual CodeMirror editors
- Myers and patience-lite diff strategies
- Line, word, and character-level highlighting
- Language detection and syntax highlighting for common code formats
- Filters for whitespace, case, and trimmed-line comparison
- Local autosave and import/copy utilities

## Tech Stack
- React 19
- TypeScript
- Vite
- CodeMirror 6
- `diff`
- Vitest and Testing Library

## Setup / Run Locally
```bash
npm install
npm run dev
```

## Tests
```bash
npm test
```

## Deployment Notes
- This project is configured for static hosting and GitHub Pages project-site deployment.
- The current Vite base path targets `/code_compare/`, so keep that aligned with the repository name when publishing.

## Architecture
- The diff domain model lives in `src/types/diff.ts`.
- The app separates comparison logic from rendering so different view modes can reuse the same normalized diff document.
- The browser stores editor state, language, comparison settings, and theme in `localStorage`.

## Privacy / Notes
- All comparison happens locally in the browser.
- No code or text content is sent to a backend service.
