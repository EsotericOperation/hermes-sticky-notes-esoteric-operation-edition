# Hermes Sticky Notes — Esoteric Operation Edition

Fork of [VGFreakXBL/hermes-sticky-notes](https://github.com/VGFreakXBL/hermes-sticky-notes) with EO-themed enhancements.

In-Desktop sticky / post-it notes for **[Hermes Desktop](https://hermes-agent.nousresearch.com/)**, built as a single disk plugin (no app fork, no build step).

One **stack** on the glass. **Break out** notes when they need ambient space. **Drag floats together** to pile them. **Stack all** when the desk gets loud.

## What's new in this fork

- **EO namespace**: plugin id `eo-stickies`, storage key `eo-stickies:notes`
- **New tints**: `void`, `relic`, `gilt` alongside the original `classic`, `soft`, `ghost`
- **Auto-tagging**: notes are tagged on creation/migration by EO keyword rules (`broadcast`, `ritual`, `ops`, `audio`, `agent`, `divination`, `vibe`, `todo`)
- **Auto-tint**: content-aware tint selection based on keyword rules
- **Timeline view**: chronological note history with tags, available via palette, keybind (`mod+shift+t`), or `/sticky timeline`
- **Tag rendering**: tags show inline in stack rows
- **Chat commands**: `/sticky create [--tint NAME] <text>`, `/sticky list`, `/sticky search <query>`, `/sticky dump`, `/sticky tags`, `/sticky purge <id>`, `/sticky clear`
- **Local mirror**: notes also written to `~/.hermes/scripts/eo-stickies/notes.json` for CLI/agent access
- **Renamed palette/keybind categories**: everything lives under `EO Stickies`

## Install

Requires **Hermes Desktop** (the Electron app). CLI/gateway alone will not load this.

```bash
mkdir -p ~/.hermes/desktop-plugins/eo-stickies
cp plugin.js ~/.hermes/desktop-plugins/eo-stickies/plugin.js
```

Then in Desktop:
1. **⌘K → Reload desktop plugins** (or wait a few seconds for the file watcher)
2. **Settings → Plugins** → enable **EO Stickies** if it’s off
3. Look for the status chip `sticky` and the floating **stickies** stack card

Named profiles: install under `~/.hermes/profiles/<name>/desktop-plugins/eo-stickies/` instead when that profile is active.

## How to use

| Action | How |
|--------|-----|
| New sticky | Status chip, stack **New**, palette **Sticky: New (stack)**, or `⌘⇧N` |
| Edit | Select a row in the stack; body autosaves |
| Break out | **↗** on a stack row or **Break out** in the editor |
| Pile | Drag free breakout windows until they **overlap ~40%**, then **release** |
| Flip inside a pile | Click a row in the pile list |
| Split from pile | **↗** on a pile row |
| Return one to stack | **↙ stack** on a breakout, or **↙** in a pile |
| Stack everything | **Stack all** / `⌘⇧S` / palette |
| Timeline | **Sticky: Timeline** palette / `⌘⇧T` |
| Clear all | Palette **Sticky: Clear all** (destructive) |

`⌘⇧N`
`⌘⇧S`
`⌘⇧T`

Notes persist in plugin-scoped storage (`ctx.storage`), profile-aware. No real filesystem access.

## Chat commands

From any Hermes chat surface:

```
/sticky create [--tint NAME] <text>
/sticky list
/sticky search <query>
/sticky dump
/sticky tags
/sticky purge <id>
/sticky clear
```

Valid tints: `classic`, `soft`, `ghost`, `void`, `relic`, `gilt`.

## Design notes

- One stack card by default (not one float per note)
- Overlap-merge only after a real drag (not on plain clicks)
- Short grace after split so notes aren’t immediately re-piled
- Themes: no hardcoded colors — uses app CSS variables
- Disk plugin rules: `jsx()` / `jsxs()` only; imports limited to `@hermes/plugin-sdk`, `react`, `react/jsx-runtime`

## Agent (best-effort)

If the gateway event payload includes plain text, markers like these may create notes:

```
/sticky remember to check the PR
[[sticky]]
Half-baked idea
body here
[[/sticky]]
```

Treat agent authoring as experimental — demo the manual UX first.

## Customize with Hermes

See [PROMPT.md](./PROMPT.md) for a rebuild / fork prompt you can paste into Hermes.

## License

MIT — see [LICENSE](./LICENSE).

Built against the Hermes Desktop Plugin SDK. Not affiliated with Nous Research beyond using the public plugin surface.
