# Aircrack-ng

[![Linux/Mac Build Status](https://travis-ci.org/aircrack-ng/aircrack-ng.svg?branch=master)](https://travis-ci.org/aircrack-ng/aircrack-ng)
[![Windows Build Status](https://ci.appveyor.com/api/projects/status/github/aircrack-ng/aircrack-ng?branch=master&svg=true)](https://ci.appveyor.com/project/aircrack-ng/aircrack-ng)
[![Intel Compiler Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng.svg?left_text=Intel%20Compiler%20Build)](https://buildbot.aircrack-ng.org/)
[![Alpine Linux Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-alpine.svg?left_text=Alpine%20Linux%20Build)](https://buildbot.aircrack-ng.org/)
[![Kali Linux Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-kali.svg?left_text=Kali%20Linux%20Build)](https://buildbot.aircrack-ng.org/)
[![Armel Kali Linux Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-armel.svg?left_text=Armel%20Kali%20Linux%20Build)](https://buildbot.aircrack-ng.org/)
[![Armhf Kali Linux Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-armhf.svg?left_text=Armhf%20Kali%20Linux%20Build)](https://buildbot.aircrack-ng.org/)
[![DragonFly BSD Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-dfly.svg?left_text=DragonFly%20Build)](https://buildbot.aircrack-ng.org/)
[![FreeBSD 11 Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-fbsd-11.svg?left_text=FreeBSD%2011%20Build)](https://buildbot.aircrack-ng.org/)
[![FreeBSD 12 Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-fbsd-12.svg?left_text=FreeBSD%2012%20Build)](https://buildbot.aircrack-ng.org/)
[![OpenBSD 6 Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-obsd.svg?left_text=OpenBSD%20Build)](https://buildbot.aircrack-ng.org/)
[![NetBSD 8.1 Build Status](https://buildbot.aircrack-ng.org/badges/aircrack-ng-netbsd81.svg?left_text=NetBSD%20Build)](https://buildbot.aircrack-ng.org/)
[![Coverity Scan Build Status](https://scan.coverity.com/projects/aircrack-ng/badge.svg)](https://scan.coverity.com/projects/aircrack-ng)
[![PackageCloud DEB](https://img.shields.io/badge/deb-packagecloud.io-844fec.svg)](https://packagecloud.io/aircrack-ng/git/install#bash-deb)
[![PackageCloud RPM](https://img.shields.io/badge/rpm-packagecloud.io-844fec.svg)](https://packagecloud.io/aircrack-ng/git/install#bash-rpm)

Aircrack-ng is a complete suite of tools to assess WiFi network security.

It focuses on different areas of WiFi security:
 * Monitoring: Packet capture and export of data to text files for further processing by third party tools.
 * Attacking: Replay attacks, deauthentication, fake access points and others via packet injection.
 * Testing: Checking WiFi cards and driver capabilities (capture and injection).
 * Cracking: WEP and WPA PSK (WPA 1 and 2).

All tools are command line which allows for heavy scripting. A lot of GUIs have taken advantage of this feature. It works primarily Linux but also Windows, OS X, FreeBSD, OpenBSD, NetBSD, as well as Solaris and even eComStation 2. 

# Building

## Requirements

 * Autoconf
 * Automake
 * Libtool
 * shtool
 * OpenSSL development package or libgcrypt development package.
 * Airmon-ng (Linux) requires ethtool, usbutils, and often pciutils.
 * On windows, cygwin has to be used and it also requires w32api package.
 * On Windows, if using clang, libiconv and libiconv-devel
 * Linux: LibNetlink 1 or 3. It can be disabled by passing --disable-libnl to configure.
 * pkg-config (pkgconf on FreeBSD)
 * FreeBSD, OpenBSD, NetBSD, Solaris and OS X with macports: gmake
 * Linux/Cygwin: make and Standard C++ Library development package (Debian: libstdc++-dev)

Note: Airmon-ng only requires pciutils if the system has a PCI/PCIe bus and it is populated.
      Such bus can be present even if not physically visible. For example, it is present,
      and populated on the Raspberry Pi 4, therefore pciutils is required on that device.

## Optional stuff

 * If you want SSID filtering with regular expression in airodump-ng
   (-essid-regex) pcre development package is required.
 * If you want to use airolib-ng and '-r' option in aircrack-ng,
   SQLite development package >= 3.3.17 (3.6.X version or better is recommended)
 * If you want to use Airpcap, the 'developer' directory from the CD/ISO/SDK is required.
 * In order to build `besside-ng`, `besside-ng-crawler`, `easside-ng`, `tkiptun-ng` and `wesside-ng`,
   libpcap development package is required (on Cygwin, use the Aircap SDK instead; see above)
 * rfkill
 * If you want Airodump-ng to log GPS coordinates, gpsd is needed
 * For best performance on SMP machines, ensure the hwloc library and headers are installed. It is strongly recommended on high core count systems, it may give a serious speed boost
 * CMocka for unit testing
 * For intergation testing on Linux only: tcpdump, HostAPd, WPA Supplicant and screen

## Installing required and optional dependencies

Below are instructions for installing the basic requirements to build
`aircrack-ng` for a number of operating systems.

**Note**: CMocka, tcpdump, screen, HostAPd and WPA Supplicant should not be dependencies when packaging Aircrack-ng.

### Linux

#### Debian/Ubuntu

    sudo apt-get install build-essential autoconf automake libtool pkg-config libnl-3-dev libnl-genl-3-dev libssl-dev ethtool shtool rfkill zlib1g-dev libpcap-dev libsqlite3-dev libpcre3-dev libhwloc-dev libcmocka-dev hostapd wpasupplicant tcpdump screen iw usbutils

#### Fedora

    sudo yum install libtool pkgconfig sqlite-devel autoconf automake openssl-devel libpcap-devel pcre-devel rfkill libnl3-devel gcc gcc-c++ ethtool hwloc-devel libcmocka-devel make file expect hostapd wpa_supplicant iw usbutils tcpdump screen

#### CentOS/RHEL

CentOS/RHEL 7:
    sudo yum install epel-release
    sudo ./centos_autotools.sh
    # Remove older installation 
    sudo yum remove autoconf automake
    sudo yum install sqlite-devel openssl-devel libpcap-devel pcre-devel rfkill libnl3-devel ethtool hwloc-devel libcmocka-devel make file expect hostapd wpa_supplicant iw usbutils tcpdump screen

**Note**: autoconf and automake in CentOS 7 repositories are too old. We are providing a script to install more recent version called centos_autotools.sh. It automatically install dependencies required for the installation of autotools and automake and compiles them from source

CentOS/RHEL 8:
    sudo yum config-manager --set-enabled powertools
    sudo yum install epel-release
    sudo yum install libtool pkgconfig sqlite-devel autoconf automake openssl-devel libpcap-devel pcre-devel rfkill libnl3-devel gcc gcc-c++ ethtool hwloc-devel libcmocka-devel make file expect hostapd wpa_supplicant iw usbutils tcpdump screen

#### openSUSE

    sudo zypper install autoconf automake libtool pkg-config libnl3-devel libopenssl-1_1-devel zlib-devel libpcap-devel sqlite3-devel pcre-devel hwloc-devel libcmocka-devel hostapd wpa_supplicant tcpdump screen iw gcc-c++ gcc

#### Mageia

    sudo urpmi autoconf automake libtool pkgconfig libnl3-devel libopenssl-devel zlib-devel libpcap-devel sqlite3-devel pcre-devel hwloc-devel libcmocka-devel hostapd wpa_supplicant tcpdump screen iw gcc-c++ gcc make

#### Alpine

    sudo apk add gcc g++ make autoconf automake libtool libnl3-dev openssl-dev ethtool libpcap-dev cmocka-dev hostapd wpa_supplicant tcpdump screen iw pkgconf util-linux sqlite-dev pcre-dev linux-headers zlib-dev

### BSD

#### FreeBSD

    pkg install pkgconf shtool libtool gcc9 automake autoconf pcre sqlite3 openssl gmake hwloc cmocka

#### DragonflyBSD

    pkg install pkgconf shtool libtool gcc8 automake autoconf pcre sqlite3 libgcrypt gmake cmocka

#### OpenBSD

    pkg_add pkgconf shtool libtool gcc automake autoconf pcre sqlite3 openssl gmake cmocka

### OSX

XCode, Xcode command line tools and HomeBrew are required.

    brew install autoconf automake libtool openssl shtool pkg-config hwloc pcre sqlite3 libpcap cmocka

### Windows

#### Cygwin

Cygwin requires the full path to the `setup.exe` utility, in order to
automate the installation of the necessary packages. In addition, it
requires the location of your installation, a path to the cached
packages download location, and a mirror URL.

An example of automatically installing all the dependencies
is as follows:

    c:\cygwin\setup-x86.exe -qnNdO -R C:/cygwin -s http://cygwin.mirror.constant.com -l C:/cygwin/var/cache/setup -P autoconf -P automake -P bison -P gcc-core -P gcc-g++ -P mingw-runtime -P mingw-binutils -P mingw-gcc-core -P mingw-gcc-g++ -P mingw-pthreads -P mingw-w32api -P libtool -P make -P python -P gettext-devel -P gettext -P intltool -P libiconv -P pkg-config -P git -P wget -P curl -P libpcre-devel -P libssl-devel -P libsqlite3-devel

#### MSYS2

    pacman -Sy autoconf automake-wrapper libtool msys2-w32api-headers msys2-w32api-runtime gcc pkg-config git python openssl-devel openssl libopenssl msys2-runtime-devel gcc binutils make pcre-devel libsqlite-devel

## Compiling

To build `aircrack-ng`, the Autotools build system is utilized. Autotools replaces
the older method of compilation.

**NOTE**: If utilizing a developer version, eg: one checked out from source control,
you will need to run a pre-`configure` script. The script to use is one of the
following: `autoreconf -i` or `env NOCONFIGURE=1 ./autogen.sh`.

First, `./configure` the project for building with the appropriate options specified
for your environment:

    ./configure <options>

**TIP**: If the above fails, please see above about developer source control versions.

Next, compile the project (respecting if `make` or `gmake` is needed):

 * Compilation:

    `make`

 * Compilation on *BSD or Solaris:

    `gmake`

Finally, the additional targets listed below may be of use in your environment:

 * Execute all unit testing:

    `make check`

 * Execute all integration testing (requires root):
 
    `make integration`

 * Installing:

    `make install`

 * Uninstall:

    `make uninstall`


###  `./configure` flags

When configuring, the following flags can be used and combined to adjust the suite
to your choosing:

* **with-airpcap=DIR**:  needed for supporting airpcap devices on windows (cygwin or msys2 only)
                Replace DIR above with the absolute location to the root of the
                extracted source code from the Airpcap CD or downloaded SDK available
                online. Required on Windows to build `besside-ng`, `besside-ng-crawler`, 
                `easside-ng`, `tkiptun-ng` and `wesside-ng` when building experimental tools.
                The developer pack (Compatible with version 4.1.1 and 4.1.3) can be downloaded at
                https://support.riverbed.com/content/support/software/steelcentral-npm/airpcap.html

* **with-experimental**: needed to compile `tkiptun-ng`, `easside-ng`, `buddy-ng`,
                    `buddy-ng-crawler`, `airventriloquist` and `wesside-ng`.
                    libpcap development package is also required to compile most of the tools.
                    If not present, not all experimental tools will be built.
                    On Cygwin, libpcap is not present and the Airpcap SDK replaces it.
                    See --with-airpcap option above.

* **with-ext-scripts**: needed to build `airoscript-ng`, `versuck-ng`, `airgraph-ng` and 
                   `airdrop-ng`. 
                   Note: Each script has its own dependencies.

* **with-gcrypt**:   Use libgcrypt crypto library instead of the default OpenSSL.
                And also use internal fast sha1 implementation (borrowed from GIT)
                Dependency (Debian): libgcrypt20-dev

* **with-duma**:	Compile with DUMA support. DUMA is a library to detect buffer overruns and under-runs.
            	Dependencies (debian): duma

* **disable-libnl**:  Set-up the project to be compiled without libnl (1 or 3). Linux option only.

* **without-opt**:  Do not enable stack protector (on GCC 4.9 and above).

* **enable-shared**:   Make OSdep a shared library.

* **disable-shared**: When combined with **enable-static**, it will statically compile Aircrack-ng.

* **with-avx512**:  On x86, add support for AVX512 instructions in aircrack-ng. Only use it when
                    the current CPU supports AVX512.

* **with-static-simd=<SIMD>**: Compile a single optimization in aircrack-ng binary. Useful when compiling
                    statically and/or for space-constrained devices. Valid SIMD options: x86-sse2,
                    x86-avx, x86-avx2, x86-avx512, ppc-altivec, ppc-power8, arm-neon, arm-asimd.
                    Must be used with --enable-static --disable-shared. When using those 2 options, the default
                    is to compile the generic optimization in the binary. --with-static-simd merely allows
                    to choose another one.

* **enable-maintainer-mode**: It is important to enable this flag when developing with Aircrack-ng. This flag enables additional compile warnings and safety features.

#### Examples:

  * Configure and compiling:

    ```
    ./configure --with-experimental
    make
    ```

  * Compiling with gcrypt:

    ```
    ./configure --with-gcrypt
    make
    ```

  * Installing:

    `make install`

  * Installing (strip binaries):
  
    `make install-strip`

  * Installing, with external scripts:

    ```
    ./configure --with-experimental --with-ext-scripts
    make
    make install
    ```

  * Testing (with sqlite, experimental and pcre)

    ```
    ./configure --with-experimental
    make
    make check
    ```

  * Compiling on OS X with macports (and all options):

    ```
    ./configure --with-experimental
    gmake
    ```

  * Compiling on OS X 10.10 with XCode 7.1 and Homebrew:

    ```
    env CC=gcc-4.9 CXX=g++-4.9 ./configure
    make
    make check
    ```

    *NOTE*: Older XCode ships with a version of LLVM that does not support CPU feature
    detection; which causes the `./configure` to fail. To work around this older LLVM,
    it is required that a different compile suite is used, such as GCC or a newer LLVM
    from Homebrew.

    If you wish to use OpenSSL from Homebrew, you may need to specify the location
    to its' installation. To figure out where OpenSSL lives, run:

    `brew --prefix openssl`

    Use the output above as the DIR for `--with-openssl=DIR` in the `./configure` line:

    ```
    env CC=gcc-4.9 CXX=g++-4.9 ./configure --with-openssl=DIR
    make
    make check
    ```

  * Compiling on FreeBSD with gcc9

    ```
    env CC=gcc9 CXX=g++9 MAKE=gmake ./configure
    gmake
    ```

  * Compiling on Cygwin with Airpcap (assuming Airpcap devpack is unpacked in Aircrack-ng directory)

    ```
    cp -vfp Airpcap_Devpack/bin/x86/airpcap.dll src
    cp -vfp Airpcap_Devpack/bin/x86/airpcap.dll src/aircrack-osdep
    cp -vfp Airpcap_Devpack/bin/x86/airpcap.dll src/aircrack-crypto
    cp -vfp Airpcap_Devpack/bin/x86/airpcap.dll src/aircrack-util
    dlltool -D Airpcap_Devpack/bin/x86/airpcap.dll -d build/airpcap.dll.def -l Airpcap_Devpack/bin/x86/libairpcap.dll.a
    autoreconf -i
    ./configure --with-experimental --with-airpcap=$(pwd)
    make
    ```

 * Compiling on DragonflyBSD with gcrypt using GCC 8

   ```
   autoreconf -i
   env CC=gcc8 CXX=g++8 MAKE=gmake ./configure --with-experimental --with-gcrypt
   gmake
   ```

 * Compiling on OpenBSD (with autoconf 2.69 and automake 1.16)

   ```
   export AUTOCONF_VERSION=2.69
   export AUTOMAKE_VERSION=1.16
   autoreconf -i
   env MAKE=gmake ./configure
   gmake
   ```

 * Compiling and debugging aircrack-ng

   ```
   export CFLAGS='-O0 -g'
   export CXXFLAGS='-O0 -g'
   ./configure --with-experimental --enable-maintainer-mode --without-opt
   make
   LD_LIBRARY_PATH=.libs gdb --args ./aircrack-ng [PARAMETERS]
   ```


# Packaging

Automatic detection of CPU optimization is done at run time. This behavior
**is** desirable when packaging Aircrack-ng (for a Linux or other distribution.)

Also, in some cases it may be desired to provide your own flags completely and
not having the suite auto-detect a number of optimizations. To do this, add
the additional flag `--without-opt` to the `./configure` line:

`./configure --without-opt`

# Using precompiled binaries

## Linux/BSD
 * Use your package manager to download aircrack-ng
 * In most cases, they have an old version.

## Windows
 * Install the appropriate "monitor" driver for your card (standard drivers doesn't work for capturing data).
 * aircrack-ng suite is command line tools. So, you have to open a commandline
   `Start menu -> Run... -> cmd.exe` then use them
 * Run the executables without any parameters to have help

# Documentation


Documentation, tutorials, ... can be found on https://aircrack-ng.org

See also manpages and the forum.

For further information check the [README](README) file

# Infrastructure sponsors

<img src="https://uploads-ssl.webflow.com/5ac3c046c82724970fc60918/5c019d917bba312af7553b49_MacStadium-developerlogo.png" alt="MacStadium" width="150" height="61">
