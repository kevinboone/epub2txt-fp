# epub2txt-fp

This repository contains metadata for publishing the `epub2txt` utility
as a flatpak. There's little need to do this, since the utility is
trivially easy to build from source and install. Moreover, it's already
in the repositories for a number of Linux distributions.

Still, it's an interesting exercise. As a command-line utility, 
`epub2txt` is not well-suited for distribution as a flatpak. It
requires very little runtime support, and the smallest 
generally-recommended flatpak runtime is about 500Mb in size. The
`epub2txt` utility is only about 100kB in size. Still, in an 
installation that makes extensive use of flatpak, the runtime will
probably already be in place, so installing `epub2txt` as a
flatpak will not require much additional storage beyond that of
the utility itself.

Documentation for `epub2txt` itself is at
https://github.com/kevinboone/epub2txt2

This repository contains an installable binary, `epub2txt206.flatpak`.

To build and push to a local repository `flatpack-repo`:

    $ flatpak-builder --force-clean --repo=$HOME/flatpack-repo build-dir/ me.kevinboone.apps.Epub2Txt.yml

To build and install to the local user repository:

    $ flatpak-builder --user --install --force-clean build-dir me.kevinboone.apps.Epub2Txt.yml 

To install the `.flatpak` file locally:
 
    $ flatpak install {--user} epub2txt206.flatpak

Note that this will cause the host system to download the required
flatpak runtime, if it is not already present, which will use
about 500Mb of storage.

To run:

    $ flatpak run me.kevinboone.apps.Epub2Txt /path/to/document.epub

Alternatively, on a Linux system, copy the script `epub2txt-fp`
to `/usr/bin`, then you can run:

    $ epub2txt-fp /path/to/document.epub

Note that, run as a flatpak, `epub2txt` has limitations that do
not apply to the native installation. Most obviously, there will be
directories in the filesystem (like `/usr`) that are not accessible,
as these conflict with directories in the flatpak runtime.

The flatpak is also a bit slower to start up, and uses a bit
more memory. 

