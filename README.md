# Expo Native App

This agent skill scaffolds polished iOS and Android apps with Expo. It activates during new app initialization and uses current Expo guides and API references that match the scaffold's SDK.

I’ve tuned the design defaults to my taste, including native controls, system navigation, and neutral dark themes. Fork it and make it your own. Change any of the design defaults, workflows, or templates to suit how you like to build.

## Install

Clone this repository into your agent's personal skills directory. Keep the checkout named `expo-native-app`.

| Agent | Checkout location | Invocation |
| --- | --- | --- |
| Codex | ~/.codex/skills/expo-native-app | `$expo-native-app` |
| Claude Code | ~/.claude/skills/expo-native-app | `/expo-native-app` |
| Antigravity | ~/.gemini/config/skills/expo-native-app | `/expo-native-app` |

For example, with Codex:

```sh
git clone https://github.com/pjrus/expo-native-app.git ~/.codex/skills/expo-native-app
```

## What the skill does

- Scaffolds new Expo apps using the current setup guide and documents the resulting project.
- Organizes navigation with Expo Router and shares feature logic across platform views.
- Favors SwiftUI controls on iOS and Jetpack Compose controls on Android where the SDK supports them.
- Uses a first-run checklist to verify clean setup, the initial user flow, and native UI on both platforms when devices are available.

New projects receive a [README](assets/README.template.md), an [architecture document](assets/ARCHITECTURE.template.md), [repository instructions for coding agents](assets/AGENTS.template.md), a [design guide](assets/DESIGN.template.md), and a [product brief](assets/product.template.md). The skill fills in the templates using the brief and the actual scaffold.

See [SKILL.md](SKILL.md) for the workflow and [SwiftUI design and behavior examples](references/swiftui-design.md) for iOS layouts and component choices.
