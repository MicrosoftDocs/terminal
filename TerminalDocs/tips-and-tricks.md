---
title: Windows Terminal tips and tricks
description: In this page, you will find tips and tricks to help improve your Windows Terminal experience.
author: cinnamon-msft
ms.author: cinnamon
ms.date: 08/30/2021
ms.topic: how-to
ms.localizationpriority: high
---

# Windows Terminal tips and tricks

## Rename a tab

You can right click on a tab and select Rename Tab to rename a tab for that terminal session. Clicking this option in the context menu will change your tab title into a text field, where you can then edit the title. If you'd like to set the tab title for that profile for every terminal instance, you can learn more in the [Tab title tutorial](./tutorials/tab-title.md).

![Windows Terminal tab rename](./images/tab-rename.gif)

## Color a tab

You can right click on a tab and select Color... to color the tab for that terminal session. You can select from a predefined list of colors or you can click Custom... to pick any color using the color picker or the RGB/HSV or hex fields.

![Windows Terminal tab color](./images/tab-color.png)

> [!TIP]
> Use the hex field to set your tab to the same color as your background color for a seamless look.

> [!NOTE]
> While it is possible to [set the tab title from the commandline](./tutorials/tab-title.md) with escape sequences, it currently isn't possible to set the tab color in this way.

## Set Cascadia Code font as the default across all terminal profiles

Most [profile settings](./customize-settings/profile-general.md) in your terminal's [settings.json file](./get-started.md#settings-json-file) are specific to each unique command line profile. However, if you'd like a setting to apply to ALL of your profiles, you can add it to the defaults section above the list of profiles in your settings.json file.

```json
"defaults":
{
    // SETTINGS TO APPLY TO ALL PROFILES
},
"list":
[
    // PROFILE OBJECTS
]
```

To apply the [Cascadia Code font](./cascadia-code.md) (or Cascadia Code PL in this case to include Powerline glyphs) as the default font across all of your shells / command line profiles, add the following to your `settings.json` file "defaults" section:

```json
 "profiles": 
    {
    "defaults": {
    "fontFace": "Cascadia Code PL"
    },
    "list":
    [
    // PROFILE OBJECTS
    ]
``` 

Now all of your terminal profiles will automatically default to using the Cascadia Code PL font.

## Mouse interaction

There are several ways to interact with Windows Terminal using a mouse.

### Zoom with the mouse

You can zoom the text window of Windows Terminal (making the text size larger or smaller) by holding <kbd>ctrl</kbd> and scrolling. The zoom will persist for that terminal session. If you want to change your font size, you can learn more about the font size feature on the [Profile - Appearance page](./customize-settings/profile-appearance.md#text).

### Adjust background opacity with the mouse

You can adjust the opacity of the background by holding <kbd>ctrl+shift</kbd> and scrolling. The opacity will persist for that terminal session. If you want to change your acrylic opacity for a profile, you can learn more about acrylic background effects on the [Profile - Appearance page](./customize-settings/profile-appearance.md#acrylic).

### Open a hyperlink

You can open a hyperlink from inside Windows Terminal with your mouse using <kbd>ctrl</kbd> + click.

### Drag and drop file/folder to open ([Preview](https://aka.ms/terminal-preview))

You can drag and drop a file or folder over the New Tab button to open your default profile with that given file or folder. By default, this will open a new tab. You can hold <kbd>Alt</kbd> to open a new pane in your current tab or hold <kbd>Shift</kbd> to open a new window.

![Windows Terminal drag and drop](./images/drag-and-drop.gif)

> [!IMPORTANT]
> This feature is only available in [Windows Terminal Preview](https://aka.ms/terminal-preview).

### Copy/paste

You can right-click with your mouse to copy and paste text within Windows Terminal using your clipboard storage.

Windows Terminal also includes a **[copyOnSelect](./customize-settings/interaction.md#automatically-copy-selection-to-clipboard)** setting that can be set to `true` in order for any text selected with your mouse to be immediately copied to your clipboard. The right-click on your mouse will always paste in this case.

### Virtual Terminal and WSL mouse support

Windows Terminal supports mouse input in Windows Subsystem for Linux (WSL) applications as well as Windows applications that use virtual terminal (VT) input. This means applications such as [tmux](https://github.com/tmux/tmux/wiki) and [Midnight Commander](https://www.linuxhelp.com/how-to-install-midnight-commander-in-linux) will recognize when you select items in the Terminal window. If an application is in mouse mode, you can hold down <kbd>shift</kbd> to make a selection instead of sending VT input.

## Quake mode

Quake mode allows you to quickly open a new terminal instance from anywhere in Windows by typing <kbd>Win</kbd> + <kbd>`</kbd> (backtick). The quake window will appear on the top half of your screen and can easily be dismissed with the same keyboard shortcut.

"Quake mode" is the name for the special mode the terminal enters when naming a window `_quake`. When a window is in quake mode:

* The terminal is automatically snapped to the top half of the monitor.

* The window can no longer be resized horizontally or from the top. It can only be resized on the bottom.

* The window automatically enters focus mode (note that you may have multiple tabs in focus mode).

* When [`windowingBehavior`](./customize-settings/startup.md#new-instance-behavior) is set to `"useExisting"` or `"useAnyExisting"`, they will ignore the existence of the `_quake` window.

* The window will be hidden from the taskbar and from <kbd>Alt</kbd>+<kbd>Tab</kbd>.

* Only one window may be the quake mode window at a time.

The quake mode window can be created either by binding the `quakeMode` action, or by manually running the command line:

```console
wt -w _quake
```

> [!NOTE]
> If you don't have a [`quakeMode`](./customize-settings/actions.md#global-commands) action bound and minimize the quake window, you'll need to go into Task Manager to be able to exit that terminal window!
