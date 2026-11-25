---
name: research-sync
description: Trace research inputs, register shared raw data, verify a fresh checkout, and review or perform GitHub, Hugging Face, and Overleaf sync.
---

# Data and sync

Start with the user's selected folder and the requested operation. Use the
host's file, Git, or service tools. If the host lacks access, finish the local
review and tell the user the one step that will unblock the next check. Use
provider sign-in dialogs or credential helpers. Keep credentials out of chat,
commands, Git URLs, and project files.

## Where files belong

| What it is | Where to keep it |
| --- | --- |
| Original research inputs, including files read from another folder | A separate **private Hugging Face dataset**. Keep pins in project-root `data.json`. Retained originals stay local and outside staging. |
| Code, environment files, manuscript sources, and generated results | Project Git. Put working results in `artefacts/intermediate/` and final results in `artefacts/final/` where these folders fit the project. |
| The manuscript and the figures, tables, and bibliography it needs | `paper/` in project Git. Overleaf receives the contents of this subtree at its project root. |
| Reference PDFs | Zotero stored attachments. Keep local originals out of project Git. Cite with the project's `references.bib`. |

Check sharing rights for source, data, and results before any remote backup.
Keep restricted or uncleared material local, including extracted archive
members. Classify files by use. For example, a CSV written by the analysis remains an
intermediate result even if it sits in a folder named `raw`.

## Input audit

Before a format, setup, or sync proposal, trace reads in the entry scripts,
notebooks, and configuration using their actual working directories and
file-relative paths. Trace the corresponding writes to tell inputs from
generated outputs. For spreadsheets used as inputs, look for external links
and required macros without running them. Give the file and line or cell for
external, missing, and unresolved reads. Inspect unknown code without running it.
Review the existing `data.json` and flag pins the code never uses. Check the
replication README and license for restricted inputs and approved substitutes.
Distinguish original inputs, missing prerequisites, and supplied outputs that
a later stage reads. Keep the provenance of simulated or precomputed files.

List confirmed raw files before asking where to store them. When there are no
raw inputs or unresolved reads, skip dataset setup. For Overleaf-only work,
check the manuscript's own dependencies and report separate analysis gaps.

## Register shared data

1. Reuse the existing private dataset or the `data_repo` default in the user's
   local configuration. Check `rai/profile.json` in the configured user
   config directory, or in `~/.config` by default. Use the chosen project
   override. If no dataset is set, ask for the dataset ID or permission to create a private
   dataset under the selected account. Check identity, dataset type, and
   visibility with the [Hugging Face CLI](https://huggingface.co/docs/huggingface_hub/en/guides/cli)
   or an authorized Hub tool. If signed out, guide the user through the
   [Hub sign-in flow](https://huggingface.co/docs/huggingface_hub/main/quick-start#authentication),
   then retry the read. Record a default outside project Git only on request.
2. Read the shared dataset's root `manifest.json` at the current revision.
   It maps each SHA-256 to one or more dataset paths. Hash the local bytes and
   verify the bytes at any proposed match before reusing it. A same-name file
   with a different hash needs a new path. A missing or stale index needs a
   separate preview and repair from actual stored bytes. Preserve old pins.
3. For a new input, suggest a folder from its name and a brief local look at
   headers or sample rows. Use an existing category, propose a new one, or use
   `other/`. Preview exact source paths, destination paths, and reuse or
   upload decisions. Preserve originals. After approval, recheck inputs and
   dataset revision, commit the files and manifest together, and verify the
   stored bytes. If a commit fails or the dataset advances, re-read its state
   before retrying. Add exact ignore entries for retained project copies.
   Mark files with unclear sharing rights as local-only pending review.
4. Write only verified references to project-root `data.json`. Each input
   name maps to `repo_id`, `filename`, `revision` (full dataset commit SHA),
   and `sha256`. Update the exact read sites to use those pins via the
   project's data-loading conventions. Declare dependencies in the project's
   environment. Keep valid existing pins unless the user approves a change.
5. Download pins with an empty cache from a fresh checkout and compare SHA-256.
   Run the project's approved input-loading test. Report separately whether
   the pins resolve, the code actually read them, and collaborators can access
   the dataset. For software that expects local paths, restore the verified
   bytes to documented input locations and test from there. Keep the originals.

## Project backup

Use a separate private Hugging Face dataset repo for project Git by default,
especially for large results. Use GitHub for project Git when the user asks
and its preflight passes. Identify existing remotes by URL, including
`origin`. For a missing destination, confirm owner, repo, and visibility
before creating it. For a new Hub repo, write a short [dataset card](https://huggingface.co/docs/hub/en/datasets-cards)
with valid metadata and the scope of the backup. State a license only when
verified. Reuse Hub or Git credentials. If GitHub needs sign-in,
use the [GitHub authentication instructions](https://docs.github.com/en/github-cli/github-cli/authenticating-with-github-cli).
Fetch the selected branch to confirm access and tip. Set or remove only the
local remote the user approved.

For each selected remote, answer **does committed content match?** and
**is the next push ready?** State uncommitted and untracked paths separately.
Preview one destination at a time, with visibility, branch, exact local and
remote commits, changed paths, and blockers. Scan all outgoing commits,
including old blobs and merged ancestry, for secrets, raw inputs, oversized
files, and unusable pointers. Use Gitleaks or an equivalent history scan.
Block the push on a finding or an unavailable check and identify the path
and commit. Scan the outgoing blobs and nested archive contents. A diff scan
alone leaves binary and archive coverage unverified. Exclude unverified
archives from a reviewed export. An ignore rule cannot remove tracked or
historical files. Keep upstream history in its own checkout. For a selective
backup, list withheld prerequisites and their source or archive member, their
expected restore paths, and any checksums you verified. Apply the clean
checkout and actual-input smoke checks above to files restored from local
archives too. Report reproduction as unverified if its prerequisites are missing.

Approve exact paths before enabling Git-Xet or LFS for large outputs. Verify
the objects can be retrieved. Confirm a new Hugging Face repo has only its
known `.gitattributes` bootstrap before proposing a local merge that preserves
the project's rules. Other remote-ahead or divergent branches need review.
After approval, recheck both tips and the destination. Push only the reviewed
ref, fast-forward only, then verify the remote tip. On failure, inspect what
already happened before retrying.

## Overleaf

Use the [Overleaf connection and publication guide](overleaf.md) for setup,
paper-only status, incoming edits, and publishing. Use its paper file rules
when formatting a project.
