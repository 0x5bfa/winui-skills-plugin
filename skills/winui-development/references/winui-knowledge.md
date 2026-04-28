# WinUI Knowledge Notes

These notes are a compact agent reference, not a replacement for Microsoft Learn.

## WinUI 2

WinUI 2 is the UWP-focused version of the Windows UI Library. It provides newer Fluent controls and styles for UWP apps through `Microsoft.UI.Xaml` packages while the application model remains UWP.

Common signals:

- UWP project structure and `Package.appxmanifest`.
- `Windows.UI.Xaml` app/page/window infrastructure.
- `Microsoft.UI.Xaml.Controls` for WinUI library controls.
- UWP lifecycle, activation, storage, app services, background tasks, and app identity assumptions.

Good agent behavior:

- Preserve UWP constraints unless the task is migration.
- Check target/min Windows versions before suggesting APIs.
- Keep XAML resource dictionaries, theme dictionaries, and visual states compatible with UWP.

## WinUI 3

WinUI 3 is the modern native UI framework delivered with the Windows App SDK for Windows desktop apps.

Common signals:

- `Microsoft.WindowsAppSDK` package reference.
- `Microsoft.UI.Xaml` namespaces for app UI.
- `MainWindow.xaml` deriving from `Microsoft.UI.Xaml.Window`.
- Desktop target framework such as `netX.0-windows10.0.17763.0` or later.
- Packaged MSIX project or unpackaged runtime/deployment setup.

Good agent behavior:

- Treat it as desktop, not UWP.
- Be explicit about window ownership and HWND interop.
- Use `DispatcherQueue` for UI scheduling.
- Consider packaged versus unpackaged behavior.
- Avoid APIs that assume `CoreWindow` unless the project has an adapter.

## C# Patterns

Common production patterns:

- MVVM with `INotifyPropertyChanged`, commands, and dependency-injected services.
- CommunityToolkit.Mvvm source generators.
- Async command patterns with cancellation and exception reporting.
- Code-behind for view-only behavior, event bridging, and one-off UI interactions.

Review risks:

- Blocking async work on the UI thread.
- Mutating observable collections off the UI thread.
- Forgetting to unsubscribe from events or timers.
- Binding to mutable models without change notification.
- Putting business logic in XAML converters.

## C++/WinRT Patterns

Common production patterns:

- `.idl` files for WinRT components.
- `winrt::implements`, generated headers, and `InitializeComponent`.
- `IAsyncAction`, `IAsyncOperation<T>`, and coroutine-based async.
- XAML code-behind with generated partial types.

Review risks:

- Lifetime bugs from captured `this`.
- Missing apartment/thread awareness.
- Incorrect generated file assumptions.
- ABI/type mismatch between XAML and implementation.

## XAML Review Checklist

- Resource keys exist for all themes.
- Text is localizable and not hardcoded where localization matters.
- Controls have accessible names or labels.
- High contrast remains usable.
- `x:Bind` has the correct mode and update path.
- `DataContext` is intentionally set.
- Layout handles DPI, text scaling, localization expansion, and window resizing.
- `VisualStateManager` states are reachable and do not conflict.
- `ItemsRepeater`, `ListView`, and `GridView` virtualization is preserved for large lists.

## Packaging And Deployment

Check these before making deployment claims:

- Packaged MSIX, sparse package, or unpackaged app.
- Windows App Runtime version and deployment strategy.
- Processor architecture and RID.
- Store distribution requirements.
- App identity requirements for APIs.
- File/protocol activation and notification setup.

## Official Sources

- https://learn.microsoft.com/windows/apps/winui/
- https://learn.microsoft.com/windows/apps/winui/winui3/
- https://learn.microsoft.com/windows/apps/windows-app-sdk/
- https://learn.microsoft.com/windows/apps/develop/ui-input/windowing-overview
