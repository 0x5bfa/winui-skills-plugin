# Legacy UWP To Modern UWP

Use this reference when modernizing a UWP app that is staying UWP, especially when moving away from older .NET Native assumptions toward modern .NET/UWP, CoreCLR, or Native AOT constraints.

## Identify First

- Current UWP target/min version.
- Language and project type.
- .NET Native usage and release build behavior.
- Reflection, serialization, source generators, and trimming-sensitive libraries.
- Store submission requirements.
- Native dependencies and architecture support.

## Modernization Goals

- Preserve UWP app model and package identity.
- Reduce .NET Native-specific workarounds where they are no longer needed.
- Make trimming and AOT behavior explicit.
- Update dependencies that assume old UWP or old WinRT projection behavior.
- Keep activation, capabilities, storage, and app services in the UWP model.

## Review Checklist

- Release builds behave like debug builds for serialization and reflection paths.
- Runtime directives or trimming descriptors are still needed and documented.
- Source generators replace reflection-heavy code where practical.
- Package manifest capabilities are still correct.
- Background tasks, app services, and activation paths still run under UWP constraints.
- Native dependencies support all required architectures.

## Output Shape

For modernization plans, separate:

1. Safe cleanup.
2. Runtime-sensitive changes.
3. Store/package validation.
4. Manual Windows-only verification.
