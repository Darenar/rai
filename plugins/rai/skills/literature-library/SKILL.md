---
name: literature-library
description: Connect or set up Zotero, review and import research PDFs, verify item and attachment sync, and export citations.
---

# Literature with Zotero

Reuse the user's Zotero account and library. Confirm the target library and
collection. Check separately for search, metadata writes, stored PDF writes,
and sync verification. In Codex, the Zotero plugin can help with search and
BibTeX. In Claude, check for an authorized Zotero connector or local desktop
access. A connector that imports citation records may still lack file upload.
If a project has no selected literature PDFs, skip import. Check connection
readiness on request. Keep an existing project bibliography usable. If asked
to import it, preview those records as metadata only. Never count a manuscript
PDF or a BibTeX entry as a stored literature attachment.

## Connect Zotero

1. If needed, help the user install and open [Zotero Desktop](https://www.zotero.org/download/).
   Have them sign in under **Settings → Sync**. Check both data sync and
   attachment sync for the selected library. Reuse an existing file-sync
   setup. Use Zotero Storage when setting up a new library unless the user
   chooses an alternative. [Zotero sync guide](https://www.zotero.org/support/sync)
2. If using local access, enable **Settings → Advanced → Allow other
   applications on this computer to communicate with Zotero** with the user's
   approval. Probe the [local API](https://www.zotero.org/support/dev/web_api/v3/local_api)
   from the same machine. Local API writes require Zotero 10 or later and
   consent in Zotero's own dialog. Use the documented item and file-upload
   flow if the host can keep the authorization private. Keep credentials
   out of chat and project files.
3. If the host cannot reach Zotero or attach a PDF, prepare the metadata and
   show the user the exact record and file to add in Zotero Desktop. For an
   existing item, use **Add Attachment → Attach Stored Copy of File**. Then
   resume verification. [Zotero attachment guide](https://www.zotero.org/support/attaching_files)

## Import and verify

1. Inventory the selected PDFs or `literature/`. Read the title pages and
   verify title, authors, year, and DOI when present. Show uncertain fields
   before importing.
2. Search the destination by DOI, then title and authors. Compare attachment
   bytes when possible. Preview the item to reuse or create, the file to
   attach, and ambiguous matches. Get approval for the exact changes.
3. Create or reuse the parent record and add a stored PDF. Use
   `Author - Year - Title.pdf` when supported. Preserve the original. Record
   the parent and attachment keys. Confirm the stored file opens and matches
   the source bytes when accessible. On a partial import, check both keys
   before retrying so a retry cannot create a duplicate.
4. Report **record sync** and **PDF sync** separately. Wait for Zotero's sync
   and check errors or storage limits when pending. Verify the exact item in
   the online library and, with Zotero Storage, open or download its PDF.
   With WebDAV, verify on a second synced device or with the authorized
   storage tool. Treat local success and library-wide sync timestamps as
   insufficient evidence of remote PDF availability.

## Cite and migrate

Export only selected project items. Merge into `references.bib`, preserving
existing cited keys and unrelated entries. If asked, insert the selected
citation at the reviewed place in the draft. Keep literature PDFs out of
project Git and Overleaf.

For an older Rai library, use `literature/manifest.json` to locate PDFs and
metadata. Keep the old manifest and PDFs until the imported items and
attachments are verified.
