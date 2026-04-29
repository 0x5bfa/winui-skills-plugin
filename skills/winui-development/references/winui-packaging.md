# WinUI Packaging

Use this reference when the task involves MSIX, Windows App SDK runtime deployment, Store packaging, app identity, activation, or install/update behavior.

## Classify Deployment

- UWP app package.
- WinUI 3 packaged MSIX.
- WinUI 3 unpackaged app.
- Sparse package with external location.
- Desktop bridge or mixed packaging.

## Check Early

- Target framework and runtime identifier.
- Processor architecture.
- Windows App SDK package version.
- Self-contained versus framework-dependent deployment.
- App identity requirements.
- Store, enterprise, or direct distribution.
- File/protocol activation, notifications, and capabilities.

## Common Risks

- Using identity-dependent APIs from an unpackaged app.
- Forgetting Windows App Runtime deployment for unpackaged apps.
- Testing only on a developer machine with Visual Studio installed.
- Mismatched architecture between app, package, and native dependencies.
- Missing manifest capabilities after migration.
- Assuming UWP activation maps directly to Windows App SDK activation.

## Validation

- Build package artifacts.
- Install on a clean machine or VM.
- Launch from Start menu and command line where applicable.
- Test activation paths.
- Test upgrade and uninstall behavior.
- Verify runtime dependencies are present without Visual Studio.
