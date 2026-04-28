# WinUI 2 / UWP To WinUI 3 Migration Checklist

Use this checklist when moving UWP or WinUI 2 UI code to WinUI 3 with the Windows App SDK.

## 1. Inventory Before Editing

Capture:

- Project type, language, target framework, Windows target/min versions.
- NuGet/package references, especially `Microsoft.UI.Xaml` and `Microsoft.WindowsAppSDK`.
- App startup and activation flow.
- Navigation root, shell, pages, dialogs, flyouts, and popups.
- Background tasks, app services, notifications, file/protocol activation, share target, and app extensions.
- Storage, settings, permissions/capabilities, and identity-dependent APIs.
- Native interop, P/Invoke, C++/WinRT components, and XAML Islands.

## 2. Project Model

Plan:

- Create or update a Windows App SDK project.
- Decide packaged versus unpackaged early.
- Move assets, resources, app manifest settings, and packaging configuration deliberately.
- Recreate app lifecycle hooks instead of copying UWP startup code wholesale.

## 3. Namespaces And XAML

Common work:

- Move UI types from `Windows.UI.Xaml` to `Microsoft.UI.Xaml` where appropriate.
- Keep non-UI WinRT APIs only when they are supported in the new app model.
- Update XAML namespace declarations.
- Recheck merged dictionaries, theme resources, and default styles.
- Rework resource lookup if resources moved from page-level to window/app-level dictionaries.

Avoid:

- Blind global search-and-replace across all `Windows.*` namespaces.
- Assuming every UWP extension point has a direct Windows App SDK equivalent.

## 4. Window And Dispatcher Changes

Expected replacements:

- `Window.Current` -> explicit app/window reference such as `App.MainWindow` or an injected window service.
- `CoreDispatcher.RunAsync` -> `DispatcherQueue.TryEnqueue` or a dispatcher abstraction.
- `CoreWindow` assumptions -> `Window`, `AppWindow`, HWND, or platform interop.

Review:

- Multi-window ownership.
- Dialog ownership.
- UI-thread marshaling.
- App shutdown and window lifetime.

## 5. Dialogs, Pickers, Popups, And Sharing

Many UI-adjacent WinRT objects need explicit association with the WinUI 3 window.

Check:

- `ContentDialog.XamlRoot`.
- Popup/flyout placement and `XamlRoot`.
- File/folder pickers initialized with the window HWND.
- `MessageDialog` ownership.
- `DataTransferManager` association with the window.

## 6. Controls And Visual Behavior

Re-test:

- NavigationView pane behavior.
- TeachingTip, InfoBar, CommandBar, MenuBar, and flyouts.
- Acrylic/Mica/material usage.
- VisualStateManager states.
- Pointer, keyboard, focus, and access key behavior.
- Text scaling and high contrast.

## 7. App Services And Platform Features

For each UWP feature, decide whether to:

- Keep it as a supported WinRT API.
- Replace it with a Windows App SDK API.
- Replace it with Win32/.NET functionality.
- Drop it or put it behind a packaged-only feature gate.

Pay special attention to:

- Background tasks.
- Live tiles.
- Toast/app notifications.
- Share contracts.
- App extensions.
- File/protocol activation.
- App settings and local storage paths.

## 8. Validation

At minimum:

- Build the migrated project.
- Launch packaged and/or unpackaged target as applicable.
- Exercise navigation and app activation paths.
- Open every dialog, picker, popup, and flyout.
- Test theme switching, high contrast, and text scaling.
- Verify deployment on a clean machine or VM when packaging changed.

## Microsoft Migration Anchors

Official Microsoft guidance highlights several recurring differences:

- `Window.Current` is not supported in Windows App SDK apps.
- `CoreDispatcher.RunAsync` migrates to `DispatcherQueue.TryEnqueue`.
- Some dialogs, pickers, and transfer APIs need explicit window/HWND association.
- `ContentDialog` and `Popup` may need `XamlRoot`.
- Visual State Manager and page resources may need refactoring.
- Acrylic behavior differs from UWP.

Source: https://learn.microsoft.com/windows/apps/windows-app-sdk/migrate-to-windows-app-sdk/guides/winui3
