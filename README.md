# Team Elevation — Command Center Tools

Static tools hub published with GitHub Pages, styled to match the Command Center
(navy `#1B2A4A` / Transamerica red `#E5421F`).

**Live:** https://dwightrfm.github.io/team-elevation/

| Path | Tool | Source of truth |
|---|---|---|
| `/` | Hub | this repo |
| `/referral/` | Referral Engine | `~/Paul/referral_system.html` |
| `/smd/` | SMD Toolkit (RFM SpeedZone 2026) | `~/baseshop-coordinator/smd/speedzone_toolkit.html` |

## How it works

No build step. Plain HTML with inline CSS and JS, served from `main` at the repo root,
the same setup as `dwightrfm/ccs-band`. Each tool persists to `localStorage` in whatever
browser opens it, so data does not sync between devices. Use the Export button inside a
tool to move it.

## Command Center integration

The Command Center (`dwightrfm/command-center`, runs locally on :8080) embeds both tools as
tabs via `src/components/command-center/ToolFrame.tsx`, which iframes these Pages URLs. Same
origin as the standalone site, so the `localStorage` is shared: log a touch in the Command
Center tab and it shows up on the public page, and the other way round.

The Command Center itself cannot go on Pages. It needs its bun API server on :3001.

## Updating a tool

Edit the source file, copy it over, push:

```bash
cp ~/Paul/referral_system.html ~/team-elevation/referral/index.html
cd ~/team-elevation && git add -A && git commit -m "update referral engine" && git push
```

The SMD toolkit is the one exception. Its copy here has been recolored from the original
black/crimson SpeedZone palette to Command Center navy/red. Recopying from source will
undo that. The recolor lives entirely in the `:root` block plus a handful of hardcoded
hex values, so it is quick to reapply.

## Notes

- `robots.txt` disallows all crawlers and every page carries `noindex`. This keeps the
  site out of search results. It does **not** make the site private. GitHub Pages is
  publicly readable, including on private repos. Anyone with a URL can read anything here.
- `/referral/` ships with real contact data baked into the file.
