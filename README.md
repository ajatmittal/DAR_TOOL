# DAR_TOOL

## Overview
DAR_TOOL is a single-page web application that helps CGST audit teams prepare Draft Audit Reports (DARs). The tool captures all inputs that appear in the department's Target.docx template, summarises audit paras, and generates a fully formatted DAR as a downloadable DOCX file directly in the browser. 【F:index.html†L188-L603】【F:index.html†L3843-L3899】

## Key features
- **Guided Part-I data entry** – Collects unit metadata such as registration number, audit period, visit dates, circle/group assignments, and officer details through structured form controls; every Part-I field except A.R. No. must now be filled. 【F:index.html†L236-L420】
- **Responsive navigation rail** – Keeps section shortcuts in a sticky left rail on wide screens, collapses them into a horizontal top bar on smaller viewports, and now reveals only the selected section while moving focus to its heading for keyboard users. 【F:index.html†L188-L214】【F:index.html†L640-L699】
- **Detection and recovery calculators** – Mirrors the nested tables in Table 1 of Target.docx, auto-totals revenue detection and recovery figures, and keeps GST/interest/penalty breakdowns in sync. 【F:index.html†L424-L460】【F:index.html†L3342-L3374】
- **Dynamic para management** – Lets users add, remove, and collapse major and minor paras, capture detailed gists in a rich-text area, and toggle which para types appear in the summary. 【F:index.html†L462-L480】【F:index.html†L2000-L2156】
- **Risk flag tracker** – Provides an editable table for Template Table 3 so auditors can log risk parameters, descriptions, and verification notes. 【F:index.html†L482-L503】【F:index.html†L3824-L3839】
- **Issuing authority block** – Captures issuing officer information and injects a formatted signature table into the generated report. 【F:index.html†L505-L535】【F:index.html†L3798-L3818】
- **Real-time dashboard and totals ribbon** – Surfaces combined detection/recovery totals, para-wise summaries, and missing-data warnings to highlight gaps before generation. 【F:index.html†L208-L225】【F:index.html†L545-L579】【F:index.html†L2297-L2316】【F:index.html†L3313-L3362】【F:index.html†L3486-L3572】
- **Accessible pre-flight checklist** – Highlights outstanding unit details, visit dates, and gist gaps while keeping the Generate button available; progress updates still announce blockers and flag paras missing revenue so autosave notices stay informative. 【F:index.html†L202-L225】【F:index.html†L705-L718】【F:index.html†L966-L1106】
- **Session management and autosave** – Supports manual JSON export/import of work in progress and quietly snapshots sessions to localStorage, restoring the latest draft on load when available. 【F:index.html†L567-L601】【F:index.html†L3170-L3239】
- **Excel-ready session export** – Flattens the current DAR session into a single-row workbook so teams can analyse metadata, dashboard totals, and per-para/risk notes in spreadsheets without any build tooling. 【F:index.html†L567-L601】【F:index.html†L3214-L3324】【F:index.html†L4051-L4084】
- **One-click DOCX generation** – Uses embedded JSZip and FileSaver libraries to merge the captured data into the bundled Word template, remove document protections, and trigger a download of the completed DAR. 【F:index.html†L183-L184】【F:index.html†L3720-L3899】

## Getting started
1. **Open the application** – Launch `index.html` in a modern Chromium- or Firefox-based browser. Network access is required on first load so the JSZip and FileSaver CDNs can provide the generation libraries. 【F:index.html†L183-L184】
2. **Fill Part-I details** – Complete the entity information (all fields except A.R. No. are mandatory), add one or more visit dates, and document the audit circle, group, and team members. Use the navigation rail to swap between sections; only the active card group stays visible so you can focus on one area at a time. 【F:index.html†L236-L535】【F:index.html†L188-L214】【F:index.html†L640-L699】
3. **Enter detection and recovery figures** – Input cash/ITC amounts; totals are recalculated automatically and mapped into the nested tables of the Word template. 【F:index.html†L424-L460】【F:index.html†L3342-L3374】
4. **Capture summary paras** – Use the “Add Para” buttons to create major or minor entries, draft gists and audit comments, and record agreement/revenue outcomes. 【F:index.html†L462-L480】【F:index.html†L2000-L2156】
5. **Log risk flags** – Populate Template Table 3 rows with risk parameters, descriptions, and verification notes using the editor embedded in the Verification column. 【F:index.html†L482-L503】【F:index.html†L3824-L3839】
6. **Review dashboards** – Check the totals ribbon and dashboard for outstanding data gaps; the dashboard now lists overall detection/recovery totals plus para-wise breakdowns, and warnings appear if revenue details are missing from any para. 【F:index.html†L208-L225】【F:index.html†L545-L579】【F:index.html†L3313-L3362】【F:index.html†L3486-L3572】
7. **Generate the DAR** – Review the pre-flight checklist for any outstanding blockers, then open **Output & Session** in the navigation rail and click **Generate DAR** to merge your inputs into the embedded Word template; the tool strips editing protections and downloads `Target-Filled.docx`. The completion toast now offers a “Download again” shortcut if you need another copy immediately. 【F:index.html†L202-L225】【F:index.html†L188-L214】【F:index.html†L567-L601】【F:index.html†L4009-L4040】
8. **Save or restore a session** – Export your progress as `dar-session.json`, generate a spreadsheet via **Download Excel**, or import a saved session. Autosave runs silently in the background; if a snapshot exists when you reopen the tool it is restored automatically, with an option in the toast to discard it. 【F:index.html†L567-L601】【F:index.html†L3170-L3239】【F:index.html†L4051-L4084】

## Implementation notes
- The Target.docx template is embedded as a Base64 string and unpacked at runtime; `fillTemplateXml` rewrites the document XML so table structures, headers, and nested tables reflect the latest form data. 【F:index.html†L3490-L3818】
- Autosave snapshots are stored under `dar_form_autosaves_v1` with a 10-entry history cap; the latest snapshot restores itself automatically on load and can be discarded from the notification action. 【F:index.html†L3170-L3239】
- Generated files default to landscape Indian Legal size (14"×8.5") to match the department specification. 【F:index.html†L3491-L3502】

## Suggested enhancements
- **Bundle offline dependencies** – Ship JSZip and FileSaver with the project (or provide a service worker cache) so the generator works without CDN access, which is useful on restricted government networks. 【F:index.html†L183-L184】
- **Template management** – Add UI controls to upload a revised Word template or select among multiple templates so future format updates do not require editing the embedded Base64 payload manually. 【F:index.html†L3490-L3818】
- **Collaborative review hooks** – Add lightweight task assignments or reviewer hand-offs so multiple officers can coordinate without emailing JSON session files. 【F:index.html†L1137-L3112】
