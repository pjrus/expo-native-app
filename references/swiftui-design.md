# SwiftUI design and behavior examples

Before choosing controls, use the app's installed Expo SDK to open its SwiftUI component index and the individual component pages. These examples describe the intended behavior. Verify the component, modifiers, and OS support against that SDK. Use the [Expo SwiftUI index](https://docs.expo.dev/versions/latest/sdk/ui/swift-ui/) to discover components and the [Apple Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/) to check interaction conventions.

## Choose native controls for the job

| Interaction | SwiftUI on iOS | Android counterpart |
| --- | --- | --- |
| One selection from a few short options | Segmented `Picker` | Single-select segmented buttons |
| One selection from many options | Menu-style `Picker` or a list of options | Dropdown or selection list |
| Secondary or contextual actions | `Menu` or `ContextMenu` | Overflow or contextual menu |
| Confirm a consequential action | `ConfirmationDialog` or `Alert` | Alert dialog |
| Edit preferences or enter data | `Form` or inset-grouped `List` with `Section`, using controls like `Toggle`, `TextField`, and `DatePicker` | Grouped Material rows, switches, text fields, and date pickers |

## Screen examples

- **Settings.** Put preferences in native sections with aligned labels and toggles. Show one row per setting. Use the native stack title and reserve a footer for information that explains a choice. Verify that the label remains readable at larger text sizes and that the switch exposes its current state.
- **Filterable list.** Place a segmented picker above the list for short options like All, Open, and Closed. Use a menu when labels get long. Keep the selection visible and update the rows in place. Show a concise empty state when the selected filter has no results.
- **Create item.** Use native inputs in a grouped form. On a multi-step flow, keep the progress position and main action consistent and retain the draft when users go back. Put short review values in aligned rows and let descriptions wrap at full width. Keep the action reachable with the keyboard open and identify what needs correcting before users can continue.

## Host the layout

Build a coherent SwiftUI subtree for an iOS screen or section inside a sized `Host`. Use content sizing for intrinsically sized controls and give scrolling content a bounded viewport along its scroll axis. Keep SwiftUI imports in the iOS variant and share state and callbacks with the other platforms. Use `RNHostView` when a specialized React Native view needs to sit inside SwiftUI. See the [Expo Host reference](https://docs.expo.dev/versions/latest/sdk/ui/swift-ui/host/).
