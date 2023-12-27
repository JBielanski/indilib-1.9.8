This repo contains patches for INDI library (https://www.indilib.org/) 1.9.8.
Current version of INDI can be found:
- [INDI]: https://github.com/indilib/indi/releases
- [INDI-3RDPARTY]: https://github.com/indilib/indi-3rdparty/releases
I don't use current versions on my computer for astrophotography equipment 
from specific issues with my QHY600 PH camera. For newer drivers than 1.9.8 
in CCDCiel I got incorrect image frame. 

This repository store only patches, software should be download from 
original INDI repository:
- [INDI 1.9.8]: https://github.com/indilib/indi/archive/refs/tags/v1.9.8.tar.gz
- [INDI-3RDPARTY 1.9.8]: https://github.com/indilib/indi-3rdparty/archive/refs/tags/v1.9.8.tar.gz

Software was testing only on Gentoo Linux. I create patch for oryginal packages and 
indilib ebuild with contain INDI only without 3rd-party.

Installation for GENTOO:
1) Create your local repository, base on this tutorial:
	https://wiki.gentoo.org/wiki/Creating_an_ebuild_repository
2) Copy directory indilib to your repository:
	cp -r gentoo/sci-libs/indilib /var/db/repos/${YOUR_REPOSITORY}/sci-libs/
3) Unmask your indilib and mask newer idilib version"
	echo "sci-libs/indilib:${YOUR_REPOSITORY}" >> /etc/portage/package.accept_keywords/sci-libs
	echo ">sci-libs/indilib-1.9.8-r1" >> /etc/portage/package.mask/sci-libs
4) Install auxiliary software (some should be unmasked first):
	emerge -avu dev-util/cmake dev-libs/libusb sci-libs/{libnova,gsl,fftw} dev-lang/cfortran virtual/fortran media-libs/libgphoto2 media-libs/libraw dev-cpp/gtest media-libs/{libsdl,sdl-mixer,libdc1394} sci-libs/{cfitsio,ccfits} sci-misc/fitsverify sci-astronomy/fitspng sci-geosciences/gpsd sys-apps/fxload net-wireless/limesuite
5) Install indilib
	emerge -av --quiet sci-libs/indilib

Manual installation INDI:
1) Unpack INDI and apply patch:
	tar -xf indi-1.9.8.tar.gz
	patch -p0 < patches/indilib-1.9.8-cstdint.patch
2) Create build directory and run cmake
	mkdir build && cd build
	cmake ../indi-1.9.8
3) Continue with README ../indi-1.9.8/README


Manual installation INDI-3RDPARTY:
1) Unpack INDI-3RDPARTY and apply patch:
	tar -xf indi-3rdparty-1.9.8.tar.gz
	patch -p0 < patches/indi-3rdparty-1.9.8-ctime.patch
2) Create build directory
	mkdir build && cd build
3) Use cmake according to README ../indi-3rdparty-1.9.8/README

