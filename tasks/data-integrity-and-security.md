# Data Integrity and Security Enhancements

## Objectives
- Prevent malicious or malformed content from being restored into the application state.
- Enforce strong validation for all persisted and user-entered data with actionable feedback.
- Modernise clipboard interactions to rely on secure, standards-based APIs.

## Tasks
- [ ] Integrate a trusted sanitisation library (e.g., DOMPurify) and run imported JSON or restored sessions through it before rendering.
- [ ] Define a strict data schema covering gist editors, verification text, numeric inputs, and dates.
- [ ] Adopt a validation library such as Zod or Yup to validate the schema on load, before save, and prior to DOCX generation.
- [ ] Implement user-facing error messages that clearly identify invalid fields and suggest corrections.
- [ ] Replace `document.execCommand` usage with the asynchronous Clipboard API for copy and paste flows.
- [ ] Provide paste handlers that normalise tables and preserve formatting while blocking unsafe markup.
- [ ] Add automated tests (unit or integration) covering sanitisation and schema validation edge cases.

## Acceptance Criteria
- Application rejects and reports invalid or unsafe session payloads without rendering arbitrary markup.
- All clipboard operations use the modern asynchronous API and maintain formatting fidelity.
- Validation errors are surfaced clearly to the user and prevent progression to DOCX generation until resolved.
