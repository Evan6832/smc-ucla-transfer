# Setup Guide

## 1. Create the GPT

1. Open ChatGPT on the web.
2. Go to Explore GPTs, then Create.
3. Open Configure.
4. Name: `SMC to UCLA Transfer Planning GPT`.
5. Description: `Unofficial transfer planning assistant for Santa Monica College students comparing completed SMC coursework against UCLA undergraduate major-preparation articulation agreements.`
6. Paste `gpt/instructions.md` into Instructions.
7. Enable file uploads / data analysis if available so students can upload unofficial transcripts.
8. Do not enable Apps. This GPT uses Actions only.

## 2. Add the ASSIST Action

1. In Actions, create a new Action.
2. Authentication: None.
3. Import or paste `actions/assist-openapi.yaml`.
4. Privacy policy URL: use the published URL for `public/privacy-policy.html`.
5. Test `listUclaSmcMajorAgreements` with:
   - `receivingInstitutionId`: `117`
   - `sendingInstitutionId`: `137`
   - `academicYearId`: `76`
   - `types`: `Major`
6. Confirm the response includes `Psychology/B.A.`, `Computer Science/B.S.`, and `Business Economics/B.A.`.
7. Test `getArticulationAgreement` with key `76/137/to/117/Major/4326f498-897c-4aae-1fce-08ddcb96df9e`.

## 3. Prepare Google OAuth

1. In Google Cloud Console, create or select a project.
2. Enable the Google Drive API.
3. Configure OAuth consent screen.
4. User type: External for personal/test accounts, unless using an internal Google Workspace.
5. Add scope: `https://www.googleapis.com/auth/drive.readonly`.
6. Add yourself and any interview reviewer emails as OAuth test users.
7. Create OAuth client credentials for a web application.
8. In GPT Builder, create the Google Drive Action and choose OAuth.
9. Use:
   - Authorization URL: `https://accounts.google.com/o/oauth2/v2/auth`
   - Token URL: `https://oauth2.googleapis.com/token`
   - Scope: `https://www.googleapis.com/auth/drive.readonly`
   - Token exchange method: Default / authorization code
10. Copy the callback URL from GPT Builder into the Google OAuth client's authorized redirect URIs.

Note: `drive.readonly` is a restricted Google scope. For an interview assessment, keep the app in testing mode and add reviewers as test users. Full public use may require Google verification.

## 4. Add the Google Drive Action

1. Authentication: OAuth.
2. Import or paste `actions/google-drive-openapi.yaml`.
3. Test `searchDriveCacheFiles` with:
   - `q`: `name contains 'ASSIST 2025-2026 SMC to UCLA' and mimeType = 'application/vnd.google-apps.document' and trashed = false`
   - `pageSize`: `10`
4. Test `getDriveFileMetadata` on one returned Google Doc file id.

## 5. Create the Drive Cache

Create a Google Drive folder named `SMC-UCLA Articulation Cache`.

Create three native Google Docs using these exact titles:

- `ASSIST 2025-2026 SMC to UCLA - Psychology/B.A. - Normalized`
- `ASSIST 2025-2026 SMC to UCLA - Computer Science/B.S. - Normalized`
- `ASSIST 2025-2026 SMC to UCLA - Business Economics/B.A. - Normalized`

Paste the matching source content from `drive-cache/` into each document.

In this workspace, the three Google Docs have already been created and verified. See `docs/drive-cache-links.md` for links. The connector available in this session did not expose a folder-create or move operation, so move those docs into the `SMC-UCLA Articulation Cache` folder manually if you want strict folder organization.

## 6. Conversation Starters

- `I want to transfer from SMC to UCLA Psychology. Here is my course list: PSYC C1000 A, STAT C1000 B, BIOL 3 IP. What is left?`
- `Which SMC courses can satisfy UCLA Computer Science B.S. lower-division preparation?`
- `I am considering UCLA Business Economics. Which requirements have no SMC articulation?`
- `I uploaded my unofficial SMC transcript. Can you audit it against UCLA Psychology/B.A.?`
