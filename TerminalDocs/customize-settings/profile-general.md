---
title: Windows Terminal General Profile Settings
description: Learn how to customize the general profile settings within Windows Terminal.
author: cinnamon-msft
ms.author: cinnamon
ms.date: 04/14/2021
ms.topic: how-to
ms.localizationpriority: high
---

# General profile settings in Windows Terminal

The settings listed below are specific to each unique profile. If you'd like a setting to apply to all of your profiles, you can add it to the `defaults` section above the list of profiles in your [settings.json file](../get-started.md#settings-json-file).

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

## Name

This is the name of the profile that will be displayed in the dropdown menu. This value is also used as the "title" to pass to the shell on startup. Some shells (like `bash`) may choose to ignore this initial value, while others (`Command Prompt`, `PowerShell`) may use this value over the lifetime of the application. This "title" behavior can be overridden by using `tabTitle`.

**Property name:** `name`

**Necessity:** Required

**Accepts:** String

<br />

___

## Command line

This is the executable used in the profile.

**Property name:** `commandline`

**Necessity:** Optional

**Accepts:** Executable file name as a string

**Default value:** `"cmd.exe"`

<br />

___

## Starting directory

This is the directory the shell starts in when it is loaded.

**Property name:** `startingDirectory`

**Necessity:** Optional

**Accepts:** Folder location as a string

**Default value:** `"%USERPROFILE%"`

**Example:** Start the PowerShell profile in the *GitHubRepos* folder of your *Documents* directory by finding the powershell.exe profile and adding `"startingDirectory": "%USERPROFILE%/Documents/GitHubRepos",`

**Example with WSL:** When setting the starting directory for a [Linux distribution installed via WSL](/windows/wsl/install-win10), use the format: `"startingDirectory": "\\\\wsl$\\DISTRO NAME\\home\\USERNAME"`, replacing with the placeholders with the proper names of your distribution. For example, `"startingDirectory": "\\\\wsl$\\Ubuntu-20.04\\home\\user1"`. If you are using the Windows Terminal Settings UI, rather than the [settings.json file](../get-started.md#settings-json-file), to declare this path, you can use the **Browse...** button to select your starting directory or enter the WSL path as: `//wsl.localhost/DISTRO NAME/home/USERNAME`. For example, `//wsl.localhost/Ubuntu-20.04/home/user1`. 

**Default behavior:** When the startingDirectory value is not specified, you will get different results depending on where you launch Terminal:
- If you run Windows Terminal from the Start menu: C:\windows\system32
- If you run wt.exe from the Start menu: C:\windows\system32
- If you run wt.exe from Win+R: %USERPROFILE%
- If you run wt.exe from the explorer address bar: whatever folder you were looking at.

> [!NOTE]
> Backslashes need to be escaped. For example, `C:\Users\USERNAME\Documents` should be entered as `C:\\Users\\USERNAME\\Documents`.

___

## Icon

This sets the icon that displays within the tab, dropdown menu, jumplist, and tab switcher.

**Property name:** `icon`

**Necessity:** Optional

**Accepts:** File location as a string, or an emoji

**Example:** By placing the icon image `ubuntu.ico` in the folder located at `%LOCALAPPDATA%\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\RoamingState`, you can display the icon by adding this line to the profile in your [settings.json](../get-started.md#settings-json-file): `"icon": "ms-appdata:///roaming/ubuntu.ico"`.

<br>
___

## Tab title

If set, this will replace the `name` as the title to pass to the shell on startup. Some shells (like `bash`) may choose to ignore this initial value, while others (`Command Prompt`, `PowerShell`) may use this value over the lifetime of the application. If you'd like to learn how to have the shell set your title, visit the [tab title tutorial](./../tutorials/tab-title.md).

**Property name:** `tabTitle`

**Necessity:** Optional

**Accepts:** String

<br />

___

## Hide profile from dropdown

If `hidden` is set to `true`, the profile will not appear in the list of profiles. This can be used to hide default profiles and dynamically generated profiles, while leaving them in your settings file. To learn more about dynamic profiles, visit the [Dynamic profiles page](./../dynamic-profiles.md).

**Property name:** `hidden`

**Necessity:** Optional

**Accepts:** `true`, `false`

**Default value:** `false`
