---
title: How to Build the Latest Emacs from Source
categories:
  - Docs
tags:
  - Linux
---

This guide uses Ubuntu 22.04 LTS, but it should work equally well on any Debian-flavor Linux variant.

The first step is to download the latest release of Emacs from the main [Gnu FTP server](https://ftp.gnu.org/gnu/emacs/) or a [nearby mirror](http://ftpmirror.gnu.org/emacs/).

Extract the compressed source and `cd` into the directory.

Install the necessary dependencies:

```sh
    sudo apt update
    sudo apt install build-essential texinfo libx11-dev libxpm-dev libjpeg-dev libpng-dev libgif-dev libtiff-dev libgtk-3-dev libncurses-dev automake autoconf libgnutls28-dev libgccjit-12-dev
```

We grabbed version 12 of GCC with the dependencies, so we need to tell our system to use it:

```sh
    export CC="gcc-12"
```

Create the configuration file (your `pwd` should still be the uncompressed Emacs source directory):

```sh
    ./configure
```

Check for errors in the configuration output to see if there are any missing dependencies. You generally only need to pay attention to the red "error" notices. The yellow "warning" notices can be safely ignored.

If everything looks good in the configuration, it's time to build Emacs:

```sh
    sudo make && sudo make install
```

That's it! [Let me know](/about) if I got anything wrong, or send me some comments if you run into trouble.
