---
title: Windows Terminal Theme Settings
description: Learn how to customize the theme settings within Windows Terminal.
author: zadjii-msft
ms.author: migrie
ms.date: 09/06/2022
ms.topic: how-to
---

# Theme settings in Windows Terminal

The settings listed below affect the visuals of the Terminal window itself, rather than the appearance of an individual tab/pane. These settings are currently only editable directly in the [settings.json file](../install.md#settings-json-file), and are not configurable via the Settings UI.

```json
"theme": "dark"
"themes":
[
    // THEME OBJECTS
]
```

For some example themes, take a head over to the [Themes Gallery](/custom-terminal-gallery/theme-gallery.md).

Each theme in the `themes` list is comprised of a collection of property objects, that specify the properties of individual elements of the application. For example, the default `"dark"` theme is the following:

```json
{
    "name": "dark",
    "window": {
        "applicationTheme": "dark"
    },
    "tab": {
        "background": "terminalBackground",
        "unfocusedBackground": "#00000000"
    },
    "tabRow": {
        "unfocusedBackground": "#333333FF"
    }
},
```

## Theme Name

This is the name of the theme. Names should be unique. The names `dark`, `light`, and `system` are reserved for the built-in default themes.

**Property name:** `name`

**Necessity:** Required

**Accepts:** a string

___

## Window

### Application Theme

This is the name of the color scheme used in the profile. Color schemes are defined in the `schemes` object. More detailed information can be found on the [Color schemes page](./color-schemes.md).

**Property name:** `applicationTheme`

**Necessity:** Optional

**Accepts:** `"system"`, `"dark"`, `"light"`

**Default value:** `"dark"`

___

## Tab Row

These settings are used to configure the appearance of the tab row. When `showTabsInTitlebar` is `true` (the default), this configures the titlebar.

### Background color

The color of the tab row when the window is in the foreground.

**Property name:** `background`

**Necessity:** Optional

**Accepts:** a [Theme Color](#theme-colors).

### Inactive background color

The color of the tab row, when the window is inactive.

**Property name:** `unfocusedBackground`

**Necessity:** Optional

**Accepts:** a [Theme Color](#theme-colors).

___

## Tabs

### Background color

The color a tab should be when the tab is active. Setting a `tabColor` in a profile will override this value. Similarly, setting a color at runtime with the tab color picker will override this color.

This color is always treated as a solid color, even if set to a `terminalBackground` with a pane with an acrylic background.

**Property name:** `background`

**Necessity:** Optional

**Accepts:** a [Theme Color](#theme-colors).

### Inactive background color

The color a tab should be when the tab is inactive. Setting a `tabColor` in a profile will override this value. Similarly, setting a color at runtime with the tab color picker will override this color.

This color is always treated as a solid color, even if set to a `terminalBackground` with a pane with an acrylic background.

When set to `terminalBackground` or `accent`, this will automatically use an alpha value of 30%, to be semi-transparent.

**Property name:** `unfocusedBackground`

**Necessity:** Optional

**Accepts:** a [Theme Color](#theme-colors).

### Show close button

Configures how the "close" button on the tab should behave. This accepts the following values:
* `"always"`: Always show tab close buttons.
* `"hover"`: Show the tab close button on the active tab, and any tabs that are hovered with the mouse.
* `"never"`: Never show tab close buttons. This also disables the ability to close the tab with the middle mouse button.

**Property name:** `showCloseButton`

**Necessity:** Optional

**Accepts:** `"always"`, `"hover"`, `"never"`

**Default value:** `"always"`

___


## Theme Colors

The colors used in themes both accept RGBA color values, as well as a few special strings for custom values. The accepted values are as follows

* `"#rgb`, `"#rrggbb`, `"#rrggbbaa`: An RGB color value. When the alpha chanel is omitted, these colors default to a fully opaque alpha channel.
* `"accent"`: This is a special value that means "the accent color set in the system settings".
* `"terminalBackground"`: This is a special value evaluated to mean "the background color of the active terminal pane". If there are multiple panes in a tab, then this is the color of the active one. This always uses the `background` of the profile - it ignores anything from a `backgroundImage`, if set.
