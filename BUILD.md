Build Instructions
==================

PAPPL requires Microsoft® Windows® 10 or higher or a POSIX-compliant host
operating system such as Linux®, macOS®, QNX®, or VxWorks®.  On Windows, the
provided project files require Visual Studio 2019 or higher.  For POSIX hosts,
a "make" utility that supports the `include` directive (like GNU make), a
C99-compatible C compiler such as GCC or Clang, and the "pkg-config" utility
are required along with the following support libraries:

- Avahi 0.8 or later (most operating systems) or mDNSResponder (macOS and
  Windows) for mDNS/DNS-SD support
- CUPS 2.2 or later for the CUPS libraries
- GNU TLS 3.0 or later (except on macOS and Windows) for TLS support
- JPEGLIB 8 or later or libjpeg-turbo 2.0 or later for JPEG image support
  (optional for B&W printers)
- LIBPNG 1.6 or later for PNG image support (optional)
- LIBPAM for authentication support (optional)
- LIBUSB 1.0 or later for USB printing support (optional)
- PAM for authentication support (optional)
- ZLIB 1.1 or later for compression support


Getting Prerequisites
---------------------

CentOS 7/Fedora 22/RHEL 7:

    sudo yum groupinstall 'Development Tools'
    sudo yum install avahi-devel cups-devel gnutls-devel libjpeg-turbo-devel \
        libpng-devel libusbx-devel pam-devel zlib-devel

CentOS 8/Fedora 23+/RHEL 8:

    sudo dnf groupinstall 'Development Tools'
    sudo dnf install avahi-devel cups-devel gnutls-devel libjpeg-turbo-devel \
        libpng-devel libusbx-devel pam-devel zlib-devel

Debian/Raspbian/Ubuntu:

    sudo apt-get install build-essential libavahi-client-dev libcups2-dev \
        libcupsimage2-dev libgnutls28-dev libjpeg-dev libpam-dev libpng-dev \
        libusb-1.0-0-dev zlib1g-dev

macOS (after installing Xcode from the AppStore):

    (install brew if necessary)
    brew install libjpeg
    brew install libpng
    brew install libusb

or download, build, and install libjpeg, libpng, and libusb from source.

Windows (after installing Visual Studio 2019 or later) will automatically
install the prerequisites via NuGet packages.


Building PAPPL
--------------

PAPPL uses the usual `configure` script to generate a `make` file:

    ./configure [options]
    make

Use `./configure --help` to see a full list of options.

There is also an Xcode project under the `xcode` directory that can be used on
macOS:

    open xcode/pappl.xcodeproj

and a Visual Studio solution under the `vcnet` directory that must be used on
Windows.

You can test the build by running the PAPPL test program:

    testsuite/testpappl


Installing PAPPL
----------------

Once you have successfully built PAPPL, install it using:

    sudo make install

By default everything will be installed under `/usr/local`.  Use the `--prefix`
configure option to override the base installation directory.  Set the
`DESTDIR`, `DSTROOT`, or `RPM_BUILD_ROOT` environment variables to redirect the
installation to a staging area, as is typically done for most software packaging
systems (using one of those environment variables...)
