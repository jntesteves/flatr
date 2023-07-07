# flatr

flatr (pronounced "flatter") is a tool to run a Flatpak app exposing the current working directory. This program is highly experimental and not very useful yet. I use it to launch VSCodium without having to give the IDE full access to the HOME directory, and that's pretty much all the testing it's got.

## Usage
```
flatr 0.1.0
Run Flatpak app exposing the current working directory

Usage: flatr [OPTION...] APP [ARG...]

Options:
 -*         Any option for the flatpak-run command
 -h --help  Print this help text and exit

Examples:
    flatr com.vscodium.codium --new-window .
    flatr --command=bash com.vscodium.codium
```

## Dependencies
flatr depends on Flatpak and a POSIX-compatible shell with core utilities for operation.

## Installing
Download or clone this repository with git. flatr can be easily installed with `./make install`, or a simple file copy to a directory in the PATH, for example `cp flatr ~/.local/bin/`.

```shell
# To install into default PREFIX (~/.local)
./make install

# To uninstall from default PREFIX
./make uninstall

# You can install into a different prefix by setting the PREFIX parameter
sudo ./make install PREFIX=/usr/local

# To uninstall from system PREFIX
sudo ./make uninstall PREFIX=/usr/local
```

We use the directory at `~/.local/bin` by default, as it is defined as a place for user-specific executable files in the [XDG Base Directory Specification](https://specifications.freedesktop.org/basedir-spec/basedir-spec-latest.html) and should already be included in the PATH environment variable. If this directory is not present in the PATH, you can add it in your `~/.bashrc` (or similar) file. The following code does that:
```shell
case ":${PATH}:" in
    *:"${HOME}/.local/bin":*) ;;
    *) export PATH="${HOME}/.local/bin:${PATH}" ;;
esac
```

## Contributing
To develop flatr we only depend on Podman and [contr](https://codeberg.org/jntesteves/contr). We have a development container image with all the tools required to build and validate the project.

```shell
# Build the development image
podman build -f Containerfile.develop -t flatr-develop

# Enter the development container
contr flatr-develop

# Validate your changes for correctness
./make lint
```

Every change must pass lint and formatting validation with `./make lint`. As an option, formatting can be automatically applied with `./make format`.

## License
This is free and unencumbered software released into the public domain.

Anyone is free to copy, modify, publish, use, compile, sell, or
distribute this software, either in source code form or as a compiled
binary, for any purpose, commercial or non-commercial, and by any
means.

See [UNLICENSE](UNLICENSE) file or http://unlicense.org/ for details.
