---
title: "Running An Ubuntu-Powered Terminal In Windows"
---

# Intro

Lots of time and energy can be spent trying to get a good terminal setup inside of Windows, whether that is using popular tools such as Cywign, cmder, or similar. After trying the various options, the best solution I found was to skip the unnecessaries and use a native Linux shell inside Windows itself! There is a fair amount of setup to get this to work correctly, but buy using the [Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) and a native X server running on your Windows machine you can have a nearly seamless experience.  This article will focus on using Ubuntu though if you dig hard enough you might be able to get the terminal working on other distros.

Before I get too deep into this, I want to give a special thanks to [this blog post,](https://blog.ropnop.com/configuring-a-pretty-and-usable-terminal-emulator-for-wsl/) which got me 90% of the way there. There were a few steps that were ambigous and had some issues I had to work through, so I thought supplying an updated guide would be appreciated.

## Windows Subsystem for Linux

Unfortunately due to the advanced nature of this topic Microsoft has decided to hide the ability to enable this feature through a flag that's set through PowerShell. Open a new PowerShell window as admin and run the following command:

```powershell
Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
```

Once you have this enabled, you'll be able to install some of the more popular distros either through the Windows Store or by [using PowerShell](https://docs.microsoft.com/en-us/windows/wsl/install-on-server) if you're feeling spicy. Personally I went through the Windows Store, since I like the idea of accidentally uninstalling my Linux machine and losing all my hard-earned progress.

Once you have your Linux distro installed (this guide will be using Ubuntu moving foward), you will need to launch it once to set up your username and password. After this is set up, it's time to install an X server on your Windows machine!

## X on Windows

To start off with, what is X?  X at it's core is a [protocol](https://en.wikipedia.org/wiki/X_Window_System_core_protocol) that makes up the X Window System. Essentially this protocol handles communication between the application you're running and the X server that renders the windows. Luckily it's a protocol, meaning that someone has already implemented X inside of Windows and has allowed this whole process to work in the first place.

There are two major options for getting this working, [VcXsrv](https://sourceforge.net/projects/vcxsrv/) and [Xming](https://sourceforge.net/projects/xming/). I blindly followed the advice supplied by Ronnie Flather's blog post and chose VcXsrv.  

## Installing the Command Line

Now that we have the X server running on Windows the next step is to get the terminal application installed in Ubuntu-land.  There are a few options available and all of them have their little quirks.  `gnome-terminal` is a good option, as is `terminator` (though it needs a little configuration to feel "right"). Unfortunately trying run either will result in an error without some... intervention.

Remember the X Server that's running on Windows?  These terminals use `dbus` to communicate between the running application and the X Server.  Most documentation I managed to find on the issue suggests that the reason why by default `dbus` errors out is due to it trying to communicate with the X Server using Unix sockets (which gets blocked inside of Windows).  The suggestions say to edit the configuration to make `dbus` to fall back to using TCP communication, but unfortunately at time of writing the configuration file is missing.  After searching and messing around, I managed to figure out just the fix.

Either option will require you to get a working `dbus` working inside of Ubuntu.  Sadly it seems that the default Ubuntu install at time of writing isn't working but _luckily_ you can get around the issues of not being able to communicate using `dbus` by installing the `x11-dbus` package.  After looking around for more information on `x11-dbus` it appears as though [x11-dbus adds a `dbus-launch` command missing by default](https://serverfault.com/a/411353).  Is that why if you run either terminal it dies?  I'm not sure, but I do know that installing the package fixes the launch problem.

## Setting Up ZSH and Friends

## Set Up Launch Scripts

## Advanced ZSH Configuration
