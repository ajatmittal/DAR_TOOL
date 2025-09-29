# Architecture and Build System Enhancements

## Objectives
- Modularise the front-end codebase into dedicated HTML, CSS, and JavaScript source files managed through a modern build pipeline.
- Bundle third-party dependencies locally to eliminate CDN reliance and enable integrity checks.
- Introduce a reusable component abstraction to simplify repeated UI patterns and state management.

## Tasks
- [ ] Audit current inline HTML, CSS, and JavaScript within `index.html` and document required separations.
- [ ] Select and configure a bundler (e.g., Vite or Parcel) that supports ES modules or TypeScript while outputting a single distributable HTML bundle.
- [ ] Extract styles into standalone `.css` files and scripts into `.js`/`.ts` modules organised by feature area.
- [ ] Update build tooling to generate the existing single-file deliverable, ensuring paths and asset loading remain compatible with offline use.
- [ ] Install JSZip, FileSaver, and any other third-party packages locally and configure the bundler to include them in the build output with hash-based integrity metadata.
- [ ] Design and implement a lightweight component model (custom elements, Lit, or equivalent) for repeated UI sections such as para cards and revenue tables.
- [ ] Refactor existing DOM-manipulation logic to leverage the component abstraction, ensuring stateful features remain functional.
- [ ] Document new project structure, development workflow, and build commands in `README.md`.

## Acceptance Criteria
- Development workflow uses the selected build tool and produces an optimised single-page bundle.
- All third-party libraries load from local bundles with integrity guarantees.
- Core UI blocks reuse the new component abstraction without regressions in functionality.
