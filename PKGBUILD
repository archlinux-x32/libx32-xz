# $Id: PKGBUILD 143671 2015-10-11 15:34:05Z fyan $
# Contributor: Pierre Schmitz <pierre@archlinux.de>
# Contributor: François Charette <firmicus@gmx.net>

pkgname=lib32-xz
_pkgbasename=xz
pkgver=5.2.2
pkgrel=1
pkgdesc='Library and command line tools for XZ and LZMA compressed files (32-bit)'
arch=('x86_64')
url='http://tukaani.org/xz/'
license=('GPL' 'LGPL' 'custom')
depends=('lib32-glibc' 'xz')
makedepends=('gcc-multilib')
source=("http://tukaani.org/xz/${_pkgbasename}-${pkgver}.tar.gz"
        "http://tukaani.org/xz/${_pkgbasename}-${pkgver}.tar.gz.sig")
md5sums=('7cf6a8544a7dae8e8106fdf7addfa28c'
         'SKIP')
validpgpkeys=('3690C240CE51B4670D30AD1C38EE757D69184620')  # Lasse Collin

build() {
	cd ${srcdir}/xz-${pkgver}

	export CC="gcc -m32"
	export PKG_CONFIG_PATH="/usr/lib32/pkgconfig"
	
	./configure --prefix=/usr \
		--libdir=/usr/lib32 \
		--disable-rpath \
		--enable-werror
	make
}

check() {
	cd ${srcdir}/xz-${pkgver}

	make check
}

package() {
	cd ${srcdir}/xz-${pkgver}
	
	make DESTDIR=${pkgdir} install

	rm -rf "${pkgdir}"/usr/{bin,include,share}
	install -d -m755 "${pkgdir}"/usr/share/licenses
	ln -s xz "$pkgdir/usr/share/licenses/lib32-xz"
}
