# Maintainer: Daniel Kirchner <daniel at ekpyron dot org>

pkgname=mingw-w64-freetype
pkgver=2.5.5
pkgrel=2
pkgdesc="TrueType font rendering library (mingw-w64)"
arch=('any')
url="http://www.freetype.org/"
license=('GPL')
depends=(mingw-w64-zlib mingw-w64-crt)
makedepends=(mingw-w64-gcc mingw-w64-configure)
source=(http://download.savannah.gnu.org/releases/freetype/freetype-$pkgver.tar.gz)
options=(!strip !buildflags !libtool staticlibs)
md5sums=('7448edfbd40c7aa5088684b0a3edb2b8')

_architectures="i686-w64-mingw32 x86_64-w64-mingw32"

build() {
  for _arch in ${_architectures}; do
    mkdir -p "${srcdir}/freetype-${pkgver}/build-${_arch}"
    cd "${srcdir}/freetype-${pkgver}/build-${_arch}"
    ${_arch}-configure --with-zlib=/usr/${_arch} --without-png
    make
  done
}

package () {
  for _arch in ${_architectures}; do
  	cd "${srcdir}/freetype-${pkgver}/build-${_arch}"
  	make DESTDIR="${pkgdir}" install
    rm -rf "${pkgdir}/usr/${_arch}/share/"
  	${_arch}-strip -g "${pkgdir}/usr/${_arch}/lib/"*.a
  	${_arch}-strip --strip-unneeded "$pkgdir"/usr/${_arch}/bin/*.dll
  done
}
