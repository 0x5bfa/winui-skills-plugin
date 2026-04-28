---
name: winui-development
description: Build, review, debug, and migrate Microsoft WinUI apps, including WinUI 2 for UWP, WinUI 3 with Windows App SDK, and WinUI 2/UWP to WinUI 3 migration. Use when a user mentions WinUI, Windows App SDK, UWP XAML, Microsoft.UI.Xaml, XAML Islands, C#/WinRT, C++/WinRT, MSIX packaging, desktop windowing, or Fluent Windows UI.
---

# WinUI Development

Use this skill for production Windows UI work with WinUI 2, WinUI 3, and migrations between them.

## First Response Behavior

When a user asks for implementation or migration work:

1. Inspect the project files before assuming the app model.
2. Identify whether the app is WinUI 2/UWP, WinUI 3/Windows App SDK, Uno/MAUI-hosted XAML, or a mixed/interoperability project.
3. Check the target framework, Windows App SDK package version, `Microsoft.UI.Xaml` package usage, `Package.appxmanifest`, `.wapproj`, `.csproj`, `.vcxproj`, and XAML namespaces.
4. Keep changes aligned with the existing language and architecture: C# MVVM, C++/WinRT, code-behind, CommunityToolkit.Mvvm, ReactiveUI, Prism, or another established pattern.
5. Prefer small, verifiable edits over broad rewrites.

Ask a clarifying question only when the app model or migration target cannot be inferred safely.

## Project Identification Checklist

Treat these signals as important:

- WinUI 2/UWP: UWP project style, `TargetPlatformIdentifier` or UWP project files, `Package.appxmanifest`, `Windows.UI.Xaml`, and `Microsoft.UI.Xaml` NuGet package for newer controls/styles.
- WinUI 3: Windows App SDK package references, `Microsoft.WindowsAppSDK`, `Microsoft.UI.Xaml.Window`, `App.xaml`, `MainWindow.xaml`, desktop TFM such as `netX.0-windows10.0.x`, optional MSIX packaging, and Win32/HWND interop patterns.
- Packaged WinUI 3: MSIX packaging project, app identity, app manifest, app lifecycle, protocol/file activation, push notifications, app notifications, or Store distribution.
- Unpackaged WinUI 3: bootstrapper/runtime initialization concerns, deployment of Windows App Runtime, and limitations of identity-dependent APIs.
- C++/WinRT: `.idl`, `.vcxproj`, generated headers, `winrt::`, `xaml_typename`, `InitializeComponent`, and C++/WinRT async patterns.

## WinUI 2 Guidance

For WinUI 2 work:

- Remember that WinUI 2 is for UWP apps and supplements platform XAML with newer controls and styles.
- Preserve UWP app lifecycle assumptions unless the user is explicitly migrating.
- Check whether the project uses `Microsoft.UI.Xaml` controls while still relying on `Windows.UI.Xaml` app/window/page infrastructure.
- Be careful with minimum target platform versions and API availability checks.
- Validate visual states, resource dictionaries, theme resources, and high-contrast behavior.
- Avoid suggesting Win32-only APIs unless you are proposing a migration or an explicit desktop bridge/interoperability strategy.

## WinUI 3 Guidance

For WinUI 3 work:

- Treat WinUI 3 as part of the Windows App SDK and as a desktop app model, not UWP.
- Use `Microsoft.UI.Xaml` types for UI, pages, windows, controls, and XAML resources.
- Use `DispatcherQueue` for UI-thread scheduling.
- For APIs that need a window handle, obtain and pass the app window HWND deliberately.
- For dialogs, popups, and flyouts, set `XamlRoot` when required by the hosting context.
- Consider packaged versus unpackaged behavior before using identity-dependent Windows features.
- Keep windowing code explicit: `Window`, `AppWindow`, presenters, activation, size/position, and multi-window ownership.
- Prefer MVVM-friendly bindings and commands, but do not force MVVM into a small project that already uses simple code-behind consistently.

## Migration Guidance

When migrating WinUI 2/UWP-style code to WinUI 3:

1. Inventory app surface area before editing: project system, app lifecycle, pages, navigation, controls, storage APIs, background tasks, notifications, app services, identity-dependent APIs, and deployment.
2. Move UI namespaces and project references carefully. Do not blindly replace every namespace without checking whether it is a UWP-only API, a Windows App SDK API, or a WinRT API that remains available.
3. Replace `Window.Current` patterns with an explicit app window reference.
4. Replace `CoreDispatcher.RunAsync` with `DispatcherQueue.TryEnqueue` or an app-specific dispatcher abstraction.
5. Update UI APIs that require `XamlRoot`, HWND initialization, or `InitializeWithWindow`.
6. Rework activation, navigation startup, app settings, file/protocol handling, and lifecycle assumptions for desktop.
7. Re-test resources and visual states because top-level `Window` content and resource lookup can differ.
8. Validate deployment separately for packaged and unpackaged targets.

Use `references/migration-winui2-to-winui3.md` as the migration checklist.

## Code Review Rules

Prioritize issues in this order:

- UI-thread access, deadlocks, blocking `.Result`/`.Wait()`, and unsafe event lifetime.
- Incorrect app model assumptions between UWP, WinUI 2, WinUI 3, packaged, and unpackaged apps.
- XAML resource lookup, theme dictionaries, high contrast, localization, and accessibility.
- Binding errors, missing `INotifyPropertyChanged`, incorrect `x:Bind` mode, and command enablement.
- Window/dialog/picker initialization issues, especially HWND and `XamlRoot`.
- Memory leaks from event handlers, static references, timers, and long-lived view models.
- Packaging, deployment, architecture, RID, trimming, and Windows App Runtime version risks.

## Implementation Preferences

- Use existing project patterns and dependencies.
- Use CommunityToolkit.Mvvm only when the project already uses it or the user asks for it.
- Keep generated code and designer files untouched unless required.
- For XAML, prefer theme resources and existing styles over hardcoded colors.
- For controls, use semantic WinUI controls before custom drawing.
- For icons, use `FontIcon`, `SymbolIcon`, `PathIcon`, or existing app icon infrastructure consistently.
- Add comments only where WinUI interop or lifecycle behavior is non-obvious.

## Testing And Verification

For meaningful changes, try to run the closest available verification:

- `dotnet build` or Visual Studio/MSBuild equivalent for C# projects.
- `msbuild` or Visual Studio Build Tools for C++/WinRT projects.
- Unit tests when present.
- Manual launch instructions when local Windows UI execution is not available.

If the agent is running on macOS/Linux, say clearly that the build or launch may require Windows with Visual Studio and Windows App SDK workloads.

## Official References

When current accuracy matters, prefer official Microsoft sources:

- WinUI overview: https://learn.microsoft.com/windows/apps/winui/
- WinUI 3: https://learn.microsoft.com/windows/apps/winui/winui3/
- Create a WinUI 3 project: https://learn.microsoft.com/windows/apps/winui/winui3/create-your-first-winui3-app
- UI migration guide: https://learn.microsoft.com/windows/apps/windows-app-sdk/migrate-to-windows-app-sdk/guides/winui3
- Windowing overview: https://learn.microsoft.com/windows/apps/develop/ui-input/windowing-overview
- Windows App SDK release notes: https://learn.microsoft.com/windows/apps/windows-app-sdk/release-notes-archive
