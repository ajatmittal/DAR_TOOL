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

## 6. Intelligence, Collaboration, and Automation
- **Embed contextual AI assistance** that can summarise drafted paras, propose remediation actions, or flag inconsistencies between risk statements and quantitative data. Running prompts against a secure, self-hosted LLM (or an API gateway that redacts sensitive content) would give analysts smarter starting points without leaking regulated information.
- **Layer in scenario modelling** that lets reviewers explore “what-if” adjustments to detection, recovery, and revenue forecasts. A reactive calculation engine paired with charting (e.g., Observable Plot embedded offline) can highlight downstream impacts of remedial actions.
- **Introduce collaborative review workflows**: allow analysts to request approvals, assign follow-up tasks, and track status within the tool. Lightweight real-time sync via WebRTC data channels or a hosted SignalR/Pusher service would let geographically distributed teams iterate together without emailing JSON files back and forth.
- **Automate downstream publishing** by integrating with document management systems (e.g., SharePoint, Alfresco). A secured connector could push final DOCX exports and metadata (finding owner, severity, completion date) directly into retention repositories.

## 7. Backend Data Capture and Telemetry Strategy
- **Session event streaming**: instrument the UI to emit structured events (field edits, para additions, generation attempts) to a telemetry pipeline. A background `navigator.sendBeacon` or `fetch` to a hardened ingestion endpoint (Cloudflare Workers, Azure Function) can persist audit-friendly timelines without slowing the UI.
- **Form-state snapshots**: provide an opt-in sync that periodically serialises the DAR payload and posts it to a backend document store (Cosmos DB, DynamoDB, PostgreSQL JSONB). Pair the uploads with encryption-at-rest and per-tenant keys so sensitive fraud data remains compliant.
- **Metrics aggregation**: process captured events through a stream processor (Kafka Streams, Kinesis Analytics) to derive KPIs—average completion time, common validation failures, risk categorisation trends—and expose them via a secure analytics dashboard for programme leadership.
- **Template/version analytics**: log which DOCX templates and remediation playbooks are used during generation. This enables A/B comparisons of template efficacy and early detection of outdated guidance.
- **Compliance and retention controls**: add backend policies that honour data retention schedules, redact personally identifiable information before long-term storage, and surface access logs for audits. Provide administrators with tooling to export or purge captured sessions on demand.
