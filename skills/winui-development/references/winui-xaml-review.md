# WinUI XAML Review

Use this reference for XAML, resources, visual states, layout, accessibility, and binding review.

## First Pass

- Identify whether XAML uses `Windows.UI.Xaml` or `Microsoft.UI.Xaml`.
- Check `x:Bind` versus `{Binding}` and whether update modes are intentional.
- Find resource dictionaries, theme dictionaries, merged dictionaries, and default styles.
- Check whether controls are page-level, app-level, or window-level resources.

## Checklist

- Text is localizable where product UI requires localization.
- Interactive controls have accessible names or labels.
- High contrast has usable resources and does not rely only on color.
- Layout handles text scaling, DPI, long localized strings, and window resizing.
- `VisualStateManager` states are reachable and do not fight layout constraints.
- Large lists preserve virtualization.
- Converters are simple presentation adapters, not business logic containers.
- `DataContext` is set intentionally and does not break nested templates.

## WinUI 3-Specific Checks

- `ContentDialog.XamlRoot` is set where needed.
- Popups, flyouts, and teaching tips are associated with the correct visual root.
- Window-level resources are available to pages after migration.
- Acrylic, Mica, and theme resources are tested in light, dark, and high contrast.

## Review Output

Prioritize findings by user-visible impact:

1. Crashes or broken interaction.
2. Accessibility and localization blockers.
3. Binding/resource bugs.
4. Layout and visual polish.
5. Maintainability.
