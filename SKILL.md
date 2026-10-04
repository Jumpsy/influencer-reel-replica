---
name: influencer-reel-replica
description: Find and analyze a public Instagram/TikTok/Reels reference, then recreate its editing grammar with the user's own footage in Palmier Pro. Covers reference discovery, shot-by-shot timing, visual asset sourcing and rights checks, repeatable Palmier setup, captions, SFX, licensed music and trend-sound suggestions, render inspection, and reusable edit recipes. Use when an influencer asks an AI to edit a Reel like a reference, replicate a viral edit, source visuals or sounds, or make this format repeatably in Palmier.
---

# Influencer Reel Replica

Create a repeatable short-form edit in Palmier from a public reference and the creator's own footage. Reproduce the **editing grammar** (structure, pacing, framing, transitions, caption behavior, sound roles), not another creator's identity, watermark, exact script, or protected assets. Match the requested format while keeping every source and license traceable.

## Operating contract

- Work inside the active Palmier project when its tools are available. Any compatible AI agent can follow this skill if given Palmier access; otherwise produce the edit recipe and setup checklist for the creator to apply in Palmier.
- Never claim to have watched a reference, downloaded an asset, rendered, or listened to audio unless the relevant tool or file gave direct evidence.
- Ask for a reference URL or permission to search when none is provided; ask for source footage if it is not in the Palmier library. Continue independent discovery while waiting.
- Ask before purchasing, subscribing, posting, or using paid generation. Do not publish or contact anyone.
- Use licensed assets and the creator's own footage. Do not bypass login, DRM, download restrictions, or platform controls. Do not remove watermarks or copy a real person's likeness/voice without permission.

## Palmier and agent setup

### Install this skill

