# Connect and publish a paper to Overleaf

Work from the committed `paper/` tree. Overleaf receives the contents of that
tree at its root. Use a dedicated Overleaf destination for this paper. Linking
the full project GitHub repository to Overleaf exposes the wrong scope. If
there is no manuscript, report that and stop before setting up a remote.

## Connect

1. Inspect existing Git remotes and the project's saved Overleaf settings.
   If the destination is missing, ask the user to open the intended Overleaf
   project, select **Integrations → Git** (or **Menu → Git**), and share the
   displayed Git URL. Help them create a new Overleaf project first if needed.
   Git integration is a premium feature. [Overleaf Git integration](https://docs.overleaf.com/integrations-and-add-ons/git-integration-and-github-synchronization/git-integration)
2. Probe access and the remote's default branch with Git, such as
   `git ls-remote --symref`. If authentication is needed, have the user
   generate a Git authentication token in Overleaf Account Settings and
   enter it at Git's password prompt with username `git`. Reuse the system
   Git credential helper when available. Retry the probe after sign-in.
   [Overleaf authentication](https://docs.overleaf.com/integrations-and-add-ons/git-integration-and-github-synchronization/git-integration/git-integration-authentication-tokens)
3. Verify the returned branch and tip. Fetch its contents for inspection
   without merging into the project branch. If Git access is unavailable,
   report remote status as unverified and check the paper locally. Offer a
   paper-only ZIP for manual upload once the same dependency and file checks
   pass. An incomplete bundle is for diagnosis only.

## Prepare and review

1. Identify the main TeX file and follow LaTeX includes, figures, tables,
   citations, style files, and generated assets from the actual compile root.
   Keep legitimate publication assets in `paper/artefacts/` when appropriate.
   Flag dependencies outside `paper/`, case mismatches, missing files,
   symlinks, submodules, raw data, working outputs, and literature PDFs.
   Trace nested includes and group missing files by directory or generator.
   Show any proposed LaTeX path edits. Compile in isolation when possible
   and report the first failure and its source. Stop for missing required
   assets. [Overleaf Git limitations](https://docs.overleaf.com/integrations-and-add-ons/git-integration-and-github-synchronization/git-integration/advanced-git-operations)
2. Compare committed paper content to the remote root. For each file compare
   actual bytes or verified content hashes. Confirm the remote stores the
   real files. Report **content match** and **next-push readiness** separately.
   Report the history relationship as `equal`, `local-ahead`,
   `remote-ahead`, or `diverged` when supported by ancestry or a recorded
   baseline. If no baseline exists and content differs, show the diff and
   establish whether the destination is new or has collaborator work.
3. Use `git subtree split` with prefix `paper` and the reviewed source
   commit to prepare the candidate. If the split contains LFS/Xet pointers,
   private files in older commits, or history incompatible with a verified
   new or previously synced destination, prepare a paper-only snapshot in a
   separate checkout for review. Materialize the exact committed binaries,
   check their hashes against the pointers, and store ordinary Git blobs.
   Base a snapshot update on the reviewed remote tip to preserve its
   history. Block publication if a file cannot be retrieved or verified.
4. Inspect the actual candidate tree **and every outgoing commit**, including
   old blobs. Apply the history and secret checks from the sync skill. Block
   the push on private inputs, secrets, unusable pointers, or unsupported files.
   Show the reviewer the project URL, branch, source commit, remote
   tip, candidate commit, added, changed and removed files, and compile
   result. Show template files that a first upload would replace.

## Publish or review incoming changes

- When the remote is ahead or both sides changed, show the incoming edits and
  conflicts. Bring accepted edits back under `paper/` as a separate reviewed
  change. Prepare a fresh publication preview after integration.
- If content already matches, skip the push. After approval, record a
  verified baseline for later changes. Reuse existing local
  `rai.overleafSource`, `rai.overleafPublished`, and `rai.overleafBranch`
  settings when they correspond to this Overleaf destination.
- For an approved push, confirm the source and remote tips still match the
  preview. Verify that the candidate advances only the chosen remote branch
  and contains no unrelated ancestry. Push only that candidate ref, with
  tag forwarding disabled.
  Re-fetch the result and compare its contents, including the actual binary
  files. Record the verified branch and baseline in local Git configuration.
  Report file sync and Overleaf compilation separately.
