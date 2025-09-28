# Enhancement Plan for DAR_TOOL

## 1. Architecture and Build System
- **Modularise the front end** by splitting the monolithic `index.html` into separate HTML, CSS, and JavaScript bundles. Adopt a build tool such as Vite or Parcel so you can author ES modules (or TypeScript) and ship a minified single-file build for deployment. This removes the current web of globals and makes stateful features like autosave and revenue calculators easier to reason about.
- **Bundle third-party libraries** (JSZip, FileSaver) locally through the build step so the generator no longer relies on live CDNs. This also lets you pin hashes for subresource integrity and makes the tool usable on restricted networks.
- **Introduce a component abstraction** (lightweight state containers, Lit, or even Web Components) for repeated UI blocks such as para cards and revenue tables. This will reduce duplication and make it easier to evolve the summary layout.

## 2. Data Integrity and Security
- **Sanitise persisted rich text** when restoring sessions or importing JSON so that gist/verification editors cannot inject arbitrary markup into the DOM. A small DOMPurify pass combined with a strict schema guards against hostile session files.
- **Validate session payloads and form state** using a declarative schema (e.g., Zod or Yup). Reject invalid numeric strings, enforce date formats, and surface actionable error messages before the DOCX merge step.
- **Replace deprecated clipboard APIs** (`document.execCommand`) with the asynchronous Clipboard API. Provide paste handlers that normalise tables and preserve formatting without relying on legacy browser behaviour.

## 3. User Experience and Accessibility
- **Add semantic validation feedback** by marking required fields, surfacing error summaries above the form, and pairing colour cues with text/aria hints. This improves accessibility compared to the current colour-only highlights.
- **Streamline large forms** with collapsible sections, progress indicators, and a “pre-flight” checklist that blocks generation until core data is present. Combine this with autosave insights so reviewers can quickly spot missing revenue data.
- **Expose keyboard and screen-reader affordances** for para reordering, risk-table editing, and toast notifications (aria-live regions, focus management) to meet WCAG expectations for government tools.

## 4. Document Templating and Extensibility
- **Externalise the DOCX template** so admins can upload new versions or switch between templates without editing an embedded Base64 blob. A template manager with metadata (version, checksum, page settings) reduces risk during regulatory updates.
- **Codify the WordprocessingML mappers** into reusable utilities with tests, and document the mapping between each form field and the target XML nodes. This makes future template tweaks safer and opens the door for multi-language variants.

## 5. Quality Assurance and Tooling
- **Automate calculations** with unit tests that cover detection/recovery totals, nested table shaping, and dashboard aggregations. Pair this with Playwright/Cypress smoke tests to ensure DOCX generation remains stable across refactors.
- **Add diagnostics and logging hooks** (structured console logs, downloadable debug reports) so audit teams can share reproducible traces when generation fails.
- **Wire up continuous integration** to lint, type-check, run tests, and build the distributable artifact on every change, guaranteeing that the packaged single-page app is always in sync with source modules.
