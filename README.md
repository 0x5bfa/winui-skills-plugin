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
skills/winui-development/references/
                                   WinUI reference notes and migration checklist
```

## Codex Installation

Use this repository as a local Codex plugin:

```bash
git clone https://github.com/0x5bfa/winui-skills-plugin.git
```

Then install or register it through your Codex plugin workflow. The manifest lives at:

```text
.codex-plugin/plugin.json
```

## Starter Prompts

- "Review this WinUI 3 view and view model for threading, lifetime, and XAML issues."
- "Migrate this UWP/WinUI 2 page to WinUI 3 with Windows App SDK."
- "Create a production-ready WinUI 3 settings page using MVVM."

## Source Notes

The skill is intentionally docs-linked instead of pretending to freeze Microsoft guidance forever. Key official sources are Microsoft Learn pages for WinUI, WinUI 3, Windows App SDK migration, and WinUI/windowing documentation.
