# WinUI 2 / UWP To WinUI 3 Migration

Use this reference for migrating UWP or WinUI 2 UI code to WinUI 3 with the Windows App SDK.

## Migration Phases

1. Inventory the app model, project files, packages, target versions, capabilities, and deployment path.
2. Create the Windows App SDK project shape before moving code.
3. Move UI namespaces deliberately from `Windows.UI.Xaml` to `Microsoft.UI.Xaml`.
4. Replace UWP lifecycle, activation, window, and dispatcher assumptions.
5. Rework dialogs, pickers, popups, sharing, and notifications.
6. Validate packaging, activation, theme resources, accessibility, and deployment.

## High-Risk Replacements

- `Window.Current` -> explicit window ownership or injected window service.
- `CoreDispatcher.RunAsync` -> `DispatcherQueue.TryEnqueue`.
- `CoreWindow` -> `Window`, `AppWindow`, HWND interop, or window service.
- UWP activation overrides -> Windows App SDK app lifecycle and activation handling.
- UWP-only extension points -> Windows App SDK, Win32, or feature removal.

## Do Not

- Do not run a blind global namespace replacement.
- Do not assume every UWP contract has a Windows App SDK equivalent.
- Do not leave picker and dialog ownership implicit.
- Do not postpone packaged versus unpackaged decisions until the end.

## See Also

`migration-winui2-to-winui3.md` contains the fuller checklist.
