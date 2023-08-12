pkgname=dmenu
pkgver=5.2
pkgrel=1
pkgdesc='Generic menu for X'
url='https://tools.suckless.org/dmenu/'
arch=('x86_64')
license=('MIT')
depends=('sh' 'glibc' 'coreutils' 'libx11' 'libxinerama' 'libxft' 'freetype2' 'fontconfig' 'libfontconfig.so')
source=(
  https://dl.suckless.org/tools/dmenu-${pkgver}.tar.gz
  https://tools.suckless.org/dmenu/patches/fuzzymatch/dmenu-fuzzymatch-4.9.diff
  dmenu-fuzzyhighlight-caseinsensitive-4.9.diff
)
sha256sums=('d4d4ca77b59140f272272db537e05bb91a5914f56802652dc57e61a773d43792'
            'd9a1e759cd518348fc37c2c83fbd097232098562ebfd1edf85b51413ff524b79'
            'bd3a79967f7b5fb2de2a851c6cccfd32f046b6d7ffacc124a48e9dae325e58e5')

prepare() {
  cd ${pkgname}-${pkgver}

  echo "CPPFLAGS+=${CPPFLAGS}" >> config.mk
  echo "CFLAGS+=${CFLAGS}" >> config.mk
  echo "LDFLAGS+=${LDFLAGS}" >> config.mk

  patch -p1 -i ../dmenu-fuzzymatch-4.9.diff
  patch -p1 -i ../dmenu-fuzzyhighlight-caseinsensitive-4.9.diff
}

build() {
  cd ${pkgname}-${pkgver}
  make \
	  X11INC=/usr/include/X11 \
	  X11LIB=/usr/lib/X11 \
	  FREETYPEINC=/usr/include/freetype2
}

package() {
  cd ${pkgname}-${pkgver}
  make PREFIX=/usr DESTDIR="${pkgdir}" install
  install -Dm 644 LICENSE -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim: ts=2 sw=2 et:
