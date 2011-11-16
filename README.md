This directory contains the patches necessary to build OpenSSH-LPK packages
for Debian Squeeze.

64-bit packages are available at apt.c--g.net

## Setup

    # Install some required packages
    apt-get install libssl-dev libpam0g-dev libgtk2.0-dev libedit-dev libkrb5-dev libwrap0-dev quilt libselinux1-dev libldap2-dev
    # Configure [dquilt](http://www.debian.org/doc/manuals/maint-guide/modify.en.html#quiltrc) by adding to your .bashrc:
    alias dquilt="quilt --quiltrc=${HOME}/.quiltrc-dpkg" 


## Build instructions

    apt-get source openssh
    cd openssh-5.5p1
    dquilt pop -a
    dquilt import ../contrib-openssh-lpk-5.5p1-0.3.13.patch
    dquilt push
    dquilt refresh
    cp ../package-versioning.patch debian/patches/
    while dquilt push
    do
      dquilt refresh
    done
    dquilt import ../lpk-makefile.patch
    dquilt push

Edit debian/changelog: Add a version with a new version (which should be higher than the existing). So if the old version is 1:5.5p1-6+squeeze1, go with 1:5.5p1-6+squeeze1cg. Explain the reason for the reroll.

    dpkg-buildpackage -rfakeroot -b -uc

and then deploy the packages openssh*.deb to your repository.

## Resources

There is more information in the resources-old directory, including a README.md.

However, the contrib-openssh-lpk-5.5p1-0.3.13.patch was edited by single line in version.h to update the version, and this patch then applies. It originally came from the repository at http://code.google.com/p/openssh-lpk/source/checkout

The other two patches in this directory I rolled to make things work.
