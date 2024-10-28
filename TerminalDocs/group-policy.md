---
title: Group Policy
description: Learn how to set Group Policy for Windows Terminal.
author: chrnguyen
ms.author: chrnguyen
ms.date: 10/24/2024
ms.topic: how-to 
---

# Group Policies

Since Windows Terminal Preview 1.22, Windows Terminal is released on GitHub with Administrative Templates that allow you to configure Windows Terminal using Group Policies.

## How to install

### Download

You can find the latest administrative templates (ADMX and ADML files) in the assets section of our [newest Windows Terminal release on GitHub](https://github.com/microsoft/terminal/releases/latest). The file is named `GroupPolicyTemplates-<Version>.zip`

### Add the administrative template to an individual computer

1. Unzip the `GroupPolicyTemplates-<Version>.zip` file to your **Policy Definition** template folder. (Example: `C:\Windows\PolicyDefinitions`)

> [!NOTE]
> The `WindowsTerminal.adml` file in the `en-US` folder will apply the policy even if you are not using an `en-US`-based machine.

### Add the administrative template to Active Directory

1. On a domain controller or workstation with RSAT, go to the **PolicyDefinition** folder (also known as the Central Store) on any domain controller for your domain. <br>
For older versions of Windows Server, you might need to create the PolicyDefinition folder. For more information, see [How to create an manage the Central Store for Group Policy Administrative Templates in Windows](/troubleshoot/windows-client/group-policy/create-and-manage-central-store).
2. Copy the `WindowsTerminal.admx` file to the **PolicyDefinition** folder. (Example: `%systemroot%\sysvol\domain\policies\PolicyDefinitions`)
3. Copy the `WindowsTerminal.adml` file to the matching language folder in your language folder in your Policy Definition folder. Create the folder if it does not already exist (Example: `%systemroot%\sysvol\domain\policies\PolicyDefinitions\EN-US`)
4. If your domain has more than one domain controller, the new ADMX files will be replicated to them at the next domain replication interval.

> [!NOTE]
> You can always use `EN-US` as this is the fallback language. If no correct language exists, `EN-US` will be used.

### Import the administrative template in Intune

You can find all instructions on how to import the administrative template in Intune on [Import custom ADMX and ADML administrative templates into Microsoft Intune](/mem/intune/configuration/administrative-templates-import-custom#add-the-admx-and-adml-files)

You will also need to import `Windows.admx` since the Windows Terminal ADMX files contains references to that file.

## Policies

### Disabled Source Profiles

Supported on Windows Terminal Preview 1.22 or later.
<br>
This policy disables source profiles from being generated. Source names can be arbitrary strings. Potential candidates can be found as the "source" property on profile definitions in Windows Terminal's `settings.json` file.

Common sources are:
- Windows.Terminal.Azure
- Windows.Terminal.PowershellCore
- Windows.Terminal.Wsl

For instance, setting this policy to `Windows.Terminal.Wsl` will disable the built-in WSL integration of Windows Terminal.

Existing profiles will disappear from Windows Terminal after adding their source to this policy.

### Enabled Language Models/AI Providers

Supported on Windows Terminal Preview 1.23 or later.
<br>

This policy allows the listed Language Models / AI providers to be used with Terminal Chat. <br>

Common providers are:
- OpenAI
- AzureOpenAI
- GitHubCopilot

For instance, setting this policy to `OpenAI` will allow the use of OpenAI in Terminal Chat.

**Disabling Terminal Chat**

Enabling this policy but leaving the list empty disallows all providers and disables the Terminal Chat feature. 
