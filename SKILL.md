---
name: expo-native-app
description: Design, scaffold, or extend Expo and React Native apps for iOS and Android using current official guides, Expo Router, shared feature logic, and platform-native controls. Use for new mobile apps and for screens or navigation in existing Expo projects.
---

# Expo apps for iOS and Android

## Start with the project and live guides

1. Read the applicable AGENTS.md, ARCHITECTURE.md, package manifest, lockfile, and a representative feature. Follow the project's current phase. For a design brief, describe the screen flow, interaction states, and platform controls with mock data. An explicit build request authorizes implementation within its scope.
2. **Fetch fresh documentation on every invocation**, including design-only tasks. Open [Expo's current agent instructions](https://docs.expo.dev/agents.md) and [documentation index](https://docs.expo.dev/llms.txt), then fetch and read the specific guides that apply. Search snippets and a previously fetched index are insufficient. Fetch additional guides as the task introduces new APIs.
3. For an existing app, read the major version of the `expo` dependency. Resolve ambiguous ranges or workspace dependencies from the lockfile or installed package. Open `https://docs.expo.dev/versions/v<major>.0.0/` and the matching reference pages for the packages and controls in use. Check platform support, imports, minimum OS versions, and development-build requirements. Use the installed React Native version's official reference for RN-specific APIs. Keep the SDK pinned unless upgrading is in scope.
4. For a new app, fetch the current **Create a project** guide from the index. Follow its stable template and package-manager instructions, including any SDK transition guidance. After scaffolding, read the generated manifest and apply the same version check before writing feature code.
5. For platform design choices, open the relevant [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/) and [Android design guidance](https://developer.android.com/design). Link the specific guides used in the handoff and identify the SDK. If a fetch fails, try another official format or versioned source. Report any remaining gap and continue with work independent of the unverified API.

## Document a new repository

When initializing a new app or repository, write these files at the app repository root as part of scaffolding:

- Use [the README template](assets/README.template.md) for `README.md`. Replace the generated starter README with app-specific setup, run, and verification instructions. Preserve any project-specific content that already exists.
- Use [the architecture template](assets/ARCHITECTURE.template.md) for `ARCHITECTURE.md`. Record the implemented layout, route graph, platform boundaries, and state ownership so future changes have a reference.
- Use [the agent instructions template](assets/AGENTS.template.md) for `AGENTS.md`. Record the repo's conventions and the live documentation workflow. Merge with existing agent instructions where present.

- Use [the design template](assets/DESIGN.template.md) for `DESIGN.md`. Record the visual system, reusable controls, and interaction and accessibility conventions for iOS and Android.
- Use [the product template](assets/product.template.md) for `product.md`. Capture the product purpose, intended users, primary flows, and the scope agreed for the current phase.

Read the bundled templates from the skill directory. Fill in the bracketed prompts from the product brief, design references, and the app's manifest, lockfile, configuration, and source tree. Record unresolved product or design decisions as open questions, then remove all template prompts. Verify commands against the project scripts and current official guides. Keep additional READMEs focused on setup or workflows that need their own documentation and link them from the root README. Before finishing, verify that all five root files exist, their links resolve, and their commands and paths match the scaffold.

## Organize by feature

- Use Expo Router. In a fresh project, keep routes and navigator layouts under `src/app/`. A route such as `src/app/settings.tsx` can simply re-export `SettingsScreen` from `src/features/settings/`. Preserve an existing project's route root. Put providers at the narrowest layout that owns their lifetime.
- Keep feature models, draft state, data access, and callbacks shared. A feature hook can expose the same selected value and change handler to `.ios.tsx`, `.android.tsx`, and a web-capable `.tsx` fallback. Reuse a shared view when the interaction is already native on both platforms.
- Keep common controls in `src/components/`, theme tokens in `src/constants/`, and fixtures in `src/data/` as needed. Give cross-feature state one owner. Keep state transitions independently testable. Update an existing architecture reference when navigation, state ownership, or platform boundaries change.

## Design the same flow for each platform

| Interaction | iOS | Android |
| --- | --- | --- |
| Select one short filter | Segmented picker | Single-select segmented buttons |
| Choose from longer labels | Menu-style picker | Exposed dropdown or selection dialog |
| Show actions or confirm a choice | Menu, context menu, or confirmation dialog | Overflow menu, bottom sheet, or alert dialog according to the action |
| Edit preferences | Inset-grouped sections with toggles | Grouped settings rows with switches |

- Prefer SwiftUI via `@expo/ui/swift-ui` on iOS and Jetpack Compose via `@expo/ui/jetpack-compose` on Android where the installed SDK supports them. Isolate platform imports. Give each native subtree a sized Host using documented content sizing or layout constraints. Embed React Native content inside a native tree only where needed.
- Use native tabs, headers, and back behavior. Preserve Android system back and iOS swipe-back across detail screens and dismissible presentations. Give a floating action button a distinct action.
- Use semantic foregrounds and system tint on iOS, Material theme colors on Android, and shared theme tokens for custom surfaces. For the reference project's dark palette, use neutral black and charcoal. Let native navigation provide system chrome. Gate optional glass on availability and Reduce Transparency.
- Preserve readable text at larger system font sizes, accessible labels and selection states, safe-area and system-bar insets, and keyboard access to form actions. For long collections, use a virtualized or native lazy list and stable item identifiers.

## Install and verify

Use the project runner (`bunx` with a Bun lockfile, otherwise follow the repository convention). Install dependencies through `expo install` for SDK compatibility. For projects using Continuous Native Generation, configure native behavior through app configuration and config plugins. Build a development client when the native dependency or configuration requires it. For requested cloud builds, submissions, or updates, fetch the task-specific EAS guide before choosing commands.

Run the project's lint and TypeScript checks after implementation. Exercise each changed flow on an iOS Simulator and an Android Emulator or representative devices. Check light and dark appearance, insets, text scaling, modal dismissal, platform back navigation, and Metro/runtime logs. Report which flows and platforms were exercised and identify unavailable checks explicitly.
