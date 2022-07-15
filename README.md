# Mia's Operating System

This respository holds all the source code for my operating system

## Prerequisites

 - A text editor such as [VS Code](https://code.visualstudio.com/).
 - [Docker](https://www.docker.com/) for creating our build-environment.
 - [Qemu](https://www.qemu.org/) for emulating our operating system.
 - Qemu should be added to the path so that we can access it from the command-line. 

## Setup

Build an image for our build-environment:
 - `docker build buildenv -t myos-buildenv`

## Build

Enter build environment:
 - Linux or MacOS: `docker run --rm -it -v "$(pwd)":/root/env myos-buildenv`
 - Windows (CMD): `docker run --rm -it -v "%cd%":/root/env myos-buildenv`
 - Windows (PowerShell): `docker run --rm -it -v "${pwd}:/root/env" myos-buildenv`

Build for x86 (other architectures may come in the future):
 - `make build-x86_64`
 - If you are using Qemu, please close it before running this command to prevent errors.

To leave the build environment, enter `exit`.

## Emulate

To emulate the operating system using [Qemu] (Don't forget to [add qemu to your path]
 - `qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso`
 - Note: Close the emulator when finished, so as to not block writing to `kernel.iso` for future builds.

If the above command fails, try one of the following:
 - Windows: [`qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso -L "C:\Program Files\qemu"`]
 - Linux: [`qemu-system-x86_64 -cdrom dist/x86_64/kernel.iso -L /usr/share/qemu/`]
 - Alternatively, install a custom BIOS binary file and link it to Qemu using the `-L` option.

Alternatively, you should be able to load the operating system on a USB drive and boot into it when you turn on your computer. 

## Cleanup

Remove the build-evironment image:
 - `docker rmi myos-buildenv -f`
 
