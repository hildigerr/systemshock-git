# Maintainer: Hildigerr Vergaray <Maintainer at YmirSystems dot com>
pkgname=systemshock-git
pkgver=0.7.8_g38ede87e_dirty
pkgrel=2
pkgdesc="Cross platform port of System Shock"
arch=('x86_64')
url="https://github.com/Interrupt/systemshock"
license=('GPL' 'CCPL')
depends=('sdl2_mixer')
makedepends=('git' 'cmake')
provides=("${pkgname%-git}")
install=systemshock.install
source=(
    "${pkgname%-git}::git+${url}"
    "nobundle.patch"
    "xxx-user-home-res-dir.patch"
    "http://icons.iconarchive.com/icons/3xhumed/mega-games-pack-25/256/Systemshock-1-icon.png"
    "${pkgname%-git}.desktop"
)
md5sums=(
    'SKIP'
    '63a0155056bbc57db0562747c13c57d9'
    '61fadcac0da1e6998267ecc666f11f47'
    '22201fe8de40c18cc6acdf06a3eff5fe'
    'ea3f0561699c7a5b624e44ae3f4390e8'
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
	install -Dm755 "$srcdir/${pkgname%-git}/systemshock" "$pkgdir/usr/bin/systemshock"
    install -Dm644 "Systemshock-1-icon.png" "$pkgdir/usr/share/pixmaps/Systemshock-1-icon.png"
    install -Dm644 "${pkgname%-git}.desktop" "$pkgdir/usr/share/applications/${pkgname%-git}.desktop"
}
