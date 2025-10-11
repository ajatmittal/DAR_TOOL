# Test Results

## Playwright smoke test
- **Setup:** Served the app locally with `python -m http.server 8000` and executed an automated Playwright flow against `index.html`.
- **Validation summary:** Clicking **Generate DAR** with an empty form surfaced the validation summary with the following errors:
  - Name of Unit is required.
  - Registration Number is required.
  - Commissionerate/Division/Range is required.
  - Period Covered is required.
  - A.R. Number is required.
  - Add at least one audit visit date.
  - Add at least one para (major or minor) before generating.
- **Rich-text sanitization:** After adding a para card, injecting `<script>` and `javascript:` URI content into the gist editor resulted in sanitized markup of `<div><p>Testalert(1)<a>bad</a></p></div>` where scripting content and unsafe URI attributes were stripped.

These automated assertions confirm that the validation gate and rich-text sanitizer behave as expected in the browser.

## Dashboard flag clearing check
- **Setup:** Served the app locally with `python -m http.server 8000` and ran a headless Playwright script against `index.html` to mimic entering para data.
- **Observation:** Upon adding a major para the dashboard reported three missing-field flags. After programmatically filling the gist, agreement status/notes, and audit comment, the script observed the dashboard flag list dropping to zero within the same interaction cycle, confirming immediate recalculation.
