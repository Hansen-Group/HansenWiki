# Tips and trick for using RstudioServer on Hulk

This document was written by Malte Thodberg and last updated 2022-06-08.

Official cluster wiki: <https://sites.google.com/site/cmbrgenetics/cluster>

## Access RStudioServer on Hulk

You can access RStudioServer on Hulk by typing this address in a brower:

<http://hulk:8787>

You will need to be on an ethernet connection at CBMR or connected via KU VPN.

## Edit `~/.R/Makevars` to use a newer C++ version

hulk is very old, so you might not be able to install R-packages that depends on newer C++ compilers. Instead you can edit your `~/.R/Makevars` file to point to a local and newer version of C++:

`CC=/opt/rh/devtoolset-11/root/usr/bin/gcc`

`CXX=/opt/rh/devtoolset-11/root/usr/bin/g++`

`CXX11=/opt/rh/devtoolset-11/root/usr/bin/g++`

You will need to restart RStudioServer server for these to take effect.

## Edit `~/.Renviron` to control library and tempoary locations

If you install a lot of R-packages they will be default be placed in personal home directory, which can subsequently run out of space quickly. To avoid this, you can put your R-packages in local folder instead, by adding this line to your `~/.Renviron` file:

`R_LIBS_USER="/emc/cbmr/users/abc123/R/%v"`

You will need to manually create this folder with `mkdir` first. The `%v` specifies the version of R (e.g. 4.1). This allows you keep different collections of R-packages in your local folder (useful is you sometimes work on porus which has a much older version of R currently.)

Sometimes other users might freeze RStudioServer (and the terminal) by filling up the default temporary storage on hulk. To avoid this, you can instruct R to save temporary files to your own personal directory:

`TMPDIR="/emc/cbmr/users/abc123/tools/R/tmp"`

You will need to manually create this folder with `mkdir` first.

## Mount the server locally

The official cluster wiki contains a guide for how to mount hulk/porus locally via sshfs, so you can browse files via you your local file browser (e.g. Finder on macOS).

If you have a newer Apple Silicon Mac (M1), you need some additional actions to enable sshfs, described here:

<https://techstuffer.com/fuse-for-macos-apple-silicon-m1/>
