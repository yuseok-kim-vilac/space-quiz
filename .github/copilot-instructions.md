# Copilot instructions for this repository

## Repository shape

This repository is a small static web app: a single-page quiz experience rendered from `index.html`. There is no build pipeline, package manifest, or framework setup in the repository root.

The app is intentionally self-contained:

- HTML defines the quiz layout and visual styling.
- CSS includes the full UI theme and responsive behavior.
- JavaScript contains the quiz data (`Q` array), answer handling, scoring, keyboard interaction, and restart flow.
- The page uses a data-driven pattern: each question is an array entry containing the prompt, answer choices, correct index, and explanation.

## Build, test, and lint commands

No build, test, or lint scripts were found in this repository.

For local preview, either:

- open `index.html` directly in a browser, or
- serve the folder from the repo root:

```bash
cd C:\gh-copilot-session
python -m http.server 8000
```

Then open `http://localhost:8000` in a browser.

There are no unit tests or linters to run here; changes should be verified by manually checking the page behavior in a browser.

## Architecture and behavior

The page is organized around a few central pieces:

- `Q`: the complete quiz dataset, each item containing `[question, options, correctIndex, explanation]`
- `show()`: renders the current question and answer buttons
- `pick(index)`: handles answer selection, shows correct/incorrect feedback, updates score, and unlocks the next step
- `finish()`: calculates final score and shows the result screen with celebratory state
- `start()`: resets game state and restarts the quiz

Important UI behavior is implemented in-browser with direct DOM manipulation rather than a framework or component system. The state is simple and local to the page; there is no persistence or backend.

## Conventions specific to this codebase

- Keep the app as a single-file, no-build experience unless a new tooling setup is intentionally introduced.
- Prefer direct DOM APIs (`document.getElementById`, `createElement`, class toggling) over abstractions that would add framework overhead.
- Preserve the quiz's data-driven model: questions live in one array and are rendered from that source of truth.
- Maintain the existing visual design language: Korean UI labels, sci-fi HUD styling, and the theme system using CSS variables and `prefers-color-scheme`.
- Keyboard support is part of the UX; preserve the 1-4 answer shortcut and Enter/Tab behavior when editing the quiz interactions.
- When changing question content, keep the answer array format consistent: `question, choices, correctIndex, explanation`.

## Editing expectations

- Default to small, surgical changes in `index.html`.
- If you add functionality, keep it self-contained to the page logic instead of splitting into a multi-file app structure unless the repo grows beyond this static single-page pattern.
- If you change the visual design, respect the CSS variable-based palette and the dark-mode adaptation already present in the stylesheet.
- If you add new quiz questions, keep the text concise and the scoring logic untouched.
