---
title: How to install FreeBSD 13.2
date: 2023-10-15 07:00:00 +0200
categories: [FreeBSD, Setup]
tags: [os, tech, freebsd]
image:
    path: /assets/img/sample/freebsd_start_blog.png
    alt: Welcome to FreeBSD.
---

This is going to be a quick installation guide on how to install FreeBSD 13.2 with some of my rambling in between.

## Prerequisites

this guide will be regarding installing freebsd on your system so having some sort of USB would be recommended unless you are installing it to Virtual Machine.

## Getting ISO file

To get you ISO file you will head to [FreeBSD download page](https://www.freebsd.org/where/) in this case we will be installing FreeBSD 13.2-RELEASE.

![Desktop View](/assets/img/sample/freebsd_download.png){: w="500" h="500" .right }
Here you will have to make choice about what system architecture are you installing it for.
If you have 64bit system running x86 processor clicking on **amd64** option under installer should be just about what you need.
There you will be presented with quite a lot of options for ISOs. so which one to choose ?

**bootonly** - requires internet to pull all the necessary files for you system.
**disc1/dvd1** - does not require internet connection but it takes longer to download ISO from the website. 

**.xz** - means it is compressed and you will need to un-compress it before you can use the ISO.

also make sure to get **SHA256** file as well to check that you have correct file.

## Verifying ISO via SHA256 checksum

reason you get checksum file is to verify integrity of your iso file
and i will list some ways to do it on different operating systems: 

Powershell (Windows):

```powershell
Get-FileHash \yourISOpath\ -Algorithm SHA256 | Format-List
```
now you can open checksum file and compare your powershell output to it.

sha256sum (Linux):

```sh
sha256sum /yourISOpath/
cat /yourSHA256file/
```
if output matches congratulations you have safe ISO install on your system.

## Creating bootable USB

When you obtain you ISO you will have to create bootable USB to start the installer.

Some tools to make bootable USB are:

**Etcher** (Linux,MacOS,Windows)

- GUI tool that flashes ISO images on to you usb stick.

**dd** (Linux,MacOS)

- Terminal GNU utility.

**Rufus** (Windows)

- GUI windows only tool.

There is an article from website linuxhint that goes more in to detail [here](https://linuxhint.com/create_bootable_linux_usb_flash_drive/).

## Installation

After all that we can finally get on with the installation. that should be pretty strait forward.
Plug your USB with flashed iso in to the device and boot in to freebsd menu and press ***enter*** that will get you in to installer for FreeBSD.

> If your USB is not booting on start up you will have to set it as first thing to boot in your BIOS
{: .prompt-warning }

![Desktop View](/assets/img/sample/freebsd_install_blog1.png){: w="500" h="500" .left }
When you are in the installer you should choose mostly default options unless you really know what you are doing in which case i have no idea what you are doing here, but hey thank you for reading my blog regardless.

moving in installer is via TAB/arrow keys

confirming ENTER

selecting is SPACE

Most options from this point should be pretty self explanatory but there are some options that you might be curios about.

## Optional components

in FreeBSD installer you have an option to download certain components for the system by default it will look like this:

![FreeBSD installer components](/assets/img/sample/freebsd_install_blog2.png){: w="700" h="700" .normal }

Most of these components are not something that you need (specially debugging options) when you just want to have a apache or nginx server and running your website.

But there is **Ports** option which is nice one to consider if you want use ports as your provider of packages.
Just remember that it is not recommended to mix **Ports** packages with packages from **pkg** (FreeBSDs package manager)

difference between pkg and ports is that with ports you are compiling packages on your system which allows for better customization while pkg installs precompiled binaries.

personally i would recommend to stick with pkg and not worry about ports for now.

## System Configuration

After some time you should get to system configuration of services that are going to start on system boot. Here it is nice to have SSHD since since that is going to setup OpenSSH on your FreeBSD system so i highly recommend leaving that ON. As you will probably want to SSH in to your server sooner or later.

## New User and Default shell

![New User](/assets/img/sample/freebsd_install_blog3.png){: w="500" h="500" .right }
When it comes to setting up new user i usually set everything as default since defaults are pretty nice. If you come from Linux there might be two thing that might surprise you about this setup like that there is no bash option and that i don't add my user to wheel group.

Bash is not included in FreeBSD by default but you can install it later if you want from pkg or ports, but to be honest default shell is pretty nice to use and is POSIX compliant. And the reason i don't put my new user in to wheel group is because there is no sudo or doas command by default either so it has to be installed and configured manually and i will add my user to the wheel group when i install sudo or doas which i do recommend doing after you setup everything that you need as a root on your FreeBSD instance.

## Third party resources

Website that will probably help you the most is official FreeBSD website and Handbook on there. I will put link to FreeBSDs guide on installation where you will find everything under the sun that you might need. Link [HERE](https://docs.freebsd.org/en/books/handbook/bsdinstall/).

## The End

If you got here and read through all of this i want thank you for reading and wish you to have fun with your new FreeBSD system.