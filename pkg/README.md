OS-specific packaging bits for tarsnap
======================================

This directory contains bits to allow tarsnap to fit into operating system
package management systems.  I don't have access to all of these systems,
so please email me (at <cperciva@tarsnap.com>) if there are any problems
with these bits or if you can provide packaging bits for another OS.


Debian
------

To build a Debian package:

    ln -s pkg/debian .
    dpkg-buildpackage -b

Then to install it:

    sudo dpkg -i ../tarsnap_<version>_<arch>.deb

The [DEBIAN.md](DEBIAN.md) file discusses a more advanced packaging system
with a view towards reproducibility and cryptographically signed packages.


Arch Linux
----------

There is a PKGBUILD file for an earlier version of tarsnap in pkg/archlinux.
I can't include a PKGBUILD for the current version of tarsnap because the
PKGBUILD file contains the hash of the tarball which contains the PKGBUILD
file.  If you're running Arch Linux, you should know what to do with the
PKGBUILD file; but you may wish to change the pkgver=, md5sums=, and
sha256sums= lines so that you get the latest version of tarsnap.

There may be a newer version of the PKGBUILD file at

> http://www.archlinux.org/packages/community/i686/tarsnap/
> http://www.archlinux.org/packages/community/x86_64/tarsnap/

(in fact, those probably have identical PKGBUILD files).


Fedora
------

To build a Fedora package:

    sudo dnf install rpmdevtools
    sudo dnf builddep pkg/fedora/tarsnap.spec
    rpmdev-setuptree
    cp .../tarsnap-autoconf-<version>.tgz ~/rpmbuild/SOURCES
    rpmbuild -bb pkg/fedora/tarsnap.spec

Then to install it:

    sudo dnf install ~/rpmbuild/RPMS/<arch>/tarsnap-<version>-*.rpm

> Note: this spec file has been tested on Fedora; there may be some
> incompatibilities with CentOS, OpenSUSE, or other spec-file-based Linux
> distributions.


Slackware
---------

There is a SlackBuild for tarsnap (possibly an earlier version) at

> http://slackbuilds.org/repository/${VER}/system/tarsnap/

for VER = 12.2 and 13.1 (and possibly other versions by the time
you read this).


FreeBSD, OpenBSD, and pkgsrc
----------------------------

Tarsnap is in the FreeBSD ports tree, the OpenBSD ports tree, and
the pkgsrc tree as sysutils/tarsnap.
