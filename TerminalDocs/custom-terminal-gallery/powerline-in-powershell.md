---
title: Windows Terminal Powerline in PowerShell
description: This is the configuration and theme for Powerline in PowerShell.
author: cinnamon-msft
ms.author: cinnamon
ms.date: 05/19/2020
ms.topic: sample
---

# Powerline in PowerShell theme for Windows Terminal

The prompt is styled using Powerline and is using the `Cascadia Code PL` font, which can be downloaded from the [Cascadia Code GitHub releases page](https://github.com/microsoft/cascadia-code/releases).

> [!div class="nextstepaction"]
> [Learn how to set up Powerline](./../tutorials/powerline-setup.md)

![Windows Terminal Powerline PowerShell](./../images/powerline-powershell.png)

```json
    {
        "theme": "dark",
        "profiles": [
            {
                "name" : "Powershell",
                "source" : "Windows.Terminal.PowershellCore",
                "acrylicOpacity" : 0.7,
                "colorScheme" : "Campbell",
                "cursorColor" : "#FFFFFD",
                "fontFace" : "Cascadia Code PL",
                "useAcrylic" : true
            }
        ]
    }
```
