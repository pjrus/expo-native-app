# Repository instructions

This is an Expo and React Native app. See [Architecture](ARCHITECTURE.md) for the project layout, routes, platform boundaries, and state ownership.

## Scope

[Record the current development phase and any project-specific scope limits.]

## Check current Expo guides before editing

- Read the installed Expo major from the manifest and lockfile. Open `https://docs.expo.dev/versions/v<major>.0.0/` and the relevant API pages before using Expo or React Native APIs.
- Fetch the current [Expo agent instructions](https://docs.expo.dev/agents.md) and [Expo documentation index](https://docs.expo.dev/llms.txt). Read the task-specific guides, including EAS guidance when applicable.
- Use the repository's package manager and install Expo dependencies through `expo install`. For projects using Continuous Native Generation, configure generated native projects through app config and config plugins.

## Navigation and platform UI

- Keep Expo Router files thin and keep feature logic outside the route directory. Own shared state in platform-agnostic modules.
- On iOS, push dedicated full-page stack screens for forms and each step in a multi-step flow. Preserve drafts on Back and redirect invalid entry to a valid step. Use native dialogs or sheets for brief confirmations, contextual choices, and dismissible previews.
- Build iOS screen sections, forms, lists, and controls with SDK-supported SwiftUI. Use Jetpack Compose on Android where supported. Use a custom or shared control when native support or the interaction requires it. Isolate platform imports, size native hosts, and keep selection state and callbacks shared.
- Reuse the type scale in [Design](DESIGN.md) and keep eyebrow labels for context the heading does not convey. Use platform navigation and theme conventions. Preserve safe areas, system back behavior, text scaling, and accessible control labels.
- Update [Architecture](ARCHITECTURE.md) when routes, platform boundaries, or state ownership change.

## Verification

[Insert this repository's lint and TypeScript commands. Include any required tests.]

Exercise changed UI on iOS and Android. Check light and dark appearance, insets, text scaling, back navigation, and runtime errors. Report any device checks you could not run.
