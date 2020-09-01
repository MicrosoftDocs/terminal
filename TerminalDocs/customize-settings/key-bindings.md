---
title: Windows Terminal Key Bindings
description: Learn how to create custom key bindings for Windows Terminal.
author: cinnamon-msft
ms.author: cinnamon
ms.date: 08/26/2020
ms.topic: how-to
ms.service: terminal
ms.localizationpriority: high
---

# Custom key bindings in Windows Terminal

> [!NOTE]
> If you are using [Windows Terminal Preview](https://aka.ms/terminal-preview) and want to customize commands in the command palette, additional information can be found on the [Command palette page](./../command-palette.md).

You can create custom key bindings (keyboard shortcuts) inside Windows Terminal that give you control of how you interact with the terminal using your keyboard.

## Key binding formats

Key bindings can be structured in the following formats.

- Commands without arguments:

    ```json
    { "command": "commandName", "keys": "modifiers+key" }
    ```

    For example, this default setting uses the <kbd>Alt</kbd>+<kbd>F4</kbd> shortcut key to close the terminal window:

    ```json
    { "command": "closeWindow", "keys": "alt+f4" }
    ```

- Commands with arguments

    ```json
    { "command": { "action": "commandName", "argument": "value" }, "keys": "modifiers+key" }
    ```

    For example, this default setting uses the <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>1</kbd> shortcut key to open a new tab in the terminal based on whichever profile is listed first in your dropdown menu (typically this will open the PowerShell profile):

    ```json
    { "command": { "action": "newTab", "index": 0 }, "keys": "ctrl+shift+1" }
    ```

### Key binding properties

As seen above, key bindings can be constructed using the following properties.

- **Command:** This is the command executed when the associated keys are pressed.
    - **Property name:** `command`
    - **Necessity:** Required
    - **Accepts:** String or action block (see below)
- **Keys:** This defines the key combinations used to call the command. Keys can have any number of modifiers with one key. Accepted modifiers and keys are listed [below](#accepted-modifiers-and-keys).
    - **Property name:** `keys`
    - **Necessity:** Required
    - **Accepts:** String or array of strings (in the form of `["string1", "string2", ...]`)

The action block is a JSON object consisting of the following name-value pairs:

- **Action:** This adds additional functionality to certain commands.
    - **Property name:** `action`
    - **Necessity:** Required
    - **Accepts:** String
- **Target:** The object on which the command operates. The value depends on the command.
    - **Property name:** `target`
    - **Necessity:** Contextual
    - **Accepts:** String
- **Index:** When the command operates on a collection of object, "index" indicates the item in the collection.
    - **Property name:** `index`
    - **Necessity:** Contextual
    - **Accepts:** Integer
- **Color:** For some commands, you can specify a color.
    - **Property name:** `color`
    - **Necessity:** Contextual
    - **Accepts:** String, in hex format: `"#rgb"` or `"#rrggbb"`

## Accepted modifiers and keys

The `keys` parameter has the following general format:

```XML  <!-- Well, not really XML, but the syntax highlighting is useful-->
[<Modifier1>+][<Modifier2>+][<Modifier3>+]<KeyName>
```

For `<Modifier1>`, `<Modifier2>`, and `<Modifier3>`, the following are acceptable:

| Type | Keys |
| ---- | ---- |
| Modifier keys | `ctrl`, `shift`, `alt` |

For `<KeyName>`, the following are acceptable:

| Type | Keys |
| ---- | ---- |
| Function and alphanumeric keys | `f1` through `f24`, `a` through `z`, `0` through `9` |
| Symbols | ``` ` ```, `-`, `=`, `[`, `]`, `\`, `;`, `'`, `,`, `.`, `/`, `plus` |
| Arrow keys | `down`, `left`, `right`, `up`, `pagedown`, `pageup`, `pgdn`, `pgup`, `end`, `home` |
| Action keys | `tab`, `enter`, `esc`, `escape`, `space`, `backspace`, `delete`, `insert` |
| Numpad keys | `numpad_0-numpad_9`, `numpad0-numpad9`, `numpad_add`, `numpad_plus`, `numpad_decimal`, `numpad_period`, `numpad_divide`, `numpad_minus`, `numpad_subtract`, `numpad_multiply` |

> [!IMPORTANT]
>
> - `=` and `plus` are equivalents. The latter must not be confused with `numpad_plus`.
> - Not all keyboards have function keys F13 through F24
> - `app` and `menu` are only available in [Windows Terminal Preview](https://aka.ms/terminal-preview/).

## Application-level commands

### Close window

:::row:::
:::column span="":::

- **Description:** This closes the current window and all tabs within it. If `confirmCloseAllTabs` is set to `true`, a confirmation dialog will appear to ensure you'd like to close all your tabs. More information on this setting can be found on the [Global settings page](./global-settings.md#hide-close-all-tabs-popup).
- **Command name:** `closeWindow`
- **Default binding:** <kbd>Alt</kbd>+<kbd>F4</kbd>

    ```json
    { "command": "closeWindow", "keys": "alt+f4" }
    ```

:::column-end:::
:::column span="":::
![Windows Terminal confirm close all tabs](./../images/confirm-close-all-tabs.png)

:::column-end:::
:::row-end:::

### Find

- **Description:** This opens the search dialog box. More information on search can be found on the [Search page](./../search.md).
- **Command name:** `find`
- **Default binding:** <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>F</kbd>

    ```json
    { "command": "find", "keys": "ctrl+shift+f" }
    ```

### Open the dropdown

- **Description:** This opens the dropdown menu.
- **Command name:** `openNewTabDropdown`
- **Default binding:** <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Space</kbd>

    ```json
    { "command": "openNewTabDropdown", "keys": "ctrl+shift+space" }
    ```

### Open settings files

- **Description:** This opens either the default or custom settings files. Without the `target` field, this will open the settings.json file.
- **Command name:** `openSettings`
- **Default binding:** <kbd>Ctrl</kbd>+<kbd>,</kbd> and <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>,</kbd>

    ```json
    { "command": "openSettings", "keys": "ctrl+," },
    { "command": { "action": "openSettings", "target": "defaultsFile" }, "keys": "ctrl+alt+," },
    ```

- **Action block arguments:**
    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `target` | Optional | `"settingsFile"`, `"defaultsFile"`, `"allFiles"` | The settings file to open. |

### Toggle full screen

- **Description:** This allows you to switch between full screen and default window sizes.
- **Command name:** `toggleFullscreen`
- **Default bindings:** <kbd>Alt</kbd>+<kbd>Enter</kbd> and <kbd>F11</kbd>

    ```json
    { "command": "toggleFullscreen", "keys": "alt+enter" },
    { "command": "toggleFullscreen", "keys": "f11" }
    ```

### Toggle focus mode

- **Description:** This allows you to enter "focus mode", which hides the tabs and title bar.
- **Command name:** `toggleFocusMode`
- **Default bindings:** _This command is not currently bound in the default settings_.

    ```json
    { "command": "toggleFocusMode", "keys": "" }
    ```

### Toggle always on top mode

- **Description:** This allows you toggle the "always on top" state of the window. When in "always on top" mode, the window will appear on top of all other non-topmost windows.
- **Command name:** `toggleAlwaysOnTop`
- **Default bindings:** _This command is not currently bound in the default settings_.

    ```json
    { "command": "toggleAlwaysOnTop", "keys": "" }
    ```

### Send input ([Preview](https://aka.ms/terminal-preview/))

- **Description:** Send arbitrary text input to the shell. As an example the input `"text\n"` will write "text" followed by a newline to the shell. ANSI escape sequences may be used, but escape codes like `\x1b` must be written as `\u001b`. For instance `"\u001b[A"` will behave as if the up arrow button had been pressed.
- **Command name:** `sendInput`
- **Default bindings:** _This command is not currently bound in the default settings_.

    ```json
    { "command": { "action": "sendInput", "input": "\u001b[A" }, "keys": "" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `input` | Required | String | The text input to feed into the shell. |

> [!IMPORTANT]
> This feature is only available in [Windows Terminal Preview](https://aka.ms/terminal-preview/).

## Tab management commands

### Close tab

- **Description:** This closes the current tab.
- **Command name:** `closeTab`
- **Default binding:** _This command is not currently bound in the default settings_.

    ```json
    { "command": "closeOtherTabs", "keys": "" }
    ```

### Close all other tabs ([Preview](https://aka.ms/terminal-preview/))

- **Description:** This closes all tabs except for the one at an index. If no index is provided, use the focused tab's index.
- **Command name:** `closeOtherTabs`
- **Default binding:** _This command is not currently bound in the default settings_.

    ```json
    { "command": { "action": "closeOtherTabs", "index": 1 }, "keys": "" }
    { "command": { "action": "closeOtherTabs", "index": null }, "keys": "" }
    { "command": "closeOtherTabs", "keys": "" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `index` | Optional | Integer | Position of the tab to be kept open. |

> [!IMPORTANT]
> This feature is only available in [Windows Terminal Preview](https://aka.ms/terminal-preview/).

### Close tabs after index ([Preview](https://aka.ms/terminal-preview/))

- **Description:** This closes the tabs following the tab at an index. If no index is provided, use the focused tab's index.
- **Command name:** `closeTabsAfter`
- **Default binding:** _This command is not currently bound in the default settings_.

    ```json
    { "command": { "action": "closeTabsAfter", "index": 1 }, "keys": "" }
    { "command": { "action": "closeTabsAfter", "index": null }, "keys": "" }
    { "command": "closeTabsAfter", "keys": "" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `index` | Optional | Integer | Position of the last tab to be kept open. |

> [!IMPORTANT]
> This feature is only available in [Windows Terminal Preview](https://aka.ms/terminal-preview/).

### Duplicate tab

- **Description:** This makes a copy of the current tab and opens it.
- **Command name:** `duplicateTab`
- **Default binding:**

    ```json
    { "command": "duplicateTab", "keys": "ctrl+shift+d" }
    ```

### New tab

- **Description:** This creates a new tab. Without any arguments, this will open the default profile in a new tab. If an action is not specified, the default profile's equivalent setting will be used.
- **Command name:** `newTab`
- **Default bindings:** <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>1</kbd> through <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>9</kbd>

    ```json
    { "command": "newTab", "keys": "ctrl+shift+t" },
    { "command": { "action": "newTab", "index": 0 }, "keys": "ctrl+shift+1" },
    { "command": { "action": "newTab", "index": 1 }, "keys": "ctrl+shift+2" },
    { "command": { "action": "newTab", "index": 2 }, "keys": "ctrl+shift+3" },
    { "command": { "action": "newTab", "index": 3 }, "keys": "ctrl+shift+4" },
    { "command": { "action": "newTab", "index": 4 }, "keys": "ctrl+shift+5" },
    { "command": { "action": "newTab", "index": 5 }, "keys": "ctrl+shift+6" },
    { "command": { "action": "newTab", "index": 6 }, "keys": "ctrl+shift+7" },
    { "command": { "action": "newTab", "index": 7 }, "keys": "ctrl+shift+8" },
    { "command": { "action": "newTab", "index": 8 }, "keys": "ctrl+shift+9" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `commandLine` | Optional | Executable file name as a string | Executable run within the tab. |
    | `startingDirectory` | Optional | Folder location as a string | Directory in which the tab will open. |
    | `tabTitle` | Optional | String | Title of the new tab. |
    | `index` | Optional | Integer | Profile that will open based on its position in the dropdown (starting at 0). |
    | `profile` | Optional | Profile's name or GUID as a string | Profile that will open based on its GUID or name. |

### Open next tab

- **Description:** This opens the tab to the right of the current one.
- **Command name:** `nextTab`
- **Default binding:** <kbd>Ctrl</kbd>+<kbd>Tab</kbd>

    ```json
    { "command": "nextTab", "keys": "ctrl+tab" }
    ```

### Open previous tab

- **Description:** This opens the tab to the left of the current one.
- **Command name:** `prevTab`
- **Default binding:** <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>Tab</kbd>

    ```json
    { "command": "prevTab", "keys": "ctrl+shift+tab" }
    ```

### Tab search ([Preview](https://aka.ms/terminal-preview/))

:::row:::
:::column span="":::

- **Description:** This opens the tab search box.
- **Command name:** `tabSearch`
- **Default binding:** _This command is not currently bound in the default settings_.

    ```json
    {"command": "tabSearch", "keys": ""}
    ```

:::column-end:::
:::column span="":::
![Windows Terminal tab search](./../images/tab-search.gif)

:::column-end:::
:::row-end:::

> [!IMPORTANT]
> This feature is only available in [Windows Terminal Preview](https://aka.ms/terminal-preview/).

### Open a specific tab

- **Description:** This opens a specific tab depending on the index.
- **Command name:** `switchToTab`
- **Default bindings:** <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>1</kbd> through <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>9</kbd>

    ```json
    { "command": { "action": "switchToTab", "index": 0 }, "keys": "ctrl+alt+1" },
    { "command": { "action": "switchToTab", "index": 1 }, "keys": "ctrl+alt+2" },
    { "command": { "action": "switchToTab", "index": 2 }, "keys": "ctrl+alt+3" },
    { "command": { "action": "switchToTab", "index": 3 }, "keys": "ctrl+alt+4" },
    { "command": { "action": "switchToTab", "index": 4 }, "keys": "ctrl+alt+5" },
    { "command": { "action": "switchToTab", "index": 5 }, "keys": "ctrl+alt+6" },
    { "command": { "action": "switchToTab", "index": 6 }, "keys": "ctrl+alt+7" },
    { "command": { "action": "switchToTab", "index": 7 }, "keys": "ctrl+alt+8" },
    { "command": { "action": "switchToTab", "index": 8 }, "keys": "ctrl+alt+9" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `index` | Required | Integer | Tab that will open based on its position in the tab bar (starting at 0). |

### Rename tab

- **Description:** This command can be used to rename a tab to a specific string.
- **Command name:** `renameTab`
- **Default binding:** _This command is not currently bound in the default settings_.

    ```json
    // Rename a tab to "Foo"
    { "command": { "action": "renameTab", "title": "Foo" }, "keys": "" }

    // Reset the tab's name
    { "command": { "action": "renameTab", "title": null }, "keys": "" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `title` | Optional | String | The new title to use for this tab. If omitted, this command will revert the tab title back to its original value. |

### Change tab color

- **Description:** This command can be used to change the color of a tab to a specific value.
- **Command name:** `setTabColor`
- **Default binding:** _This command is not currently bound in the default settings_.

    ```json
    // Change the tab's color to a bright magenta
    { "command": { "action": "setTabColor", "color": "#ff00ff" }, "keys": "" }

    // Reset the tab's color
    { "command": { "action": "setTabColor", "color": null }, "keys": "" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `color` | Optional | String, in hex format: `"#rgb"` or `"#rrggbb"` | The new color to use for this tab. If omitted, this command will revert the tab's color back to its original value. |

### Open tab color picker

- **Description:** This command can be used to open the color picker for the active tab. The color picker can be used to set a color for the tab at runtime.
- **Command name:** `openTabColorPicker`
- **Default binding:** _This command is not currently bound in the default settings_.

    ```json
    { "command": "openTabColorPicker", "keys": "" }
    ```

## Pane management commands

### Close pane

- **Description:** This closes the active pane. If there aren't any split panes, this will close the current tab. If there is only one tab open, this will close the window.
- **Command name:** `closePane`
- **Default binding:** <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>W</kbd>

    ```json
    { "command": "closePane", "keys": "ctrl+shift+w" }
    ```

### Move pane focus

- **Description:** This changes focus to a different pane depending on the direction.
- **Command name:** `moveFocus`
- **Default bindings:** <kbd>Alt</kbd>+<kbd>↓</kbd>, <kbd>Alt</kbd>+<kbd>←</kbd>, <kbd>Alt</kbd>+<kbd>→</kbd>, <kbd>Alt</kbd>+<kbd>↑</kbd>

    ```json
    { "command": { "action": "moveFocus", "direction": "down" }, "keys": "alt+down" },
    { "command": { "action": "moveFocus", "direction": "left" }, "keys": "alt+left" },
    { "command": { "action": "moveFocus", "direction": "right" }, "keys": "alt+right" },
    { "command": { "action": "moveFocus", "direction": "up" }, "keys": "alt+up" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `direction` | Required | `"left"`, `"right"`, `"up"`, `"down"` | Direction in which the focus will move. |

### Zoom a pane ([Preview](https://aka.ms/terminal-preview))

:::row:::
:::column span="":::

- **Description:** This expands the focused pane to fill the entire contents of the window.
- **Command name:** `togglePaneZoom`
- **Default binding:** _This command is not currently bound in the default settings_.

    ```json
    { "command": "togglePaneZoom", "keys": "" }
    ```

:::column-end:::
:::column span="":::
![Windows Terminal toggle pane zoom](./../images/toggle-pane-zoom.gif)

:::column-end:::
:::row-end:::

> [!IMPORTANT]
> This feature is only available in [Windows Terminal Preview](https://aka.ms/terminal-preview/).

### Resize a pane

- **Description:** This changes the size of the active pane.
- **Command name:** `resizePane`
- **Default bindings:** <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>↓</kbd>, <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>←</kbd>, <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>→</kbd>, <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>↑</kbd>

    ```json
    { "command": { "action": "resizePane", "direction": "down" }, "keys": "alt+shift+down" },
    { "command": { "action": "resizePane", "direction": "left" }, "keys": "alt+shift+left" },
    { "command": { "action": "resizePane", "direction": "right" }, "keys": "alt+shift+right" },
    { "command": { "action": "resizePane", "direction": "up" }, "keys": "alt+shift+up" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `direction` | Required | `"left"`, `"right"`, `"up"`, `"down"` | Direction in which the pane will be resized. |

### Split a pane

- **Description:** This halves the size of the active pane and opens another. Without any arguments, this will open the default profile in the new pane. If an action is not specified, the default profile's equivalent setting will be used.
- **Command name:** `splitPane`
- **Default bindings:** <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>D</kbd>, <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>-</kbd>, <kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>=</kbd>

    ```json
    // In settings.json
    { "command": { "action": "splitPane", "split": "auto", "splitMode": "duplicate" }, "keys": "alt+shift+d" },

    // In defaults.json
    { "command": { "action": "splitPane", "split": "horizontal"}, "keys": "alt+shift+-" },
    { "command": { "action": "splitPane", "split": "vertical"}, "keys": "alt+shift+plus" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `split` | Required | `"vertical"`, `"horizontal"`, `"auto"` | How the pane will split. `"auto"` will split in the direction that provides the squarest panes. |
    | `commandLine` | Optional | Executable file name as a string | Executable run within the pane. |
    | `startingDirectory` | Optional | Folder location as a string | Directory in which the pane will open. |
    | `tabTitle` | Optional | String | Title of the tab when the new pane is focused. |
    | `index` | Optional | Integer | Profile that will open based on its position in the dropdown (starting at 0). |
    | `profile` | Optional | Profile's name or GUID as a string | Profile that will open based on its GUID or name. |
    | `splitMode` | Optional | `"duplicate"` | Controls how the pane splits. Only accepts `"duplicate"`, which will duplicate the focused pane's profile into a new pane. |

## Clipboard integration commands

### Copy

- **Description:** This copies the selected terminal content to your clipboard.
- **Command name:** `copy`
- **Default bindings:** <kbd>Ctrl</kbd>+<kbd>C</kbd>, <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>C</kbd>, <kbd>Ctrl</kbd>+<kbd>Ins</kbd>

    ```json
    // In settings.json
    { "command": { "action": "copy", "singleLine": false }, "keys": "ctrl+c" },

    // In defaults.json
    { "command": { "action": "copy", "singleLine": false }, "keys": "ctrl+shift+c" },
    { "command": { "action": "copy", "singleLine": false }, "keys": "ctrl+insert" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `singleLine` | Optional | `true`, `false` | When `true`, the copied content will be copied as a single line. When `false`, newlines persist from the selected text. |
    | `copyFormatting` | Optional | `true`, `false`, `"all"`, `"none"`, `"html"`, `"rtf"` | When `true`, the color and font formatting of the selected text is also copied to your clipboard. When `false`, only plain text is copied to your clipboard. You can also specify which formats you would like to copy. When `null`, the global `copyFormatting` behavior is inherited. |

> [!IMPORTANT]
> `copyFormatting` is only available in [Windows Terminal Preview](https://aka.ms/terminal-preview/).

### Paste

- **Description:** This inserts the content that was copied onto the clipboard.
- **Command name:** `paste`
- **Default bindings:** <kbd>Ctrl</kbd>+<kbd>V</kbd>, <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>V</kbd>, <kbd>Shift</kbd>+<kbd>Ins</kbd>

    ```json
    // In settings.json
    { "command": "paste", "keys": "ctrl+v" },

    // In defaults.json
    { "command": "paste", "keys": "ctrl+shift+v" },
    { "command": "paste", "keys": "shift+insert" }
    ```

## Scrollback commands

### Scroll up

- **Description:** This scrolls the screen up.
- **Command name:** `scrollUp`
- **Default binding:** <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>↑</kbd>

    ```json
    { "command": "scrollUp", "keys": "ctrl+shift+up" }
    ```

### Scroll down

- **Description:** This scrolls the screen down.
- **Command name:** `scrollDown`
- **Default binding:** <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>↓</kbd>

    ```json
    { "command": "scrollDown", "keys": "ctrl+shift+down" }
    ```

### Scroll up a whole page

- **Description:** This scrolls the screen up by a whole page, which is the height of the window.
- **Command name:** `scrollUpPage`
- **Default binding:** <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>PgUp</kbd>

    ```json
    { "command": "scrollUpPage", "keys": "ctrl+shift+pgup" }
    ```

### Scroll down a whole page

- **Description:** This scrolls the screen down by a whole page, which is the height of the window.
- **Command name:** `scrollDownPage`
- **Default binding:** <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>PgDn</kbd>

    ```json
    { "command": "scrollDownPage", "keys": "ctrl+shift+pgdn" }
    ```

## Visual adjustment commands

### Adjust font size

- **Description:** This changes the text size by a specified point amount.
- **Command name:** `adjustFontSize`
- **Default bindings:** <kbd>Ctrl</kbd>+<kbd>=</kbd>, <kbd>Ctrl</kbd>+<kbd>-</kbd>

    ```json
    { "command": { "action": "adjustFontSize", "delta": 1 }, "keys": "ctrl+=" },
    { "command": { "action": "adjustFontSize", "delta": -1 }, "keys": "ctrl+-" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `delta` | Required | Integer | Amount of size change per command invocation. |

### Reset font size

- **Description:** This resets the text size to the default value.
- **Command name:** `resetFontSize`
- **Default binding:** <kbd>Ctrl</kbd>+<kbd>0</kbd>

    ```json
    { "command": "resetFontSize", "keys": "ctrl+0" }
    ```

### Toggle retro terminal effects

- **Description:** This toggles the "retro terminal effect", which is enabled with the profile setting `experimental.retroTerminalEffect`.
- **Command name:** `toggleRetroEffect`
- **Default binding:** _This command is not currently bound in the default settings_.

    ```json
    { "command": "toggleRetroEffect", "keys": "" }
    ```

### Set the color scheme ([Preview](https://aka.ms/terminal-preview/))

- **Description:** Changes the active color scheme.
- **Command name:** `setColorScheme`
- **Default binding:** _This command is not currently bound in the default settings_.

    ```json
    { "command": "toggleRetroEffect", "keys": "" }
    ```

- **Action block arguments:**

    | Name | Necessity | Accepts | Description |
    | ---- | --------- | ------- | ----------- |
    | `colorScheme` | Required | String | The `name` of the color scheme to apply. |

- **Example binding:**

    ```json
    { "command": { "action": "setColorScheme", "colorScheme": "Campbell" }, "keys": "" }
    ```

> [!IMPORTANT]
> This feature is only available in [Windows Terminal Preview](https://aka.ms/terminal-preview/).

## Unbind keys

- **Description:** This unbinds the associated keys from any command.
- **Command name:** `unbound`
- **Default binding:** _This command is not currently bound in the default settings_.

    ```json
    { "command": "toggleRetroEffect", "keys": "" }
    ```
