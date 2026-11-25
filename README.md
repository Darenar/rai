# Rai

Rai reviews a local research folder, checks that its inputs can be reproduced,
and helps send the right files to Git, Hugging Face, Overleaf, and Zotero.
Its three Markdown skills use the tools available in Claude or Codex.

## Install in Claude

For a personal plugin on claude.ai or in Cowork, build a fresh ZIP as
described below and upload it under **Customize → Plugins → Add → Upload plugin**.
Use Cowork with the research folder selected for local file work. Account
and workspace settings control which tools the plugin can use.
[Claude plugin upload instructions](https://claude.com/docs/plugins/build#test-the-plugin-on-each-surface)

For a local Claude Code install, run this from the Rai repository.

```sh
claude plugin install rai-assistant --marketplace "$PWD"
```

Then open your research folder and invoke `/rai-assistant:rai`.

## Install in Codex

From the Rai repository, register its marketplace and install the plugin.

```sh
codex plugin marketplace add "$PWD"
codex plugin add rai@rai-local
```

Open your research folder and ask **Use `$rai` to tell me how to start or
resume work here.** [OpenAI local marketplace guide](https://developers.openai.com/plugins/build/plugins#how-local-marketplaces-work)

## Source and package

The shared package lives in [plugins/rai](plugins/rai/). For a fresh upload,
zip that folder's contents, including its hidden `.claude-plugin` directory.
Use the repository marketplace catalogs for local installs.

[Examples and workflow guides](plugins/rai/README.md) · [MIT license](plugins/rai/LICENSE)
