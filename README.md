# SMC to UCLA Transfer Planning GPT

Implementation package for a custom GPT that helps Santa Monica College students compare completed SMC coursework against UCLA undergraduate major-preparation articulation agreements.

The GPT uses custom Actions only:

- ASSIST Action: no-auth calls to public ASSIST SMC-to-UCLA 2025-2026 major agreements.
- Google Drive Action: OAuth read-only access to curated normalized Google Doc metadata.

This is an unofficial planning aid. Students must verify transfer plans with an SMC counselor before enrollment or application decisions.

## Files

- `gpt/instructions.md`: paste into the GPT Builder Instructions field.
- `actions/assist-openapi.yaml`: ASSIST Action schema.
- `actions/google-drive-openapi.yaml`: Google Drive Action schema.
- `public/privacy-policy.html`: privacy policy page content for publishing.
- `drive-cache/*.md`: normalized Google Doc source content for demo majors.
- `docs/setup-guide.md`: step-by-step GPT Builder, Google OAuth, and Drive setup.
- `tests/preview-test-script.md`: manual GPT Preview test script.
