# DAR_TOOL

## Overview
DAR_TOOL is a single-page web application that helps CGST audit teams prepare Draft Audit Reports (DARs). The tool captures all inputs that appear in the department's Target.docx template, summarises audit paras, and generates a fully formatted DAR as a downloadable DOCX file directly in the browser. 【F:index.html†L150-L205】【F:index.html†L2937-L2977】

## Key features
- **Guided Part-I data entry** – Collects unit metadata such as registration number, audit period, visit dates, circle/group assignments, and officer details through structured form controls; every Part-I field except A.R. No. must now be filled. The category field now offers Trader/Manufacturer/Service Provider/ISD/Other presets (with an open text box when “Other” is chosen) and the period picker enforces ordered financial years via dropdowns. 【F:index.html†L208-L311】【F:index.html†L1332-L1469】
- **Detection and recovery calculators** – Mirrors the nested tables in Table 1 of Target.docx, auto-totals revenue detection and recovery figures, and keeps GST/interest/penalty breakdowns in sync. 【F:index.html†L302-L337】【F:index.html†L2460-L2706】
- **Dynamic para management** – Lets users add, remove, and collapse major and minor paras, capture detailed gists in a rich-text area, and toggle which para types appear in the summary. 【F:index.html†L340-L357】【F:index.html†L2013-L2089】
- **Risk flag tracker** – Provides an editable table for Template Table 3 so auditors can log risk parameters, descriptions, and verification notes. 【F:index.html†L360-L379】【F:index.html†L2920-L2934】
- **Issuing authority block** – Captures issuing officer information and injects a formatted signature table into the generated report. 【F:index.html†L384-L417】【F:index.html†L2885-L2915】
- **Real-time dashboard and totals ribbon** – Surfaces aggregate detection/recovery totals and missing-data warnings to highlight gaps before generation. 【F:index.html†L180-L197】【F:index.html†L423-L456】【F:index.html†L2938-L2944】
- **Accessible pre-flight checklist** – Highlights outstanding unit details, visit dates, and gist gaps while keeping the Generate button available; progress updates still announce blockers and flag paras missing revenue so autosave notices stay informative. 【F:index.html†L187-L235】【F:index.html†L528-L564】【F:index.html†L706-L771】【F:index.html†L2333-L2357】
- **Session management and autosave** – Supports manual JSON export/import of work in progress and automatically snapshots sessions to localStorage with a restorable history view. 【F:index.html†L467-L480】【F:index.html†L2013-L2240】【F:index.html†L2990-L3055】
- **One-click DOCX generation** – Uses embedded JSZip and FileSaver libraries to merge the captured data into the bundled Word template, remove document protections, and trigger a download of the completed DAR. 【F:index.html†L162-L163】【F:index.html†L2613-L2915】【F:index.html†L2937-L2977】

## Getting started
1. **Open the application** – Launch `index.html` in a modern Chromium- or Firefox-based browser. Network access is required on first load so the JSZip and FileSaver CDNs can provide the generation libraries. 【F:index.html†L162-L177】
2. **Fill Part-I details** – Complete the entity information (all fields except A.R. No. are mandatory), add one or more visit dates, and document the audit circle, group, and team members. 【F:index.html†L208-L311】
3. **Enter detection and recovery figures** – Input cash/ITC amounts; totals are recalculated automatically and mapped into the nested tables of the Word template. 【F:index.html†L302-L337】【F:index.html†L2460-L2706】
4. **Capture summary paras** – Use the “Add Para” buttons to create major or minor entries, draft gists and audit comments, and record agreement/revenue outcomes. Each para now captures assessee agreement status through a dropdown (Agreed/Not Agreed/Partially Agreed/No reply received) plus a free-text remarks box. 【F:index.html†L340-L357】【F:index.html†L1904-L1951】
5. **Log risk flags** – Populate Template Table 3 rows with risk parameters, descriptions, and verification notes using the editor embedded in the Verification column. 【F:index.html†L360-L379】【F:index.html†L2920-L2934】
6. **Review dashboards** – Check the totals ribbon and dashboard for outstanding data gaps; warnings appear if revenue details are missing from any para. 【F:index.html†L180-L197】【F:index.html†L423-L456】【F:index.html†L2938-L2944】
7. **Generate the DAR** – Review the pre-flight checklist for any outstanding blockers, then click **Generate DAR** (available at any time) to merge your inputs into the embedded Word template; the tool strips editing protections and downloads `Target-Filled.docx`. You can also re-download the last output without regenerating. 【F:index.html†L187-L235】【F:index.html†L2937-L2977】
8. **Save or restore a session** – Export your progress as `dar-session.json`, import a saved session, or restore from the rolling autosave history if the browser supports localStorage. 【F:index.html†L467-L480】【F:index.html†L2013-L2240】【F:index.html†L2990-L3055】

## Implementation notes
- The Target.docx template is embedded as a Base64 string and unpacked at runtime; `fillTemplateXml` rewrites the document XML so table structures, headers, and nested tables reflect the latest form data. 【F:index.html†L2613-L2915】
- Autosave snapshots are stored under `dar_form_autosaves_v1` with a 10-entry history cap; users can clear or restore snapshots from the in-app history panel. 【F:index.html†L2013-L2240】
- Generated files default to landscape Indian Legal size (14"×8.5") to match the department specification. 【F:index.html†L2613-L2626】

## Suggested enhancements
- **Bundle offline dependencies** – Ship JSZip and FileSaver with the project (or provide a service worker cache) so the generator works without CDN access, which is useful on restricted government networks. 【F:index.html†L162-L163】
- **Template management** – Add UI controls to upload a revised Word template or select among multiple templates so future format updates do not require editing the embedded Base64 payload manually. 【F:index.html†L2613-L2915】
- **Collaborative review hooks** – Add lightweight task assignments or reviewer hand-offs so multiple officers can coordinate without emailing JSON session files. 【F:index.html†L2990-L3055】