- **Palmier in-app Agent:** copy the entire `influencer-reel-replica` folder to `~/.palmier/skills/influencer-reel-replica/`, or install/manage it through Palmier Pro's **Settings → Skills**. The Palmier in-app Agent loads skills from `~/.palmier/skills`.
- **Claude Code:** copy this folder into `~/.claude/skills/influencer-reel-replica/` (or the project's `.claude/skills/` directory).
- **Codex:** copy it into the configured skills directory, commonly `~/.agents/skills/influencer-reel-replica/`.
- **Other agents:** give the agent this folder or the `SKILL.md` and tell it to follow the workflow. The client must support Markdown skill instructions and be connected to Palmier MCP to edit a timeline.
- The Palmier-managed community skill catalog is separate from the standalone repository. In Palmier, use **Settings → Skills** to install and manage local skills. For Claude/Codex, add the skill to their own skill directories or use the Palmier skill detail's external-agent installation action when available.

### Connect Palmier Pro

Palmier Pro must be installed and open; its local MCP server is available at `http://127.0.0.1:19789/mcp`.

- **Claude Desktop:** in Palmier choose **Help → MCP Instructions**, select the Claude Desktop connector, then install/confirm it in Claude Desktop.
- **Claude Code:** run `claude mcp add --transport http palmier-pro http://127.0.0.1:19789/mcp`.
- **Codex CLI:** run `codex mcp add palmier-pro --url http://127.0.0.1:19789/mcp`.
- **Other Streamable HTTP MCP client:** add `http://127.0.0.1:19789/mcp` as the Palmier MCP server.
- **In-app Agent:** open the target Palmier project and choose Palmier, Claude Code, or Codex in the chat footer; configure external agents in **Settings → Agent**.

Restart the agent session if it was already open while connecting Palmier. Verify the connection by listing Palmier projects and reading the intended project's timeline. The official guides are [Agent and MCP](https://www.palmier.io/docs/agent-and-mcp.md), [Timeline editing](https://www.palmier.io/docs/timeline-editing.md), [Text and captions](https://www.palmier.io/docs/text-and-captions.md), and [Export](https://www.palmier.io/docs/export.md).

If Palmier reports that no editor is available, stop timeline operations and help the creator open Palmier Pro and reconnect the MCP client. Do not silently switch to another project or claim an edit was applied.

## Intake

Collect what is missing, in one concise set of questions:

1. Reference Reel URL (Instagram preferred) or the edit's name/description.
2. Creator footage and brand assets already imported into Palmier.
3. Destination and target length (default Instagram Reel, vertical 9:16, 15–30 seconds).
4. Music preference: platform-native trend suggestion, licensed downloadable track, or no music; whether speech must remain clear.
5. Reuse target: just this video or a reusable template for future episodes.

If the user already supplied an item, do not ask again. Keep the creator's exact claims and spoken wording; never invent testimonials, product results, or factual claims.

## 1. Find a usable reference

1. Open the supplied public URL using the agent's available browser/web tool. If no URL is supplied and web search is available, search Instagram/Reels and public creator pages for a close format match. If the `agent-reach` skill is installed, use it for platform research; otherwise use the available browser/search tool directly.
2. Prefer a reference that is publicly viewable and whose timing, framing, captions, and sound can actually be inspected. If Instagram blocks playback, report that limitation and request an uploaded screen recording or a second public reference; do not pretend metadata is a full review.
3. Record URL, account, title/caption if visible, access date, duration, aspect ratio, and what was observable. Don't download or repost the reference video. Use it for analysis only.
4. If multiple candidates fit, present up to three with a one-line reason each; select the supplied or clearly closest match without delaying the edit unnecessarily.

## 2. Break down the reference into an edit recipe

Watch the whole clip at normal speed, then review key moments frame-by-frame or with screenshots if available. Note what was truly observed versus inferred. Create a beat sheet with one row per shot/beat:

| In–out time | Shot/visual | Framing or movement | Edit / transition | On-screen text | Audio event | Purpose |
|---|---|---|---|---|---|---|

Capture:

- Hook and first visual change; beat lengths; shot count; cut rhythm; ending/loop.
- Camera distance, orientation, movement, crop, speed changes, and any overlays.
- Caption placement, line length, emphasis behavior, typography character, and safe margins. Use a matching Palmier caption preset where possible; verify unfamiliar fonts in the render.
- Sound structure: speech, music energy/tempo, accents, pauses, and sound-effect roles. Identify a viral sound only if directly observable; name/link it as a suggestion, not an acquired asset.
- What can be recreated with the creator's own footage and simple edit treatment; what would require third-party rights or generation.

Do not infer exact BPM, fonts, lens, or color values from an inaccessible or compressed preview. Mark estimates as estimates.

## 3. Asset research and rights ledger

Source only assets that serve a specific beat. Prefer creator-provided brand assets, then open-license/CC0 libraries and reputable stock providers with clear licenses. Use `image_query`/web search only to discover; open the source page and verify the license and download terms before use. Save attribution and source URLs with the project.

Make an asset ledger before importing. Start from `templates/asset-ledger.csv` in this package when available:

| Asset | Beat | Source URL | License / permitted use | Attribution | Local filename |
|---|---|---|---|---|---|

- Import permitted stills/video/audio into Palmier with `import_media`. Check the import receipt and wait for its reported readiness; then use `get_media` to confirm the imported items and their technical properties. Retain local source files until Palmier confirms managed storage.
- Don't use a random Google Images result, scrape Instagram posts, or assume that publicly viewable means reusable.
- If there is no clearly reusable asset for a beat, use the creator's footage, a generated original asset (with user approval for paid generation), or omit the beat and document the substitution.

## 4. Music and sound effects

Always separate a **trend recommendation** from a **downloadable master recording**.

### Viral TikTok / Reels sounds

- If the user wants a viral sound, search current public trend reports or the platform's own trend discovery surface if available. Trends change quickly: verify the sound name, creator/artist, and date from a current source. Give the platform-native sound title/artist and direct in-app search/use instructions.
- Do not download a TikTok/Instagram sound using `yt-dlp` or another extractor. Do not treat a trend report, preview, or reference-video audio as a license to reuse the recording.
- If the creator chooses a platform-native sound, edit a clean version in Palmier with speech/SFX and leave a labeled music placeholder or deliver a music-free master. The creator adds the sound through the destination platform's licensed music picker at publishing time and checks account/region availability.
- Do not promise a sound is available or cleared for a business/brand account unless the platform confirms it for that account and use.

### Licensed downloadable music

- Ask whether the creator wants a downloadable music bed. Find a track from a source that explicitly permits the intended commercial/social use. Check the license, attribution, territory, duration, and platform limits; record the exact URL and license evidence.
- Prefer the source's official download button. `yt-dlp` is only for a source whose terms explicitly authorize third-party downloading and whose license permits this exact use. Never use it to extract music from TikTok/Instagram, bypass access controls, or ignore a platform's download restrictions. Do not infer permission from an open license alone; confirm both the platform's download terms and the asset license. If either is unclear, use the official download route or a different track.
- If approved and `yt-dlp` plus `ffmpeg` are installed, download one authorized audio source and retain its metadata for provenance:
  ```bash
  yt-dlp --no-playlist --extract-audio --audio-format mp3 --write-info-json -o "./assets/audio/%(title).150B-%(id)s.%(ext)s" "<AUTHORIZED_AUDIO_URL>"
  ffprobe -v error -show_format -show_streams "./assets/audio/<downloaded-audio-file>"
  ```
  Use the exact supported download URL, not a search result URL. Confirm the output is an audio file, listen to it, and record its source and license in `templates/asset-ledger.csv` before importing.
- If license terms are unclear, don't download or use the track. Offer it as a listening reference and find a cleared alternative.
- Place the selected track in Palmier on its own audio track, set a sensible bed level under speech, trim to picture, and use fades where needed. Keep music out of the dialogue's intelligibility range.

### Open-licensed SFX

- Source SFX from a library whose specific file license allows the intended use. Record attribution and license in the ledger. Prefer CC0/public-domain or explicit commercial-use permissions; check each file, not only the site-wide description.
- Use `yt-dlp` only if that SFX source explicitly permits it. Don't fetch sounds from short-form social posts.
- Add effects sparingly at actual edit points (impact, whoosh, tap, room tone); audition them with the edit and reduce them so they support rather than mask speech.

## 5. Palmier setup and repeatability

1. For an external MCP session, call `manage_project({ action: "list" })` before any timeline operation. Select the intended project explicitly. If none is open, use `manage_project({ action: "open", id: "<listed project id>" })` only when the creator has identified the project, or create a new project if they asked for one. For an in-app Agent, use the project already open in that conversation. Do not open a merely plausible project based on its name.
2. Call `get_timeline()` and note project fps, width, height, duration, tracks, and `canGenerate`. If generation is needed and `canGenerate` is false, stop generation and explain the account gate; editing/importing can continue.
3. Set the project to 9:16, normally 1080×1920, **before placing clips** with `set_project_settings({ aspectRatio: "9:16", quality: "1080p" })` when needed. Use project fps from `get_timeline`; never assume it. Changing project settings refits existing clips, so inspect framing after changing them.
4. `get_media()` and label inputs by role (A-roll, b-roll, product, logo, licensed music, SFX). `inspect_media({ mediaRef, overview: true })`; for dialogue-driven edits, inspect word timestamps and read the transcript before cutting.
5. Build a source map from reference beats to creator footage. Record source IDs, source in/out in seconds, timeline start frames, track roles, mute state, and any layout/caption settings in an edit recipe stored alongside the project (for example `templates/reel-recipe.md` in this package). Use stable role names rather than relying on imported filenames.
6. Place A-roll first; use `source: [startSeconds, endSeconds]`. In Palmier, timeline positions are project frames and source trims are seconds. Omit `trackIndex` when auto-creating a new track; index 0 renders on top. Follow the installed `ugc-editing` skill if available for cut, layout, and caption procedures; otherwise use the tool semantics in the current Palmier docs.
7. Cut dead air and retakes before captions. Re-read transcript after each word-cut pass because indices shift. Keep meaning and natural phrase joins.
8. Recreate beat timing with creator footage. Use `apply_layout` for crop/layout changes; split clips at boundaries before applying layouts to only part of a shot. Add b-roll to separate tracks where it should overlay, and mute linked b-roll audio. Apply captions after picture/speech edits; place them within platform-safe margins.
9. Add music/SFX only after picture rhythm is stable. Keep licensed downloadable music, platform-native trend placeholder, and SFX as separate, clearly named tracks.
10. Save a recipe with project settings, tool choices, source spans, beat durations, text style, levels, transitions, and rights ledger. For recurring content, leave variable fields for new footage/script while preserving the fixed style values. Recompute source timing from each new transcript; never reuse stale clip IDs or word indices. Keep any imported local source files in place until Palmier confirms they are stored in its managed media library.

## 6. Quality review and delivery

Do not call the result finished until all checks below have evidence:

- `inspect_timeline({ startFrame, endFrame, maxFrames })` samples the hook, each major transition, caption moments, and ending. Confirm 9:16 crop, no black gaps, no accidental overlaps/overwrites, no stretched source, legible captions, and that the ending resolves or loops as intended.
- Inspect the full timeline and compare its beat sheet against the reference: order, rough beat durations, visual variety, caption behavior, and transition style. Keep the user's message and identity original.
- Listen to dialogue, music, and SFX together. Confirm speech is intelligible, cuts have no clicks or missing words, and levels/fades are smooth. If audio playback isn't available, state that the audio pass remains unverified.
- Confirm every third-party asset has a ledger entry and permitted-use evidence. Confirm viral sound is a platform-native recommendation/placeholder rather than an extracted file.
- Confirm the timeline is vertical and its duration is within the requested target. If the creator explicitly asked for an export/deliverable, use Palmier's available export workflow, inspect the terminal export result and artifact, and don't claim a file exists until it is visible in the output/library. If they did not request an export, leave the reviewed edit in Palmier and ask whether they want a file exported.
- Deliver the reviewed Palmier project/edit plus concise notes: reference URL, observed vs estimated details, substitutions, music/SFX licensing, how to add a platform-native sound, and what was checked.

## Repeatability rules

- Each run begins from a fresh `get_timeline()` and `get_media()`; use deltas returned by mutations and refresh state after failures or outside edits.
- Store one canonical recipe per series. Keep constants (canvas, caption style, track roles, recurring transitions) in one place; derive variable timings and footage selections from the new script/reference.
- Never apply the template by blindly replaying old IDs or frame positions. Re-map source footage and recalculate frames at the current project fps.
- Before final delivery, compare the edit to both the recipe and the new reference breakdown. Explain any intentional deviation.
