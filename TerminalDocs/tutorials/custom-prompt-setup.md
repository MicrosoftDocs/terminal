---
title: Windows Terminal Custom Prompt Setup
description: In this tutorial, you learn how to set up Oh My Posh and Terminal-Icons in Windows Terminal.
author: cinnamon-msft
ms.author: cinnamon
ms.date: 08/17/2021
ms.topic: tutorial
#Customer intent: As a developer or IT admin, I want to set up Oh My Posh and Terminal-Icons in my Windows Terminal so that I can have a customized command line experience.
---

# Tutorial: Set up a custom prompt in Windows Terminal using Oh My Posh and Terminal-Icons

[Oh My Posh](https://ohmyposh.dev) provides theme capabilities for a customized command prompt experience providing Git status color-coding and prompts. [Terminal-Icons](https://github.com/devblackops/Terminal-Icons) adds file and folder icons when displaying items in the terminal.

![Windows Terminal Custom Prompt](./../images/custom-prompt.png)

In this tutorial, you learn how to:

> [!div class="checklist"]
>
> * Set up Oh My Posh in PowerShell
> * Set up Oh My Posh in Ubuntu/WSL
> * Set up Terminal-Icons in PowerShell
> * Add missing glyphs

## Prerequisites

### Install a Nerd Font

Oh My Posh and Terminal-Icons use glyphs in order to style the prompt. If your font does not include the appropriate glyphs, you may see several Unicode replacement characters '&#x25AF;' throughout your prompt. In order to see all of the glyphs in your terminal, you should install a [Nerd Font](https://nerdfonts.com). The Nerd Font that looks most like Cascadia Code is called Caskaydia Cove Nerd Font.

## Set up Oh My Posh in PowerShell

### PowerShell prerequisites

Using PowerShell, install Oh-My-Posh:

```powershell
Install-Module oh-my-posh -Scope CurrentUser
```

### Customize your PowerShell prompt

Open your PowerShell profile with `notepad $PROFILE` or the text editor of your choice. This is not your Windows Terminal profile. Your PowerShell profile is a script that runs every time PowerShell starts. [Learn more about PowerShell profiles](/powershell/module/microsoft.powershell.core/about/about_profiles).

In your PowerShell profile, add the following to the end of the file:

```powershell
Import-Module oh-my-posh
Set-PoshPrompt -Theme paradox
```

Now, each new instance starts by importing Oh My Posh, then setting the Paradox theme from Oh My Posh. Oh My Posh comes with several [built-in themes](https://ohmyposh.dev/docs/themes). If you decide to use [Cascadia Code PL](https://github.com/microsoft/cascadia-code/releases) as a font, Oh My Posh has themes that contain the `minimal`
function which do not have the need for additional icons. You can also [create a custom theme](https://ohmyposh.dev/docs/installation#change-the-theme) to match the font of your choice.

### Set a Nerd Font as your font

To set a Nerd Font for use with Oh My Posh and Terminal Icons, you will have to download, unzip, and install the font on your system first. Once this is done, you can set your font inside Windows Terminal using the settings UI. This can be accessed by selecting **Settings** (Ctrl+,) from your Windows Terminal dropdown menu.

If you'd like a font that looks like Cascadia Code, the Caskaydia Cove Nerd Font was built from the Cascadia Code repository by a community member.

## Set up Oh My Posh in WSL Ubuntu

This section is coming soon!

## Set up Terminal Icons in PowerShell

Terminal-Icons is a PowerShell module that adds file and folder icons when displaying items in your terminal. You will also need a Nerd Font installed in order to see these icons.

### PowerShell prerequisites

Using PowerShell, install Terminal-Icons:

```powershell
Install-Module Terminal-Icons
```

### Customize your PowerShell prompt

Open your PowerShell profile with `notepad $PROFILE` or the text editor of your choice. This is not your Windows Terminal profile. Your PowerShell profile is a script that runs every time PowerShell starts. [Learn more about PowerShell profiles](/powershell/module/microsoft.powershell.core/about/about_profiles).

In your PowerShell profile, add the following to the end of the file:

```powershell
Import-Module Terminal-Icons
```

## Additional resources

* [Oh my Posh documentation](https://ohmyposh.dev)
* [Terminal-Icons Repository](https://github.com/devblackops/Terminal-Icons)
