# Maintainer: alba4k <blaskoazzolaaaron@gmail.com>

_pkgname="hyprutils"
pkgname="${_pkgname}-git"
pkgver=0.1.1.r3.g0693f939
pkgrel=1
pkgdesc="Hyprland utilities library used across the ecosystem"
arch=(any)
url="https://github.com/hyprwm/hyprwayland-scanner"
license=('BSD-3-Clause')
depends=()
makedepends=('git' 'cmake' 'gcc')
source=("${_pkgname}::git+https://github.com/hyprwm/hyprutils.git")
provides=("hyprutils")
conflicts=("hyprutils")
sha256sums=('SKIP')

pkgver() {
	cd ${_pkgname}
    git describe --long --tags --abbrev=8 --exclude='*[a-zA-Z][a-zA-Z]*' \
      | sed -E 's/^[^0-9]*//;s/([^-]*-g)/r\1/;s/-/./g'
}

build() {
	cd "${srcdir}/${_pkgname}"
	cmake --no-warn-unused-cli -DCMAKE_BUILD_TYPE:STRING=Release -DCMAKE_INSTALL_PREFIX:PATH=/usr -S . -B ./build
	cmake --build ./build --config Release --target all -j`nproc 2>/dev/null || getconf _NPROCESSORS_CONF`
}

package() {
	cd "${srcdir}/${_pkgname}"
	DESTDIR="${pkgdir}" cmake --install build

	install -Dm644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
