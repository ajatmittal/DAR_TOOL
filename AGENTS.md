# Contributor Guidelines for DAR Tool

## Scope
These instructions apply to the entire repository unless a subdirectory defines its own `AGENTS.md` with more specific guidance.

## General Workflow
- Prefer incremental changes with descriptive commit messages.
- Keep the HTML document valid and accessible; run a quick manual verification in a browser when UI changes are made.
- Document any new manual testing steps or scripts in `TEST_RESULTS.md` when applicable.

## HTML & CSS
- Maintain semantic HTML structure (use proper heading levels and form landmarks).
- Inline styles should be avoided when practical; favor reusable classes inside the existing `<style>` block.
- Ensure any new components meet WCAG AA contrast guidelines and provide appropriate `aria-` attributes.

## JavaScript
- Keep all JavaScript inside the existing `<script>` section in `index.html` unless a refactor introduces modules.
- Avoid global namespace pollution—attach helpers to the existing app namespace when possible.
- Validate and sanitize all user-provided content before inserting it into the DOM.

## Testing & Verification
- When automated tests are added or executed, record the command and summary of results in `TEST_RESULTS.md`.
- For manual checks, briefly describe steps and outcomes in the same file.

## PR Message Expectations
- Summaries should focus on user-facing behavior changes or developer-facing tooling updates.
- Explicitly mention any testing commands executed, even when no automated tests exist.
