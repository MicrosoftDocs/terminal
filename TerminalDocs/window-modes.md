---
title: Windows Terminal Window Modes
description: Learn about the different window modes available in Windows Terminal including full screen, focus mode, and quake mode.
ms.date: 12/18/2024
ms.topic: how-to
---

# Window modes in Windows Terminal

Windows Terminal offers three distinct window modes that change how the terminal window appears and behaves. Each mode is designed for specific use cases and workflows.

## Overview of window modes

| Mode | Tabs visible | Title bar visible | Window border visible | Default size | Primary use case |
|------|--------------|-------------------|----------------------|--------------|------------------|
| **Full screen** | Optional (configurable) | No | No | Full monitor | Maximum screen space for terminal content |
| **Focus mode** | No | No | No | Current window size | Distraction-free work on terminal content |
| **Quake mode** | No (focus mode enabled) | No | No | Top half of screen | Quick access drop-down terminal |

## Full screen mode

Full screen mode expands the terminal window to fill the entire screen, removing the title bar and window border to maximize the space available for your terminal content.

### Characteristics

* Window fills the entire monitor
* Title bar and window border are hidden
* Tabs can be shown or hidden (controlled by the [`showTabsInFullscreen`](./customize-settings/appearance.md#show-tabs-in-fullscreen) setting)
* Works with standard window operations (can be moved between monitors, minimized, etc.)

### How to activate full screen mode

**Using keyboard shortcut:**
* Press <kbd>Alt+Enter</kbd> or <kbd>F11</kbd> (default bindings)

**Using command palette:**
* Open the command palette (<kbd>Ctrl+Shift+P</kbd>)
* Type "toggle full screen"
* Select the command

**Using command line:**
```console
wt --fullscreen
```
or
```console
wt -F
```

**From settings (startup launch mode):**

Set the terminal to always launch in full screen by adding this to your [settings.json file](./install.md#settings-json-file):

```json
{
    "launchMode": "fullscreen"
}
```

### When to use full screen mode

* When you need maximum screen space for viewing terminal output
* When working with multiple columns of text that need full width
* When presenting or sharing your screen and want to minimize distractions
* When you want to keep tabs visible while maximizing content area

## Focus mode

Focus mode hides the title bar and tabs to minimize distractions, allowing you to concentrate solely on your terminal content. The window remains at its current size (not full screen).

### Characteristics

* Title bar is hidden
* Tabs are hidden
* Window border is hidden
* Window maintains its current size (doesn't expand to full screen)
* Can be combined with maximized or full screen modes
* You can still work with multiple tabs—they're just hidden from view

### How to activate focus mode

**Using keyboard shortcut:**

Focus mode doesn't have a default keyboard shortcut, but you can add one. Open your [settings.json file](./install.md#settings-json-file) and add this to the `keybindings` array:

```json
{ "keys": "ctrl+f12", "id": "Terminal.ToggleFocusMode" }
```

(Replace `"ctrl+f12"` with your preferred key combination)

**Using command palette:**
* Open the command palette (<kbd>Ctrl+Shift+P</kbd>)
* Type "focus mode"
* Select "Toggle focus mode"

**Using command line:**
```console
wt --focus
```
or
```console
wt -f
```

**From settings (startup launch mode):**

Set the terminal to always launch in focus mode by adding this to your [settings.json file](./install.md#settings-json-file):

```json
{
    "launchMode": "focus"
}
```

Or combine focus mode with maximized window:

```json
{
    "launchMode": "maximizedFocus"
}
```

### When to use focus mode

* When you want a distraction-free environment but don't need full screen
* When you're working in a single tab and don't need to see the tab bar
* When you want to maintain your current window size but reduce visual clutter
* When you prefer to switch tabs using keyboard shortcuts rather than clicking

## Quake mode

Quake mode is a special window mode that creates a drop-down terminal that slides in from the top of your screen, similar to the console in the video game Quake. It's designed for quick access to a terminal that you can summon and dismiss instantly.

### Characteristics

* Window snaps to the top half of the monitor automatically
* Cannot be resized horizontally or from the top (only from the bottom edge)
* Automatically enters focus mode (tabs and title bar are hidden)
* Can have multiple tabs despite being in focus mode
* When minimized, hides from taskbar and <kbd>Alt+Tab</kbd> switcher
* Only one quake window can exist at a time
* The quake window is named `_quake` internally
* When using `windowingBehavior` settings, the quake window is treated specially and doesn't count as an "existing window"

### How to activate quake mode

**Using keyboard shortcut:**

Quake mode doesn't have a default global keyboard shortcut, but you can set one. This requires a [global summon](./customize-settings/actions.md#global-commands) binding. Add this to your [settings.json file](./install.md#settings-json-file) in the `keybindings` array:

```json
{ "keys": "win+`", "id": "Terminal.QuakeMode" }
```

> [!WARNING]
> If you enable quake mode and don't set a keyboard shortcut, you may need to use Task Manager to close the quake window when it's minimized.

**Using command palette:**
* Open the command palette (<kbd>Ctrl+Shift+P</kbd>)
* Type "quake"
* Select "Show/hide quake window"

Note: If you invoke "Show/hide quake window" from a regular (non-quake) terminal window, it will summon or create the quake window but won't affect the current window.

**Using command line:**
```console
wt -w _quake
```

This creates or summons a window specifically named `_quake`, which automatically enters quake mode.

### When to use quake mode

* When you need quick, temporary access to a terminal for running commands
* When you want a terminal that's always accessible but doesn't clutter your workspace
* When you frequently switch between your terminal and other applications
* When you prefer keyboard-driven workflows with a persistent terminal session

## Comparing the modes

### Visual comparison

* **Full screen**: Entire monitor is filled with terminal. Tabs may be visible at the top (depending on settings). No title bar or window border.

* **Focus mode**: Same visual appearance as full screen (no tabs, title bar, or border), but the window is not expanded to full screen—it stays at whatever size it was.

* **Quake mode**: Looks like focus mode (no tabs, title bar, or border) but automatically sized to the top half of your monitor and can only be resized from the bottom.

### Mode combinations

Some modes can be combined:

* **Full screen + Focus mode**: You can enable focus mode while in full screen. This hides tabs even if `showTabsInFullscreen` is set to true.

* **Maximized + Focus mode**: Use the `"maximizedFocus"` launch mode to start with a maximized window in focus mode.

* **Quake mode**: Always includes focus mode; this cannot be disabled.

### Switching between modes

You can toggle between modes dynamically:

* Toggle full screen on/off without affecting focus mode
* Toggle focus mode on/off without affecting full screen
* Quake mode is a special window; you can toggle it to appear/disappear but it always maintains its quake characteristics

## Additional resources

* [Actions: Toggle full screen](./customize-settings/actions.md#toggle-full-screen)
* [Actions: Toggle focus mode](./customize-settings/actions.md#toggle-focus-mode)
* [Actions: Quake mode](./customize-settings/actions.md#open-the-quake-mode-window)
* [Startup settings: Launch mode](./customize-settings/startup.md#launch-mode)
* [Command line arguments](./command-line-arguments.md)
* [Tips and tricks: Focus mode](./tips-and-tricks.md#focus-mode)
* [Tips and tricks: Quake mode](./tips-and-tricks.md#quake-mode)
