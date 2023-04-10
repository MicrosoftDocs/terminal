---
title: Windows Terminal Portable Mode
description: Learn how to use Portable mode on Windows Terminal.
author: nguyen-dows
ms.author: chrnguyen
ms.date: 04/10/2023
ms.topic: how-to 
---

# Windows Terminal Portable

As of version 1.17, Windows Terminal supports being deployed in ["Portable mode"]. Portable mode ensures that all data
created and maintained by Windows Terminal is saved next to the application so that it can be more easily moved across
different environments.

Portable mode is supported by the [unpackaged "ZIP" distribution]. This is an officially-supported mode of execution
where Windows Terminal stores its settings in a `settings` folder next to `WindowsTerminal.exe`.

Portable mode is not supported in the packaged ("MSIX bundle") distribution of Windows Terminal.

## Why use Portable mode? 

The unpackaged and portable mode distribution of Windows Terminal allows you to use Terminal without installing it
globally, e.g. on systems where you may not have permission to install MSIX packages or download software from the
Microsoft Store.

Portable mode allows you to carry around (and archive!) a preconfigured installation of Windows Terminal and run it from
a network share, cloud drive or USB flash drive. Any such installation is self-contained and will not interfere with
other installed distributions of Windows Terminal.

## Enabling Portable mode

Portable mode needs to be enabled manually. After unzipping the Windows Terminal download, create a file named `.portable` next to `WindowsTerminal.exe`.

> [!NOTE]
> Windows Terminal will not automatically reload its settings when you create the portable mode marker file.
> This change will only apply after you relaunch Terminal.

Windows Terminal will automatically create a directory named `settings` in which it will store both settings and runtime
state such as window layouts.

![Windows Terminal portable mode](./images/portable-mode.png)

## Disabling Portable mode

You can restore Portable mode unpackaged installation to its original configuration, where settings are stored in
`%LOCALAPPDATA%\Microsoft\Windows Terminal`, by removing the `.portable` marker file from the directory containing
`WindowsTerminal.exe`.

If you wish to reenable portable mode, you can create a new `.portable` marker file next to `WindowsTerminal.exe`.

## Upgrading a Portable mode Install

You can upgrade a portable mode installation of Windows Terminal by moving the `.portable` marker file and the
`settings` directory to a newly-extracted unpackaged version of Windows Terminal.

["Portable mode"]: https://en.wikipedia.org/wiki/Portable_application
[unpackaged "ZIP" distribution]: https://github.com/microsoft/terminal/releases
