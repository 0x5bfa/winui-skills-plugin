# WinUI Skills Plugin

Codex plugin skills for building, reviewing, and migrating Microsoft WinUI apps.

This repository is packaged as a Codex plugin with WinUI-focused skills.

## What It Covers

- WinUI 2 for UWP apps, including XAML controls, `Microsoft.UI.Xaml` package usage, and UWP-specific constraints.
- WinUI 3 with the Windows App SDK, including desktop project structure, windowing, packaging, deployment, and interop-sensitive APIs.
- Migration from WinUI 2/UWP-style apps to WinUI 3/Windows App SDK.
- Practical review rules for XAML, MVVM, async UI code, packaging, accessibility, high DPI, localization, trimming/AOT risk, and source generators.

## Repository Layout

```text
.codex-plugin/plugin.json          Codex plugin manifest
skills/winui-development/          Main Codex skill
skills/winui-development/agents/   PoC expert-mode prompts
skills/winui-development/references/
                                   Focused WinUI reference notes and migration checklists
```

## PoC Reference Modules

- `winui-architect.md`: architecture, MVVM, navigation, services, threading, and interop boundaries.
- `winui-xaml-review.md`: XAML review for resources, accessibility, localization, layout, and bindings.
- `winui-packaging.md`: MSIX, packaged/unpackaged deployment, Store, runtime, and identity concerns.
- `winui-migration-from-2-to-3.md`: UWP/WinUI 2 to WinUI 3 migration.
- `winui-migration-from-legacy-to-modern-uwp.md`: legacy UWP modernization while staying in UWP.
- `winui-pitfalls-between-uwp-wasdk.md`: common UWP versus Windows App SDK traps.

The `agents/` files are simple PoC role prompts for development and migration workflows. They are intentionally lightweight so the plugin can evolve without locking in too much structure too early.

## Codex Installation

Clone this repository, then use it as a local Codex plugin:

```bash
git clone https://github.com/0x5bfa/winui-skills-plugin.git
cd winui-skills-plugin
```

To add it directly as a Codex marketplace:

```bash
codex plugin marketplace add 0x5bfa/winui-skills-plugin
```

For local testing from a checkout:

```bash
codex plugin marketplace add /path/to/winui-skills-plugin
```

From this plugin repo, run:

```bash
python3 scripts/install-to-codex-repo.py /path/to/target/repo
```

That copies the plugin into:

```text
/path/to/target/repo/plugins/winui-skills-plugin
```

and creates or updates:

```text
/path/to/target/repo/.agents/plugins/marketplace.json
```

If the target repo already has this plugin, replace it with:

```bash
python3 scripts/install-to-codex-repo.py /path/to/target/repo --force
```

To preview paths without writing files:

```bash
python3 scripts/install-to-codex-repo.py /path/to/target/repo --dry-run
```

The Codex plugin manifest lives at `.codex-plugin/plugin.json`.

Manual install is also simple: copy this repository to `plugins/winui-skills-plugin` inside the target repo, then add this entry to the target repo's `.agents/plugins/marketplace.json`:

```json
{
  "name": "winui-skills-plugin",
  "source": {
    "source": "local",
    "path": "./plugins/winui-skills-plugin"
  },
  "policy": {
    "installation": "AVAILABLE",
    "authentication": "ON_INSTALL"
  },
  "category": "Developer Tools"
}
```

## Starter Prompts

- "Review this WinUI 3 view and view model for threading, lifetime, and XAML issues."
- "Migrate this UWP/WinUI 2 page to WinUI 3 with Windows App SDK."
- "Create a production-ready WinUI 3 settings page using MVVM."

## Source Notes

The skill is intentionally docs-linked instead of pretending to freeze Microsoft guidance forever. Key official sources are Microsoft Learn pages for WinUI, WinUI 3, Windows App SDK migration, and WinUI/windowing documentation.
