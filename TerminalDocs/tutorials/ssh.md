---
title: Windows Terminal SSH
description: In this tutorial, learn how to set up an SSH connection in Windows Terminal.
author: cinnamon-msft
ms.author: cinnamon
ms.date: 05/19/2020
ms.topic: tutorial
#Customer intent: As a developer or IT admin, I want to set up am SSH connection in Windows Terminal so that I can connect to other servers.
---

# Tutorial: SSH in Windows Terminal

Windows 10 has a built-in SSH client that you can use in Windows Terminal.

In this tutorial, you'll learn how to set up a profile in Windows Terminal that uses SSH.

## Create a profile

You can start an SSH session in your command prompt by executing `ssh user@machine` and you will be prompted to enter your password. You can create a Windows Terminal profile that does this on startup by adding the `commandline` setting to a profile in your settings.json file inside the `list` of profile objects.

```json
{
  "name": "user@machine ssh profile",
  "commandline": "ssh user@machine",
}
```

For more information, see:

* [Windows Terminal Profile - General settings](./../customize-settings/profile-general.md)

## Specify starting directory

To specify the starting directory for a ssh session invoked by Windows Terminal, you can use this command:

```json
{
  "commandline": "ssh -t bob@foo \"cd /data/bob && exec bash -l\""
}
```

The `-t` flag forces pseudo-terminal allocation. This can be used to execute arbitrary screen-based programs on a remote machine, e.g. when implementing menu services. You will need to use escaped double quotes as bourne shell derivatives don't do any additional parsing for a string in single quotes.

For more information, see:

* [GH Issue: How to specify the starting directory for a ssh session?](https://github.com/MicrosoftDocs/terminal/issues/25)
* [StackOverflow: How can I ssh directly to a particular directory?](https://stackoverflow.com/questions/626533/how-can-i-ssh-directly-to-a-particular-directory)

## Resources

* [How to Enable and Use Windows 10’s New Built-in SSH Commands](https://www.howtogeek.com/336775/how-to-enable-and-use-windows-10s-built-in-ssh-commands/)
