# PartyMode

Bring your AI agents into Blender, and let them build together. A Blender 5.3 add-on.

This repository only holds the release zips. It's private: you're here because you were invited.

## Install

1. Open the [latest release](../../releases/latest) and download `agent_bridge-<version>.zip`. Don't unzip it.
2. Drag the zip onto your Blender 5.3 window and click **Install**.
   (Or: Edit › Preferences › Get Extensions › ⌄ › Install from Disk, and pick the zip.)
3. Click **PartyMode** in the 3D View header, and say what to make.

The chat needs one AI agent installed and signed in on your computer:
[Claude Code](https://claude.com/claude-code) (with a Claude plan),
[Codex](https://github.com/openai/codex) (with a ChatGPT plan), or
[OpenCode](https://opencode.ai) (hosted models, or local ones that keep everything on your machine).

## Updates

PartyMode checks this repository once a day and offers new versions in its preferences
(Edit › Preferences › Add-ons › PartyMode). Because the repository is private, that check needs
the [GitHub CLI](https://cli.github.com) installed and signed in (`gh auth login`). Without it,
come back to the [releases page](../../releases/latest) for new versions, and drag the new zip in
the same way.
