---
title: Windows Terminal Custom Prompt Setup
description: In this tutorial, you learn how to set up Oh My Posh and Terminal-Icons in Windows Terminal.
author: cinnamon-msft
ms.author: cinnamon
ms.date: 08/17/2021
ms.topic: tutorial
#Customer intent: As a developer or IT admin, I want to set up Oh My Posh and Terminal-Icons in my Windows Terminal so that I can have a customized command line experience.
---

# Tutorial: Set up a custom prompt in Windows Terminal using Oh My Posh, Terminal-Icons, and Posh Git

[Oh My Posh](https://ohmyposh.dev) provides theme capabilities for a customized command prompt experience providing Git status color-coding and prompts. [Terminal-Icons](https://github.com/devblackops/Terminal-Icons) adds file and folder icons when displaying items in the terminal.

![Windows Terminal Custom Prompt](./../images/custom-prompt.png)

In this tutorial, you learn how to:

> [!div class="checklist"]
>
> * Set up Oh My Posh in PowerShell
> * Set up Oh My Posh in Ubuntu/WSL
> * Set up Terminal-Icons in PowerShell
> * Add missing glyphs

## Install a Nerd Font

Oh My Posh and Terminal-Icons use glyphs in order to style the prompt. If your font does not include the appropriate glyphs, you may see several Unicode replacement characters '&#x25AF;' throughout your prompt. In order to see all of the glyphs in your terminal, you should install a [Nerd Font](https://nerdfonts.com). (If you'd like a font that looks like Cascadia Code, the Caskaydia Cove Nerd Font was built from the Cascadia Code repository by a community member.) 

After downloading, you will need to unzip and install the font on your system. ([How to add a new font to Windows](https://support.microsoft.com/en-us/office/add-a-font-b7c5f17c-4426-4b53-967f-455339c564c1)).

## Set up Oh My Posh in PowerShell

Oh My Posh enables you to use a full color set to define and render your terminal prompt, including the ability to use built-in themes or create your own custom theme.

1. Install Oh My Posh.

Using PowerShell, install Oh My Posh with the command:

```powershell
Install-Module oh-my-posh -Scope CurrentUser
```

2. Pick your Oh My Posh theme.

After installing Oh My Posh, you can browse the built-in themes available using the command:

```powershell
Get-PoshThemes
```

3. Update your PowerShell profile.

Once you've installed Oh My Posh and chosen your theme, open your PowerShell profile using the command.
(You can replace notepad with the text editor of your choice.)

```powershell
notepad $PROFILE
```

Add the following to the end of your PowerShell profile file:

```powershell
Import-Module oh-my-posh
Set-PoshPrompt -Theme paradox
```

Now, each new PowerShell instance will start by importing Oh My Posh. [Learn more in the Oh My Posh documentation](https://ohmyposh.dev/docs/).

> [!NOTE]
> This is not your Windows Terminal profile. Your PowerShell profile is a script that runs every time PowerShell starts. [Learn more about PowerShell profiles](/powershell/module/microsoft.powershell.core/about/about_profiles).

4. Set your font in Windows Terminal settings.

To set a Nerd Font for use with Oh My Posh and Terminal Icons, open the Windows Terminal settings UI by selecting **Settings** (Ctrl+,) from your Windows Terminal dropdown menu. Select the Windows PowerShell profile, and then the **Appearance** tab. In the **Font face** drop-down menu, select *CaskaydiaCove Nerd Font* or whichever Nerd font you would like to use with your customized prompt.

![Windows Terminal Settings UI Font face menu](../../images/settings-powershell-font.png)

> [!NOTE]
> If you decide to use [Cascadia Code PL](https://github.com/microsoft/cascadia-code/releases) as your terminal font, you may consider using an Oh My Posh theme that contains the `minimal` function, indicating that additional icons aren't required.

## Set up posh-git in PowerShell

Posh-git adds a Git status summary to your Windows Terminal prompt with information and tab completion for Git commands, parameters, remotes and branch names.

1. Install posh-git.

Using PowerShell, install posh-git with the command:

```powershell
Install-Module posh-git -Scope CurrentUser
```

2. Update your PowerShell profile.

After installing, open your PowerShell profile using the command: `notepad $PROFILE`. (You can replace nodepad with the text editor of your choice).

In your PowerShell profile, add the following to the end of the file:

```powershell
Import-Module posh-git
```

Your PowerShell command prompt will now display a status whenever you are inside of a Git directory. Learn more in the [posh-git repo on GitHub](https://github.com/dahlbyk/posh-git#using-posh-git).

## Set up Oh My Posh in WSL Ubuntu

This section is coming soon!

## Additional resources

* [Oh my Posh documentation](https://ohmyposh.dev)
* [Terminal-Icons Repository](https://github.com/devblackops/Terminal-Icons)
