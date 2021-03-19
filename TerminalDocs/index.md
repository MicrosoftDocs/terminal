---
title: An overview on Windows Terminal
description: Learn about Windows Terminal and how it can improve your command line workflow.
author: cinnamon-msft
ms.author: cinnamon
ms.date: 09/22/2020
ms.topic: overview
ms.localizationpriority: high
---

# What is Windows Terminal?

Windows Terminal is a modern terminal application for users of command-line tools and shells like Command Prompt, PowerShell, and Windows Subsystem for Linux (WSL). Its main features include multiple tabs, panes, Unicode and UTF-8 character support, a GPU accelerated text rendering engine, and the ability to create your own themes and customize text, colors, backgrounds, and shortcuts.

![Windows Terminal screenshot](./images/overview.png)

> [!NOTE]
> [What's the difference between a console, a terminal, and a shell?](https://www.hanselman.com/blog/WhatsTheDifferenceBetweenAConsoleATerminalAndAShell.aspx) Read Scott Hanselman's explanation.

## Multiple profiles supporting a variety of command line applications

Any application that has a command line interface can be run inside Windows Terminal. This includes everything from PowerShell and Command Prompt to Azure Cloud Shell and any WSL distribution such as Ubuntu or Oh-My-Zsh.

## Customized schemes and configurations

You can configure your Windows Terminal to have a variety of color schemes and settings. To learn how to make your own color scheme, visit the [Color schemes page](./customize-settings/color-schemes.md). You can also find custom Terminal configurations in the [Custom terminal gallery](./custom-terminal-gallery/powerline-in-powershell.md).

## Custom actions

There are a variety of custom commands you can use in Windows Terminal to have it feel more natural to you. If you don't like a particular keyboard shortcut, you can change it to whatever you prefer.

For example, the default shortcut to copy text from the command line is <kbd>ctrl+shift+c</kbd>. You can change this to <kbd>ctrl+1</kbd> or whatever you prefer. To open a new tab, the default shortcut is <kbd>ctrl+shift+t</kbd>, but maybe you want to change this to <kbd>ctrl+2</kbd>. The default shortcut to flip between the tabs you have open is <kbd>ctrl+tab</kbd>, this could be changed to <kbd>ctrl+-</kbd> and used to create a new tab instead.

You can learn about customizing shortcuts on the [Actions page](./customize-settings/actions.md).

## Unicode and UTF-8 character support

Windows Terminal can display Unicode and UTF-8 characters such as emoji and characters from a variety of languages.

## GPU accelerated text rendering

Windows Terminal uses the GPU to render its text, thus providing improved performance over the default Windows command line experience.

## Background image support

You can have background images and gifs inside your Windows Terminal window. Information on how to add background images to your profile can be found on the [Profile - Appearance page](./customize-settings/profile-appearance.md#background-image).

## Command line arguments

You can set Windows Terminal to launch in a specific configuration using command line arguments. You can specify which profile to open in a new tab, which folder directory should be selected, open the terminal with split window panes, and choose which tab should be in focus.

For example, to open Windows Terminal from PowerShell with three panes, with the left pane running a Command Prompt profile and the right pane split between your PowerShell and your default profile running WSL, enter:

```powershell
wt -p "Command Prompt" `; split-pane -p "Windows PowerShell" `; split-pane -H wsl.exe
```

Learn how to set up command-line arguments on the [Command line arguments page](./command-line-arguments.md).
