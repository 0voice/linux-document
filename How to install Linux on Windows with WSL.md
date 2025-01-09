原文链接：https://learn.microsoft.com/en-us/windows/wsl/install



# How to install Linux on Windows with WSL



## In this article

1. [Prerequisites](https://learn.microsoft.com/en-us/windows/wsl/install#prerequisites)
2. [Install WSL command](https://learn.microsoft.com/en-us/windows/wsl/install#install-wsl-command)
3. [Change the default Linux distribution installed](https://learn.microsoft.com/en-us/windows/wsl/install#change-the-default-linux-distribution-installed)
4. [Set up your Linux user info](https://learn.microsoft.com/en-us/windows/wsl/install#set-up-your-linux-user-info)
5. [Set up and best practices](https://learn.microsoft.com/en-us/windows/wsl/install#set-up-and-best-practices)
6. [Check which version of WSL you are running](https://learn.microsoft.com/en-us/windows/wsl/install#check-which-version-of-wsl-you-are-running)
7. [Upgrade version from WSL 1 to WSL 2](https://learn.microsoft.com/en-us/windows/wsl/install#upgrade-version-from-wsl-1-to-wsl-2)
8. [Ways to run multiple Linux distributions with WSL](https://learn.microsoft.com/en-us/windows/wsl/install#ways-to-run-multiple-linux-distributions-with-wsl)
9. [Want to try the latest WSL preview features?](https://learn.microsoft.com/en-us/windows/wsl/install#want-to-try-the-latest-wsl-preview-features)
10. [Additional resources](https://learn.microsoft.com/en-us/windows/wsl/install#additional-resources)

Developers can access the power of both Windows and Linux at the same time on a Windows machine. The Windows Subsystem for Linux (WSL) lets developers install a Linux distribution (such as Ubuntu, OpenSUSE, Kali, Debian, Arch Linux, etc) and use Linux applications, utilities, and Bash command-line tools directly on Windows, unmodified, without the overhead of a traditional virtual machine or dualboot setup.



## Prerequisites

You must be running Windows 10 version 2004 and higher (Build 19041 and higher) or Windows 11 to use the commands below. If you are on earlier versions please see [the manual install page](https://learn.microsoft.com/en-us/windows/wsl/install-manual).



## Install WSL command

You can now install everything you need to run WSL with a single command. Open PowerShell or Windows Command Prompt in **administrator** mode by right-clicking and selecting "Run as administrator", enter the wsl --install command, then restart your machine.

PowerShellCopy

```powershell
wsl --install
```

This command will enable the features necessary to run WSL and install the Ubuntu distribution of Linux. ([This default distribution can be changed](https://learn.microsoft.com/en-us/windows/wsl/basic-commands#install)).

If you're running an older build, or just prefer not to use the install command and would like step-by-step directions, see **[WSL manual installation steps for older versions](https://learn.microsoft.com/en-us/windows/wsl/install-manual)**.

The first time you launch a newly installed Linux distribution, a console window will open and you'll be asked to wait for files to de-compress and be stored on your machine. All future launches should take less than a second.

 Note

The above command only works if WSL is not installed at all. If you run `wsl --install` and see the WSL help text, please try running `wsl --list --online` to see a list of available distros and run `wsl --install -d <DistroName>` to install a distro. To uninstall WSL, see [Uninstall legacy version of WSL](https://learn.microsoft.com/en-us/windows/wsl/troubleshooting#uninstall-legacy-version-of-wsl) or [unregister or uninstall a Linux distribution](https://learn.microsoft.com/en-us/windows/wsl/basic-commands#unregister-or-uninstall-a-linux-distribution).



## Change the default Linux distribution installed

By default, the installed Linux distribution will be Ubuntu. This can be changed using the `-d` flag.

- To change the distribution installed, enter: `wsl --install -d <Distribution Name>`. Replace `<Distribution Name>` with the name of the distribution you would like to install.
- To see a list of available Linux distributions available for download through the online store, enter: `wsl --list --online` or `wsl -l -o`.
- To install additional Linux distributions after the initial install, you may also use the command: `wsl --install -d <Distribution Name>`.

 Tip

If you want to install additional distributions from inside a Linux/Bash command line (rather than from PowerShell or Command Prompt), you must use .exe in the command: `wsl.exe --install -d <Distribution Name>` or to list available distributions: `wsl.exe -l -o`.

If you run into an issue during the install process, check the [installation section of the troubleshooting guide](https://learn.microsoft.com/en-us/windows/wsl/troubleshooting#installation-issues).

To install a Linux distribution that is not listed as available, you can [import any Linux distribution](https://learn.microsoft.com/en-us/windows/wsl/use-custom-distro) using a TAR file. Or in some cases, [as with Arch Linux](https://wsldl-pg.github.io/ArchW-docs/How-to-Setup/), you can install using an `.appx` file. You can also create your own [custom Linux distribution](https://learn.microsoft.com/en-us/windows/wsl/build-custom-distro) to use with WSL.



## Set up your Linux user info

Once you have installed WSL, you will need to create a user account and password for your newly installed Linux distribution. See the [Best practices for setting up a WSL development environment](https://learn.microsoft.com/en-us/windows/wsl/setup/environment#set-up-your-linux-username-and-password) guide to learn more.



## Set up and best practices

We recommend following our [Best practices for setting up a WSL development environment](https://learn.microsoft.com/en-us/windows/wsl/setup/environment) guide for a step-by-step walk-through of how to set up a user name and password for your installed Linux distribution(s), using basic WSL commands, installing and customizing Windows Terminal, set up for Git version control, code editing and debugging using the VS Code remote server, good practices for file storage, setting up a database, mounting an external drive, setting up GPU acceleration, and more.



## Check which version of WSL you are running

You can list your installed Linux distributions and check the version of WSL each is set to by entering the command: `wsl -l -v` in PowerShell or Windows Command Prompt.

To set the default version to WSL 1 or WSL 2 when a new Linux distribution is installed, use the command: `wsl --set-default-version <Version#>`, replacing `<Version#>` with either 1 or 2.

To set the default Linux distribution used with the `wsl` command, enter: `wsl -s <DistributionName>` or `wsl --set-default <DistributionName>`, replacing `<DistributionName>` with the name of the Linux distribution you would like to use. For example, from PowerShell/CMD, enter: `wsl -s Debian` to set the default distribution to Debian. Now running `wsl npm init` from Powershell will run the `npm init` command in Debian.

To run a specific wsl distribution from within PowerShell or Windows Command Prompt without changing your default distribution, use the command: `wsl -d <DistributionName>`, replacing `<DistributionName>` with the name of the distribution you want to use.

Learn more in the guide to [Basic commands for WSL](https://learn.microsoft.com/en-us/windows/wsl/basic-commands).



## Upgrade version from WSL 1 to WSL 2

New Linux installations, installed using the `wsl --install` command, will be set to WSL 2 by default.

The `wsl --set-version` command can be used to downgrade from WSL 2 to WSL 1 or to update previously installed Linux distributions from WSL 1 to WSL 2.

To see whether your Linux distribution is set to WSL 1 or WSL 2, use the command: `wsl -l -v`.

To change versions, use the command: `wsl --set-version <distro name> 2` replacing `<distro name>` with the name of the Linux distribution that you want to update. For example, `wsl --set-version Ubuntu-20.04 2` will set your Ubuntu 20.04 distribution to use WSL 2.

If you manually installed WSL prior to the `wsl --install` command being available, you may also need to [enable the virtual machine optional component](https://learn.microsoft.com/en-us/windows/wsl/install-manual#step-3---enable-virtual-machine-feature) used by WSL 2 and [install the kernel package](https://learn.microsoft.com/en-us/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package) if you haven't already done so.

To learn more, see the [Command reference for WSL](https://learn.microsoft.com/en-us/windows/wsl/basic-commands) for a list of WSL commands, [Comparing WSL 1 and WSL 2](https://learn.microsoft.com/en-us/windows/wsl/compare-versions) for guidance on which to use for your work scenario, or [Best practices for setting up a WSL development environment](https://learn.microsoft.com/en-us/windows/wsl/setup/environment) for general guidance on setting up a good development workflow with WSL.



## Ways to run multiple Linux distributions with WSL

WSL supports running as many different Linux distributions as you would like to install. This can include choosing distributions from the [Microsoft Store](https://aka.ms/wslstore), [importing a custom distribution](https://learn.microsoft.com/en-us/windows/wsl/use-custom-distro), or [building your own custom distribution](https://learn.microsoft.com/en-us/windows/wsl/build-custom-distro).

There are several ways to run your Linux distributions once installed:

- [Install Windows Terminal](https://learn.microsoft.com/en-us/windows/terminal/get-started) ***(Recommended)*** Using Windows Terminal supports as many command lines as you would like to install and enables you to open them in multiple tabs or window panes and quickly switch between multiple Linux distributions or other command lines (PowerShell, Command Prompt, Azure CLI, etc). You can fully customize your terminal with unique color schemes, font styles, sizes, background images, and custom keyboard shortcuts. [Learn more.](https://learn.microsoft.com/en-us/windows/terminal)
- You can directly open your Linux distribution by visiting the Windows Start menu and typing the name of your installed distributions. For example: "Ubuntu". This will open Ubuntu in its own console window.
- From Windows Command Prompt or PowerShell, you can enter the name of your installed distribution. For example: `ubuntu`
- From Windows Command Prompt or PowerShell, you can open your default Linux distribution inside your current command line, by entering: `wsl.exe`.
- From Windows Command Prompt or PowerShell, you can use your default Linux distribution inside your current command line, without entering a new one, by entering:`wsl [command]`. Replacing `[command]` with a WSL command, such as: `wsl -l -v` to list installed distributions or `wsl pwd` to see where the current directory path is mounted in wsl. From PowerShell, the command `get-date` will provide the date from the Windows file system and `wsl date` will provide the date from the Linux file system.

The method you select should depend on what you're doing. If you've opened a WSL command line within a Windows Prompt or PowerShell window and want to exit, enter the command: `exit`.



## Want to try the latest WSL preview features?

Try the most recent features or updates to WSL by joining the [Windows Insiders Program](https://insider.windows.com/getting-started). Once you have joined Windows Insiders, you can choose the channel you would like to receive preview builds from inside the Windows settings menu to automatically receive any WSL updates or preview features associated with that build. You can choose from:

- Dev channel: Most recent updates, but low stability.
- Beta channel: Ideal for early adopters, more reliable builds than the Dev channel.
- Release Preview channel: Preview fixes and key features on the next version of Windows just before its available to the general public.

If you prefer not switching your Windows installation to a preview channel, you can still test the latest preview of WSL by issuing the command: `wsl --update --pre-release`. For more information check the [WSL Releases page on GitHub](https://github.com/Microsoft/WSL/releases).
