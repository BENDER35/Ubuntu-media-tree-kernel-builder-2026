# Ubuntu + LinuxTV.org media tree custom kernel builder

This project builds installable Ubuntu kernel packages that include the latest
LinuxTV.org media tree drivers, with extra support for Hauppauge devices.

## Features

- Slips the latest LinuxTV.org media tree into an Ubuntu kernel source tree.
- Applies the minimal patches needed to build.
- Builds installable `.deb` kernel packages.
- Provides virtual packages for easy installation and upgrades.
- Supports a PPA for end users.

## Requirements

- Ubuntu (supported releases: see `patches/` (newer releases such as 26.04.1/26.10 fall back to the latest available patch set)).
- Build tools: `git`, `make`, `patch`, `fakeroot`, `debuild`, `equivs-build`.
- Sufficient disk space and time (kernel builds are large).

Install build dependencies (example):

```
sudo apt-get update
sudo apt-get install -y git make patch fakeroot devscripts equivs build-essential libncurses-dev
```

## Quick start (full build)

1. Initialize repositories:

```
./mediatree-kbuild.sh -i
```

2. Download and generate the LinuxTV media tree tarballs:

```
./mediatree-kbuild.sh -m
```

3. (Optional) Reset the kernel build directory to a clean state:

```
./mediatree-kbuild.sh -r
```

4. Apply the mediatree kbuild patches:

```
./mediatree-kbuild.sh -p
```

5. Apply extra patches:

```
./mediatree-kbuild.sh -x
```

6. Generate build data and clean:

```
./mediatree-kbuild.sh -c
```

7. Build the kernel:

```
./mediatree-kbuild.sh -b
```

   Or choose a build type:

```
./mediatree-kbuild.sh -B full
./mediatree-kbuild.sh -B debug
```

8. Final step (deb creation / drivers / kernel.org):

```
./mediatree-kbuild.sh -F
```

## PPA / virtual package

Build PPA descriptors:

```
./mediatree-kbuild.sh -V virtual
./mediatree-kbuild.sh -V kernel
./mediatree-kbuild.sh -V all
```

## Install from PPA (end users)

```
sudo add-apt-repository ppa:b-rad/kernel+mediatree+hauppauge
sudo apt-get update
sudo apt-get install linux-mediatree        # all Ubuntu
# or, for LTS with HWE:
sudo apt-get install linux-hwe-mediatree
```

## Automatic full build (one command)

Download drivers, apply them to the kernel, build and create the `.deb` in one step:

```
./mediatree-kbuild.sh -A
```

This runs the whole pipeline: init, media tree download, patching, build and deb/PPA generation.

## Uninstall

```
./mediatree-kbuild.sh -U k   # uninstall kernel (virtual packages)
./mediatree-kbuild.sh -U d   # remove media tree/drivers workspace
./mediatree-kbuild.sh -U p   # remove PPA
./mediatree-kbuild.sh -U a   # all of the above
```

## Other useful commands

- Generate a full patchset: `./mediatree-kbuild.sh -g`
- Show help: `./mediatree-kbuild.sh -h`

## Author

Brad Love <brad at nextdimension dot cc>

## License

GNU General Public License v3 or later.


## Debian and Debian-based distributions

Experimental support: the script falls back to Ubuntu kernel sources on Debian-based distros (Debian, Linux Mint, Pop!_OS, etc.).
