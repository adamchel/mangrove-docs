+++
date = "2016-07-15T17:10:05-04:00"
next = "/1-basics/quick-tour"
prev = "/1-basics/what-is-mangrove"
title = "Installation"
toc = true
weight = 2

+++

To get Mangrove up and running in your project, simply follow these instructions to install Mangrove on your system.

## Prerequisites

1. OS X or any other standard 'nix platform.
2. A modern compiler that supports C++14.
	* Mangrove has been confirmed to work with Clang 3.8+, Apple Clang 7.3+, or GCC 6.1+.
3. CMake 3.2+. 
4. The MongoDB C driver version 1.3.5+. (see below)
5. The MongoDB C++ driver version 3.0.2+. (see below)
6. *(Optional)* pkg-config

## Build and install the C driver

Mangrove uses {{% a_blank "libbson" "https://api.mongodb.com/libbson/current/" %}} and the {{% a_blank "MongoDB C driver" "https://api.mongodb.com/c/current/" %}} internally. If you don't already have a new enough version of the C driver and libbson installed, then you need to build them.

Build and install the C driver according to the section {{% a_blank "Building From a Release Tarball" "https://api.mongodb.com/c/current/installing.html#unix-build" %}} in the install instructions. The C driver installs libbson if necessary.

## Build and install the C++11 driver

Mangrove also uses the {{% a_blank "MongoDB C++11 Driver" "https://github.com/mongodb/mongo-cxx-driver" %}} internally.

Build and install the C++ driver according to its {{% a_blank "quickstart guide" "https://github.com/mongodb/mongo-cxx-driver/wiki/Quickstart-Guide-(New-Driver)" %}}.

## Build and install Mangrove

* Clone the repository, and check out the latest stable release.
    - `git clone -b master https://github.com/mongodb/mongo-cxx-odm`

* Build Mangrove. Note that if you installed the C driver and C++ driver to a path that is automatically searched by `pkg-config`, you can omit the `PKG_CONFIG_PATH` environment variable. If you don't have `pkg-config`, you can explicitly set the path to the libbson, libmongoc, libbsoncxx, and libmongocxx install prefixes with the `-DLIBBSON_DIR`, `-DLIBMONGOC_DIR`, -`Dlibbsoncxx_DIR`, and `-Dlibmongocxx_DIR` CMake arguments.
   - `cd mongo-cxx-odm/build`
   - `[PKG_CONFIG_PATH=CXXDRIVER_INSTALL_PATH/lib/pkgconfig] cmake -DCMAKE_BUILD_TYPE=Release [-DCMAKE_INSTALL_PREFIX=CXXDRIVER-INSTALL-PATH] ..`
   - `make && sudo make install`

