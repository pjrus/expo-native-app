---
name: expo-native-app
description: Initialize a new Expo app for iOS and Android. Use only when asked to create, bootstrap, or scaffold a new Expo app, including initial setup from a starter template. Do not trigger for features, fixes, redesigns, or upgrades in an existing app.
---

# Expo apps for iOS and Android

## Confirm initialization scope

Use this workflow when the user is starting a new Expo app, including one in an existing repository or from a starter template. If invoked for ongoing work on an established app, skip this workflow and follow that project's instructions. Treat the first scaffold, project conventions, and initial documentation as the scope of this skill.

## Start with the project and live guides

1. Read any existing project instructions and inspect the target directory for a starter scaffold.
2. Fetch fresh [Expo agent instructions](https://docs.expo.dev/agents.md) and the [Expo documentation index](https://docs.expo.dev/llms.txt) on every initialization. Read the current **Create a project** guide and any task-specific guides. Follow the stable template and package-manager instructions, including any SDK transition guidance.
3. Read the generated manifest or the starter's manifest to identify the Expo SDK major. Use the lockfile or installed package if the range is ambiguous. Open `https://docs.expo.dev/versions/v<major>.0.0/` and the matching reference pages before writing feature code. Verify imports, platform support, minimum OS versions, and development-build requirements. Use the installed React Native version's official reference for React Native APIs.
4. For platform design choices, open the relevant [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/) and [Android design guidance](https://developer.android.com/design). Link the specific guides used in the handoff and identify the SDK. If a fetch fails, try another official format or versioned source. Report any remaining gap and continue with work independent of the unverified API.

## Clarify new app scope

If the prompt leaves the app's purpose, intended users, core flows, or first-version scope unclear, ask the user a few focused questions before scaffolding or implementing the parts that depend on those answers. Ask only about gaps that would materially change the app. Group related questions, use plain language, and offer concrete options when helpful. Continue with independent work, such as checking the current Expo guides, while waiting for answers.

If the brief already establishes the scope, proceed. When offline use, accounts, sync, or distribution would change the initial scaffold, clarify the relevant choices. Resolve routine implementation details using the project's conventions. Record the agreed scope and setup decisions in `product.md`, put unresolved choices under Open product decisions, and document the implemented setup in `ARCHITECTURE.md`.

## Document a new repository

When initializing the new Expo app, write these files at the app repository root as part of scaffolding:

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

## Plan first-use permissions

When an in-scope feature needs camera, location, notifications, or another device permission, read the current [Expo permissions guide](https://docs.expo.dev/guides/permissions/) and the SDK-matched module reference. Check the native configuration and runtime behavior on each target platform. Request only the access the feature needs.

Define the action that triggers the prompt and explain the benefit in context. Default to asking when the user starts the feature. Use a first-launch prompt only when access is needed for the initial task and the reason is clear. Decide what stays usable after denial, provide an alternative where practical, and offer a way to recover if access is needed later. When the platform can no longer prompt, explain how to enable access in Settings. Record the trigger, rationale, fallback, and recovery in `DESIGN.md`.

## Install and verify

Use the project runner (`bunx` with a Bun lockfile, otherwise follow the repository convention). Install dependencies through `expo install` for SDK compatibility. For projects using Continuous Native Generation, configure native behavior through app configuration and config plugins. Build a development client when the native dependency or configuration requires it. For requested cloud builds, submissions, or updates, fetch the task-specific EAS guide before choosing commands.

## First-run acceptance checklist

- **Match the brief.** For a UI prototype, make the primary flow navigable with sample data. For a functional prototype, implement and exercise the smallest complete user flow with real behavior. Verify state survives a relaunch when persistence is in scope. For a scaffold-only brief, verify that the starter screen launches.
- **Start cleanly.** Remove unused starter screens and assets, configure the app's name and identity from the brief, and verify the README's install and launch commands from a fresh checkout or clean copy. Run the project's lint and TypeScript checks.
- **Check both platforms.** Launch on an iOS Simulator and an Android Emulator or representative devices. Check the first screen in light and dark mode, at larger text sizes, and around safe areas. Exercise keyboard behavior, modal dismissal, and platform back navigation where relevant. Check Metro and runtime logs. Capture one screenshot per platform when devices are available.
- **Verify permission flows where applicable.** On both target platforms, test the initial prompt, grant and denial, and returning to the feature after denial. Use a build that reflects the app's native permission configuration.
- **Report the result.** State which flows and platforms you verified, share the screenshots you captured, and identify any checks you could not run.
