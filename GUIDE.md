# Guide: media tree kernel builder

## What is a kernel?

The kernel is the core of the operating system. It manages hardware, processes,
memory and drivers. On Linux, drivers for devices (TV tuners, capture cards)
live inside the kernel source tree.

## What are Hauppauge drivers?

Hauppauge TV tuners and capture devices use kernel media drivers (V4L2/DVB).
The LinuxTV.org media tree contains the newest versions of these drivers,
including fixes and new device IDs that may not be in the Ubuntu kernel yet.

## How this script works

`mediatree-kbuild.sh` automates:

1. Downloading the Ubuntu kernel source for a release.
2. Downloading the LinuxTV media tree.
3. Generating a patched media tree tarball for the kernel version.
4. Applying patches to the Ubuntu kernel source.
5. Updating changelog/build metadata.
6. Building installable `.deb` packages.

## Workflow

- `-i`: initialize/update git repositories.
- `-m`: download and generate media tree tarballs.
- `-r`: hard reset the build directory.
- `-p`: apply mediatree patches.
- `-x`: apply extra patches.
- `-c`: regenerate build data and clean.
- `-b` / `-B`: build the kernel.
- `-F`: final menu (apply drivers, create deb, download kernel.org, apply to running kernel).
- `-U`: uninstall kernel/drivers/ppa.

## Compilation

Kernel compilation uses `debian/rules` with `fakeroot`. It produces
`.deb` packages for image, modules, headers and extra modules.

## Differences from Windows

- On Windows, drivers are usually installed as separate packages from the vendor.
- On Linux, media drivers are part of the kernel source tree and are compiled
  with the kernel (or as out-of-tree modules).
- Updating drivers on Linux often means updating the kernel (or rebuilding modules).
- This project delivers drivers through standard Ubuntu `.deb` packages and a PPA,
  so updates arrive via `apt`.

## Uninstall

Use `-U` to remove the installed kernel virtual packages, the media tree
workspace, or the PPA.


## Automatic full build (one command)

Download drivers, apply them to the kernel, build and create the `.deb` in one step:

```
./mediatree-kbuild.sh -A
```

This runs the whole pipeline: init, media tree download, patching, build and deb/PPA generation.


## Debian and Debian-based distributions

Experimental support: the script falls back to Ubuntu kernel sources on Debian-based distros (Debian, Linux Mint, Pop!_OS, etc.).


## openSUSE / SUSE

Experimental support: falls back to Ubuntu kernel sources on openSUSE/SUSE systems.


## Additional distributions

Experimental fallback support for: Arch Linux, Manjaro, Fedora, RHEL/CentOS/Rocky/Alma, Linux Mint, SparkyLinux, Devuan, openSUSE/SUSE. All fall back to Ubuntu kernel sources.


## RPM package

Build an RPM of the tool (requires `rpmbuild`):

```
./mediatree-kbuild.sh -R
```
