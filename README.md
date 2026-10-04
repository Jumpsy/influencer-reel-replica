# Influencer Reel Replica

A portable editing skill for Claude, Codex, and other AI agents that can read `SKILL.md` and operate Palmier Pro. It turns a public short-form reference into an original, repeatable edit using a creator's own footage, with a traceable asset ledger and a visual/audio review pass.

## Use it with an AI agent

Give the agent this folder or the link to `SKILL.md`, then ask it to follow the skill for your Reel. The agent needs:

- Access to Palmier Pro and its timeline/media tools (or the ability to give you a Palmier-ready edit recipe).
- A public reference Reel URL, or permission to find one, and your source footage imported into Palmier.
- A browser/search tool to discover references and verify current asset licenses and trend reports. Instagram may limit access; provide a screen recording if the reference cannot be viewed publicly.
- For a downloaded licensed music/SFX file, an authorized download source and local `ffmpeg`; `yt-dlp` is optional and only used when the source explicitly permits it.

The skill does not require a particular model or vendor. Any agent must be able to read the `SKILL.md`, browse when needed, and operate Palmier or document the setup for you.

## Set up Palmier and the agent

Palmier Pro must be open while an external AI agent uses its local MCP server at `http://127.0.0.1:19789/mcp`.

- Claude Desktop: in Palmier, choose **Help → MCP Instructions**, then install the Palmier connector in Claude Desktop.
- Claude Code: `claude mcp add --transport http palmier-pro http://127.0.0.1:19789/mcp`
- Codex CLI: `codex mcp add palmier-pro --url http://127.0.0.1:19789/mcp`
- Other Streamable HTTP clients: add the URL above as an MCP server.
- Palmier's in-app Agent is already connected to its open project; choose Palmier, Claude Code, or Codex in the chat footer.

Verify the connection by listing Palmier projects and reading the intended project's timeline. If no editor is available, open Palmier Pro and reconnect the MCP client. Official setup details: [Palmier Agent and MCP](https://www.palmier.io/docs/agent-and-mcp.md).

## Install as an agent skill

Copy this whole folder into the agent's skill directory, preserving the folder name and `SKILL.md`:

```text
<agent-skill-directory>/influencer-reel-replica/SKILL.md
```

For Claude Code, a personal skill can live at `~/.claude/skills/influencer-reel-replica/SKILL.md`; for Codex, use its configured skills directory (commonly `~/.agents/skills/influencer-reel-replica/SKILL.md`). Other agents can be given the file directly or configured with their own skill-folder convention. The template files are optional working documents, not code dependencies.

For Palmier's in-app Agent, copy this folder to `~/.palmier/skills/influencer-reel-replica/` and manage it under **Settings → Skills**. The in-app Agent and external agents use separate skill directories. Palmier's skill detail also offers an **Add to External Agent** action where supported. In Jacob's Palmier setup, the installed copy is `~/.palmier/skills/influencer-reel-replica/SKILL.md`.

## Repeatable project files

- `templates/reference-breakdown.md` — observed shot-by-shot recipe.
- `templates/asset-ledger.csv` — source, license, attribution, and import record.
- `templates/reel-recipe.md` — Palmier settings and repeatable edit map.

Official references: [Timeline editing](https://www.palmier.io/docs/timeline-editing.md), [Text and captions](https://www.palmier.io/docs/text-and-captions.md), and [Export](https://www.palmier.io/docs/export.md).

Start from the templates on each new series. Preserve style constants, but re-map all source clips and recalculate timing for each new video.

## Music note

Trending TikTok/Instagram sounds are recommendations to add through the platform's own licensed music picker. They are not downloads. Downloadable tracks and SFX require a checked license for the intended use; `yt-dlp` is not used to extract audio from social/video platforms.
