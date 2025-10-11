# DAR_TOOL

## Overview
DAR_TOOL is a single-page web application that helps CGST audit teams prepare Draft Audit Reports (DARs). The tool captures all inputs that appear in the department's Target.docx template, summarises audit paras, and generates a fully formatted DAR as a downloadable DOCX file directly in the browser. 【F:index.html†L188-L603】【F:index.html†L3843-L3899】

## Key features
- **Guided Part-I data entry** – Collects unit metadata such as registration number, audit period, visit dates, circle/group assignments, and officer details through structured form controls; every Part-I field except A.R. No. must now be filled. 【F:index.html†L236-L420】
- **Fixed navigation rail** – Locks section shortcuts in a left rail while the right pane scrolls independently, reveals only the selected section, and moves focus to its heading for keyboard users. 【F:index.html†L188-L214】【F:index.html†L640-L706】
- **Detection and recovery calculators** – Mirrors the nested tables in Table 1 of Target.docx, auto-totals revenue detection and recovery figures, and keeps GST/interest/penalty breakdowns in sync. 【F:index.html†L424-L460】【F:index.html†L3342-L3374】
- **Dynamic para management** – Lets users add, remove, and collapse major and minor paras, capture detailed gists in a rich-text area, toggle which para types appear in the summary, and confirm before clearing every entry. 【F:index.html†L462-L480】【F:index.html†L2000-L2160】【F:index.html†L3840-L3852】
- **Risk flag tracker** – Provides an editable table for Template Table 3 so auditors can log risk parameters, descriptions, and verification notes, and requests confirmation before wiping the list. 【F:index.html†L482-L503】【F:index.html†L3824-L3839】【F:index.html†L3854-L3862】
- **Issuing authority block** – Captures issuing officer information and injects a formatted signature table into the generated report. 【F:index.html†L505-L535】【F:index.html†L3798-L3818】
- **Real-time dashboard and totals ribbon** – Surfaces aggregate detection/recovery totals and missing-data warnings to highlight gaps before generation. 【F:index.html†L208-L225】【F:index.html†L545-L574】【F:index.html†L2297-L2316】【F:index.html†L3313-L3336】
- **Accessible pre-flight checklist** – Highlights outstanding unit details, visit dates, and gist gaps while keeping the Generate button available; progress updates still announce blockers and flag paras missing revenue so autosave notices stay informative. 【F:index.html†L202-L225】【F:index.html†L705-L718】【F:index.html†L966-L1106】
- **Session management and autosave** – Supports manual JSON export/import of work in progress and automatically snapshots sessions to localStorage with a restorable history view. 【F:index.html†L567-L601】【F:index.html†L1137-L3112】
- **One-click DOCX generation** – Uses embedded JSZip and FileSaver libraries to merge the captured data into the bundled Word template, remove document protections, and trigger a download of the completed DAR. 【F:index.html†L183-L184】【F:index.html†L3720-L3899】

## Getting started
1. **Open the application** – Launch `index.html` in a modern Chromium- or Firefox-based browser. Network access is required on first load so the JSZip and FileSaver CDNs can provide the generation libraries. 【F:index.html†L183-L184】
2. **Fill Part-I details** – Complete the entity information (all fields except A.R. No. are mandatory), add one or more visit dates, and document the audit circle, group, and team members. Use the fixed navigation rail to swap between sections; only the active card group stays visible while the right pane handles scrolling. 【F:index.html†L236-L535】【F:index.html†L188-L214】【F:index.html†L640-L706】
3. **Enter detection and recovery figures** – Input cash/ITC amounts; totals are recalculated automatically and mapped into the nested tables of the Word template. 【F:index.html†L424-L460】【F:index.html†L3342-L3374】
4. **Capture summary paras** – Use the “Add Para” buttons to create major or minor entries, draft gists and audit comments, and record agreement/revenue outcomes. 【F:index.html†L462-L480】【F:index.html†L2000-L2156】
5. **Log risk flags** – Populate Template Table 3 rows with risk parameters, descriptions, and verification notes using the editor embedded in the Verification column. 【F:index.html†L482-L503】【F:index.html†L3824-L3839】
6. **Review dashboards** – Check the totals ribbon and dashboard for outstanding data gaps; warnings appear if revenue details are missing from any para. 【F:index.html†L208-L225】【F:index.html†L545-L574】【F:index.html†L3313-L3336】
7. **Generate the DAR** – Review the pre-flight checklist for any outstanding blockers, then scroll to the **Output & Session** card at the bottom of the active section and click **Generate DAR** to merge your inputs into the embedded Word template; the tool strips editing protections and downloads `Target-Filled.docx`. You can also re-download the last output without regenerating. 【F:index.html†L202-L225】【F:index.html†L188-L214】【F:index.html†L560-L593】【F:index.html†L3849-L3905】
8. **Save or restore a session** – Use the **Output & Session** card to export your progress as `dar-session.json`, import a saved session, or restore from the rolling autosave history if the browser supports localStorage. 【F:index.html†L560-L593】【F:index.html†L1137-L3112】

## Implementation notes
- The Target.docx template is embedded as a Base64 string and unpacked at runtime; `fillTemplateXml` rewrites the document XML so table structures, headers, and nested tables reflect the latest form data. 【F:index.html†L3490-L3818】
- Autosave snapshots are stored under `dar_form_autosaves_v1` with a 10-entry history cap; users can clear or restore snapshots from the in-app history panel. 【F:index.html†L1137-L3112】
- Generated files default to landscape Indian Legal size (14"×8.5") to match the department specification. 【F:index.html†L3491-L3502】

## Suggested enhancements
- **Bundle offline dependencies** – Ship JSZip and FileSaver with the project (or provide a service worker cache) so the generator works without CDN access, which is useful on restricted government networks. 【F:index.html†L183-L184】
- **Template management** – Add UI controls to upload a revised Word template or select among multiple templates so future format updates do not require editing the embedded Base64 payload manually. 【F:index.html†L3490-L3818】
- **Collaborative review hooks** – Add lightweight task assignments or reviewer hand-offs so multiple officers can coordinate without emailing JSON session files. 【F:index.html†L1137-L3112】
