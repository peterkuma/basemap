# Basemap: fork with support for Windows and macOS

This is a fork of [basemap](https://github.com/matplotlib/basemap) with support
for recent Python versions (Anaconda Python 3.8) on Windows and macOS, since
the original basemap repository is discontinued and is not available on recent
versions of Python on Windows, and no longer builds on macOS.

## Installation

To install on Anaconda Python 3.8 on Windows (64-bit) in `Anaconda Prompt`:

```
pip install https://github.com/peterkuma/basemap/releases/download/v1.2.2%2Bdev.1/basemap-1.2.2dev-cp38-cp38-win_amd64.whl
```

To install on Anaconda Python 3.8 on macOS:

```
pip3 install git+https://github.com/matplotlib/basemap.git
```

## Building from source (Windows)

1. Install:

   - [Anaconda 3](https://www.anaconda.com/)
   - [Visual Studio 2019](https://visualstudio.microsoft.com/downloads/)
   - [cmake](https://cmake.org/)

2. Download and unpack:

   - [GEOS](https://trac.osgeo.org/geos/) (`geos-3.9.1.tar.bz2` or later)
   	 source code
   - basemap source code

3. Open the `Developer Command Prompt for VS 2019` from the Windows Start Menu
   and run:

   ```sh
   cd <geos-dir>
   mkdir build build
   cmake ..
   ```

   where `<geos-dir>` is the directory where you unpacked GEOS. Open `GEOS.sln`
   located in the GEOS build directory in Visual Studio 2019, set solution
   configuration to `Release` and perform `Build -> Build solution`.

4. Open the `Anaconda Prompt` from the Windows Start Menu and run:

   ```sh
   cd <basemap-dir>
   set GEOS_DIR=<geos-dir>
   python setup.py bdist_wheel
   pip install dist\basemap-1.2.2+dev-cp38-cp38-win_amd64.whl
   ```

   where `<basemap-dir>` and `<geos-dir>` are the directories where you
   unpacked the respective packages.

## About

Plot on map projections (with coastlines and political boundaries)
using matplotlib.

:warning: **Warning**: this package is being deprecated in favour of
[cartopy](https://scitools.org.uk/cartopy/docs/latest/).

## Requirements

* Python 2.6 (or higher)

* matplotlib

* numpy

* [pyproj](https://github.com/jswhit/pyproj)

* [pyshp](https://github.com/GeospatialPython/pyshp)

* The GEOS (Geometry Engine - Open Source) library (version 3.1.1 or higher).
Source code is included in the `geos-3.3.3` directory.

* On Linux, if your Python was installed via a package management system, make
sure the corresponding `python-dev` package is also installed. Otherwise, you
may not have the Python header (`Python.h`), which is required to build Python
C extensions.

### Optional

* [OWSLib](https://github.com/geopython/OWSLib) (optional) It is needed for
the `BaseMap.wmsimage` function.

* [Pillow](https://python-pillow.github.io/) (optional) It is needed for
Basemap warpimage, bluemarble, shadedrelief, and etop methods. PIL should
work on Python 2.x. Pillow is a maintained fork of PIL.

## Copyright

Source code for the GEOS library is included in the `geos-3.3.3` directory
under the terms given in `LICENSE_geos`.

The land-sea mask, coastline, lake, river and political boundary data are
extracted from datasets provided with the
[Generic Mapping Tools (GMT)](http://gmt.soest.hawaii.edu) and are included
under the terms given in `LICENSE_data`.

Everything else (including `src/_geos.c` and `src/_geos.pyx`) is licensed under
the terms given in `LICENSE`:

Copyright (C) 2011 Jeffrey Whitaker

Permission to use, copy, modify, and distribute this software and its
documentation for any purpose and without fee is hereby granted,
provided that the above copyright notices appear in all copies and that
both the copyright notices and this permission notice appear in
supporting documentation.

THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE,
INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO
EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, INDIRECT OR
CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF
USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR
OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR
PERFORMANCE OF THIS SOFTWARE.

## Documentation

See http://matplotlib.github.io/basemap/

See scripts in `examples` directory for example usage.

Read the FAQ and/or email the matplotlib-users mailing list if you have
problems or questions.

## Install

0. Install pre-requisite Python modules numpy and matplotlib.

1. Then download `basemap-X.Y.Z.tar.gz` (approx 100 MB) from the
[GitHub Releases](https://github.com/matplotlib/basemap/releases) page,
unpack and `cd` to `basemap-X.Y.Z`.

2. Install the GEOS library. If you already have it on your system, just
set the environment variable `GEOS_DIR` to point to the location of `libgeos_c`
and `geos_c.h` (if `libgeos_c` is in `/usr/local/lib` and `geos_c.h` is in
`/usr/local/include`, set `GEOS_DIR` to `/usr/local`). Then go to step (3).
If you don't have it, you can build it from the source code included with
basemap by following these steps:

	```
	 > cd geos-3.3.3
	 > export GEOS_DIR=<where you want the libs and headers to go>
	   A reasonable choice on a Unix-like system is /usr/local, or
	   if you don't have permission to write there, your home directory.
	 > ./configure --prefix=$GEOS_DIR
	 > make; make install
	```

3. `cd` back to the top level basemap directory (`basemap-X.Y.Z`) and run
the usual `python setup.py install`. Check your installation by running
``"from mpl_toolkits.basemap import Basemap"`` at the Python prompt.

4. To test, `cd` to the examples directory and run `python simpletest.py`.
To run all the examples (except those that have extra dependencies
or require an internet connection), execute `python run_all.py`.

An alternative method is using `pip`:

```
pip install --user git+https://github.com/matplotlib/basemap.git
```

## Contact

Ben Root <ben.v.root@gmail.com>

## Thanks

Special thanks to John Hunter, Andrew Straw, Eric Firing, Rob Hetland, Scott
Sinclair, Ivan Lima, Erik Andersen, Michael Hearne, Jesper Larsen, Ryan May,
David Huard, Mauro Cavalcanti, Jonas Bluethgen, Chris Murphy, Pierre
Gerard-Marchant, Christoph Gohlke, Eric Bruning, Stephane Raynaud, Tom Loredo,
Patrick Marsh, Phil Elson, and Henry Hammond for valuable contributions.
