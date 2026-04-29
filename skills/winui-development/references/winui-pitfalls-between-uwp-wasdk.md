# UWP And Windows App SDK Pitfalls

Use this reference when comparing UWP, WinUI 2, WinUI 3, and Windows App SDK behavior.

## App Model Differences

- UWP has a sandboxed app model with UWP lifecycle, package identity, capabilities, and platform XAML.
- WinUI 2 adds newer controls to UWP but does not change the UWP app model.
- WinUI 3 uses Windows App SDK and desktop app behavior with WinUI XAML.
- Windows App SDK apps may be packaged, unpackaged, or sparse-packaged.

## Frequent Pitfalls

- Treating WinUI 3 as UWP because both use XAML.
- Treating WinUI 2 as desktop because it uses `Microsoft.UI.Xaml.Controls`.
- Assuming `Window.Current`, `CoreWindow`, or `CoreDispatcher` exist in WinUI 3.
- Forgetting `XamlRoot` for dialogs and popups.
- Forgetting HWND initialization for pickers and some WinRT UI APIs.
- Using package-identity APIs from an unpackaged app.
- Assuming UWP background tasks, live tiles, or share contracts migrate directly.
- Copying resource dictionaries without checking lookup scope.

## Agent Rule

When a fix crosses app models, state the app model assumption explicitly before editing code.
