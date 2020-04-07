# Maintainer: Hildigerr Vergaray <Maintainer at YmirSystems dot com>
pkgname=systemshock-git
pkgver=0.7.8_g38ede87e_dirty
pkgrel=1
pkgdesc="Cross platform port of System Shock"
arch=('x86_64')
url="https://github.com/Interrupt/systemshock"
license=('GPL')
depends=('sdl2_mixer')
makedepends=('git' 'cmake')
provides=("${pkgname%-git}")
install=systemshock.install
source=(
    "${pkgname%-git}::git+${url}"
    "nobundle.patch"
    "xxx-user-home-res-dir.patch"
)
md5sums=(
    'SKIP'
    '63a0155056bbc57db0562747c13c57d9'
    '61fadcac0da1e6998267ecc666f11f47'
)

pkgver() {
	cd "$srcdir/${pkgname%-git}"

    # Match VERSION with what the executable will report
    #  should match with generated src/GameSrc/Headers/shockolate_version.h
	printf "%s_%s" \
    "$(grep 'shockolate VERSION' CMakeLists.txt | awk '{printf "%s", $3}' | sed s/\)//)" \
    "$(git describe --dirty | awk -F- '{printf "%s_%s", $3, $4}')"
}

prepare() {
	cd "$srcdir/${pkgname%-git}"
	patch -p1 -i "../nobundle.patch"
    patch -p1 -i "../xxx-user-home-res-dir.patch"
}

build() {
	cd "$srcdir/${pkgname%-git}"
	cmake .
	make systemshock
}

package() {
    mkdir -p "$pkgdir/usr/bin/"
	mv "$srcdir/${pkgname%-git}/systemshock" "$pkgdir/usr/bin/"
}
