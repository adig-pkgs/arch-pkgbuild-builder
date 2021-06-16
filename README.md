# Arch Linux PKGBUILD builder action

Differences from original repo -
* Uses pkgbuild\_dir variable instead of 'pkgname' to be used as directory containing the PKGBUILD
* You don't need to tell the 'pkgname', the script automatically extracts that info from PKGBUILD file
* Everything has defaults, and with point 2 above, you need 0 configuration on most repos

This action builds an validates Arch Linux package.
The directory containing `PKGBUILD` and `.SRCINFO` files can be specified in `pkgbuild\_dir` if not in the root of the repo (default is '.')

> Why this fork ?
> 1. Because I have PKGBUILD in root of repo.
> 2. Zero config use (Just add uses: '', and it should work)

## Inputs

### `target`

**Default: pkgbuild** Validation target. Can be one of: `pkgbuild`, `srcinfo`, `run`.

### `pkgbuild_dir`

**Default: '.'** Path to DIRECTORY where the PKGBUILD file is.

The `pkgname` is automatically extracted from the PKGBUILD

> TODO: Add this as input to explicitly tell the pkgname

### `debug`

Set to `true` to print the commands executed (ie. sh -x)

## Example usage

For most of the repos out there, this will work

Create `.github/workflows/pkgbuild.yml` (or other filename) with this content:

```yml
name: pkgbuild

on: push

jobs:
  pkgbuild_job:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
    - uses: adig-pkgs/arch-pkgbuild-builder@v2.0
```

> This currently doesn't work for split-packages (ie. if your PKGBUILD contains `pkgname=('a-aef' 'b-aef' 'c-aef') # my package`)

## Used by

All repos (source repo, not \*-git repo) in this organisation

For eg. 
[pkgbuild.yml in Ludo-The Game](https://github.com/adi-g15/Ludo-The_Game/blob/master/.github/workflows/pkgbuild.yml)
[pkgbuild.yml in worldLineSim](https://github.com/adi-g15/worldLineSim/blob/main/.github/workflows/pkgbuild.yml)

