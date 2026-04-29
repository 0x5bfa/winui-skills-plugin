# WinUI Architect

Use this reference when shaping a WinUI app, reviewing architecture, or deciding where code should live.

## Identify First

- App model: WinUI 2/UWP, WinUI 3 packaged, WinUI 3 unpackaged, XAML Islands, or mixed.
- Language stack: C#, C++/WinRT, or both.
- UI pattern: code-behind, MVVM, CommunityToolkit.Mvvm, ReactiveUI, Prism, or custom.
- Deployment target: Store, enterprise MSIX, sideloaded MSIX, unpackaged desktop, or hybrid.

## Architecture Defaults

- Keep view-only behavior in code-behind.
- Put state, commands, validation, and async workflows in view models or services.
- Hide app model differences behind small services when they affect many views.
- Keep window ownership explicit in WinUI 3.
- Use `DispatcherQueue` for WinUI 3 UI scheduling.
- Avoid global singletons for windows, navigation, and app state unless the app already uses that pattern deliberately.

## Review Checklist

- Navigation has a single owner and clear back-stack behavior.
- Services do not directly depend on XAML controls unless they are UI services.
- Async commands report errors and avoid blocking the UI thread.
- View models do not hold long-lived references to pages or controls.
- Multi-window behavior is either intentionally unsupported or explicitly modeled.
- Platform-specific APIs are gated by app model, OS version, package identity, or capability.

## Useful Output

When asked for architecture advice, return:

1. Current app model and architecture signals.
2. Risks or mismatches.
3. Smallest reasonable change.
4. Validation steps.
