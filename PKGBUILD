pkgname=clownmdemu-git
pkgver=1.5.r219.g7c23000
pkgrel=1
pkgdesc="ClownMDEmu, a Sega Mega Drive/Sega Genesis emulator."
arch=('x86_64' 'aarch64')
url="https://clownacy.wordpress.com"
license=('GPL')
depends=('sdl3')
makedepends=("git" "cmake" "gcc")
options=('!debug' 'strip')
source=("git+https://github.com/Clownacy/clownmdemu-frontend.git")
sha256sums=('SKIP')

pkgver() {
	cd clownmdemu
	git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
    mv clownmdemu-frontend clownmdemu
    cd clownmdemu
    git submodule update --init --recursive
    cd ..
}

build() {
    cd "${srcdir}/clownmdemu"
    cmake -B build . \
    -DCMAKE_BUILD_TYPE=Release \
    -DCMAKE_INSTALL_PREFIX="/usr" \
    -DCMAKE_INTERPROCEDURAL_OPTIMIZATION=ON \
    -DCMAKE_POLICY_DEFAULT_CMP0069=NEW \
    -DCLOWNMDEMU_FRONTEND_FREETYPE=ON

    cmake --build build
}

package() {
    cd "${srcdir}/clownmdemu"
    DESTDIR="$pkgdir/" cmake --install build
}
