# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: The Almighty Pegasus Epsilon <pegasus@pimpninjas.org>
pkgname=arch-libtsm-custom
pkgver=v4.0.1_1_g502ff6e
pkgrel=1
pkgdesc="Terminal-emulator State Machine. Patched up nice."
arch=('i686' 'x86_64')
url="https://github.com/Aetf/libtsm"
license=('GPL')
provides=('libtsm')
conflicts=('libtsm' 'libtsm-git' 'libtsm-patched-git')
replaces=('libtsm' 'libtsm-git' 'libtsm-patched-git')
source=("colorfix.diff")
md5sums=('8b46d269678776be2e31a15bd4eb9c7e')

prepare() {
	rm colorfix.diff
	git clone https://github.com/Aetf/libtsm.git . || \
	git reset --hard && git pull
	patch -Np1 -i ../colorfix.diff || true
}

build() {
	mkdir build || true
	cd build
	cmake .. -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_INSTALL_LIBDIR:PATH=lib
#	test -f ./configure || NOCONFIGURE=1 ./autogen.sh
#	./configure --prefix=/usr
	make
}

#check() { cd build; make -k check; }
package() { cd build; make DESTDIR="$pkgdir/" install; }
pkgver() { git describe --always | sed -e 's/-/_/g'; }
