# DAR_TOOL Agent Guidelines

## Scope
These instructions apply to the entire repository. Create more specific `AGENTS.md` files in subdirectories if a change requires additional or overriding guidance.

## Project context
- This project is a single-page web application delivered entirely through `index.html` with inline CSS and JavaScript.
- The tool is meant to run locally in modern Chromium/Firefox browsers without a build step. Avoid introducing frameworks, bundlers, or server-side dependencies unless explicitly requested.

## Coding conventions
- Preserve the existing formatting style in `index.html`: two-space indentation, lowercase HTML tag names, and kebab-case CSS class names.
- Keep CSS, HTML, and JavaScript logically grouped (styles first, markup second, scripts last). When adding new logic, favor well-named helper functions rather than large anonymous blocks.
- Prefer semantic HTML elements when expanding the UI. Ensure that newly added interactive controls are keyboard accessible and labelled.

## Documentation expectations
- Update `README.md` when you add or change user-facing functionality.
- Inline comments should explain non-obvious calculations or DOM manipulations; avoid redundant comments for self-explanatory code.

## Testing and validation
- There is no automated test suite. For any feature change, describe the manual steps you executed to verify the behavior in your final report (e.g., “manually generated a DAR with sample data”).
- If you add scripts or commands for verification, document how to run them in `README.md`.

## PR / change notes
- Summaries should highlight user-visible effects first, followed by any notable refactors or internal changes.
- If a change might impact data persistence or the generated DOCX template, call that out explicitly in both the PR message and final response.
