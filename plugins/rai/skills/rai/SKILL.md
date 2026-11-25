---
name: rai
description: Start or resume a research project. Review its environment, trace inputs, and preview or apply an optional Git-backed reorganisation.
---

# Start or resume research

Work in the user's selected folder. Start with a read-only review of the
project instructions, Git state, environment files, and main entry points.
If the folder has no Git history, review the current files and report checkout
coverage as unverified. Use the [input audit](../research-sync/SKILL.md#input-audit)
before proposing formatting or setup, even for one project.

For archives, check expanded size, member paths, duplicates, and extraction
errors. Preserve the originals. Extract needed files in isolation, skipping
transport metadata. Check for nested archives, nonportable binaries, and
legacy filenames before relying on those paths. Preserve the documented layout
of a working replication package and report gaps before moving files.

Lead with what the user can do next. Give the run command and working directory
when known, then show the few dependencies, inputs, or project changes that need
attention. Continue in a working layout if the user wants to keep it.

## Environment

- Reuse the project's declared Python, R, or other environment and its run
  instructions. Report missing tools and stale lockfiles. Restore dependencies
  only when requested or approved.
- For new Python projects propose uv. For new R projects propose renv. For
  existing code without a declared environment, inspect imports, notebook
  kernels, runtime versions, and project instructions. Show the missing
  declarations and the packages you can verify before setting them up.
- Use official installation instructions for missing tools. Keep dependency
  declarations and lockfiles in Git and installed libraries local. After
  setup, run the approved smoke test and report whether it passed separately
  from whether the environment installed. Check that the test used the real
  inputs. Label a run using demo, simulated, or precomputed inputs.

## Optional reorganisation

Prefer the existing structure when it works. For a new layout, use `code/`,
`paper/`, `artefacts/raw/` for retained local inputs, `artefacts/intermediate/`,
`artefacts/final/`, `other/`, and `literature/` as needed. Keep Git, build, and
environment configuration at the root. Use the same
[paper rules](../research-sync/overleaf.md#prepare-and-review) for formatting and publishing.

1. Review the baseline, pending edits, and ignored files. Show the exact
   paths to stage, including for a new repo. Keep preservation copies of
   archives and unresolved inputs outside staging. Check Git identity and
   get approval before creating a commit.
2. Show exact source and destination paths, affected references, and anything
   that would block publishing the paper. Preserve legitimate manuscript
   figures and tables. If one must move, include its LaTeX reference edits.
   Flag ambiguous, hard-coded, or file-relative paths. Rewrite only traced
   references with one verified replacement.
3. After approval, confirm the baseline and files still match the proposal.
   Use Git-backed moves for tracked files. Edit only the affected references,
   preserve unrelated edits, and review the diff before making the agreed
   commit. Run the approved entry point or smoke test.

Use [Research sync](../research-sync/SKILL.md) to move data or publish and
[Literature library](../literature-library/SKILL.md) for references.
