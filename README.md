# asdf-r

[R](https://www.r-project.org/) plugin for [asdf](https://github.com/asdf-vm/asdf) version manager | [plugins repository](https://github.com/asdf-vm/asdf-plugins)

## Dependencies

### MacOS

1. [Homebrew](https://brew.sh): used to install the remainder of the dependencies
2. ```brew install gcc xz libxt cairo pcre2```

More details on environment variables setup for Mac OS builds can be found [here](https://github.com/asdf-community/asdf-R/pull/2#issue-615542640).

### Linux

#### Ubuntu / Debian
1. ```sudo apt-get install build-essential libcurl3-dev libreadline-dev gfortran```
2. ```sudo apt-get install liblzma-dev liblzma5 libbz2-1.0 libbz2-dev```
3. ```sudo apt-get install xorg-dev libbz2-dev liblzma-dev libpcre2-dev```

## Install

```bash
asdf plugin add r https://github.com/asdf-community/asdf-r.git
```

## ASDF options

Check [asdf](https://github.com/asdf-vm/asdf) readme for instructions on how to install & manage versions of R.

When installing R using `asdf install`, you can pass custom configure options with the following env vars:

* `R_CONFIGURE_OPTIONS` - use only your configure options
* `R_EXTRA_CONFIGURE_OPTIONS` - append these configure options along with ones that this plugin already uses

### Building R Shared Library

RStudio (and some other libs) requires building R shared library. In order to do that pass an extra configure option to `asdf install`:

```bash
R_EXTRA_CONFIGURE_OPTIONS=--enable-R-shlib asdf install r <version>
```

maybe you'll need Cairo as well:

```bash
R_EXTRA_CONFIGURE_OPTIONS='--enable-R-shlib --with-cairo' asdf install r <version>
```

## Troubleshooting

### X11 / XQuartz errors

If you encounter X11-related errors during installation and don't need X11 support, you can skip it:

```bash
R_EXTRA_CONFIGURE_OPTIONS='--with-x=no' asdf install r <version>
```

If you do need X11 support, install [XQuartz](https://www.xquartz.org/) first manually or by running:

```bash
brew install xquartz
```

### Missing library errors (liblzma, pcre2, etc.)

If installation fails with errors about missing libraries like `liblzma` or `pcre2`, set the compiler flags to point to the Homebrew installation paths:

```bash
export CPPFLAGS="-I$(brew --prefix xz)/include -I$(brew --prefix pcre2)/include"
asdf install r <version>
```

This tells the compiler where to find the required header files for these libraries.
