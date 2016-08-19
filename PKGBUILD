# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: The Almighty Pegasus Epsilon <pegasus@pimpninjas.org>
pkgname=libtsm-git-pegasus
pkgver=75018d0
pkgrel=1
pkgdesc="Terminal-emulator State Machine. Patched up nice."
arch=('any')
url="https://github.com/Aetf/libtsm"
license=('GPL')
provides=('libtsm')
conflicts=('libtsm' 'libtsm-git' 'libtsm-patched-git')
replaces=('libtsm' 'libtsm-git' 'libtsm-patched-git')
source=("colorfix.diff")
md5sums=('24c18537ca2c92790b2c4748b99e205d')

prepare() {
	rm colorfix.diff
	git clone https://github.com/Aetf/libtsm.git . || \
	git pull
	patch -Np1 -i ../colorfix.diff || true
}

build() {
	test -f ./configure || NOCONFIGURE=1 ./autogen.sh
	./configure --prefix=/usr
	make
}

check() { make -k check; }
package() { make DESTDIR="$pkgdir/" install; }
pkgver() { git describe --always; }
