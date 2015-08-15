# Maintainer: speps <speps at aur dot archlinux dot org>

pkgname=gamgi
pkgver=0.16.3
pkgrel=1
pkgdesc="General Atomistic Modelling Graphic Interface is a free package to construct, view and analyse atomic structures."
arch=('i686' 'x86_64')
url="http://www.gamgi.org/"
license=('GPL')
depends=('gtkglext' 'hicolor-icon-theme')
options=('!emptydirs')
install="$pkgname.install"
source=("${url}src/${pkgname}-all-${pkgver}.tar.gz"
        "${pkgname}.desktop" "$pkgname.sh")
md5sums=('4a9546ec1cb968292724a13a2e96c855'
         'b558e09451368776b70e168c8f8e6c13'
         'b00fd8a0898471a15d075c26b6b621f6')

build() {
  cd "$srcdir/$pkgname$pkgver/src"
  make
}

package() {
  cd "$srcdir/$pkgname$pkgver"

  # bin
  install -Dm755 src/$pkgname "$pkgdir/usr/bin/$pkgname"

  # desktop file
  install -Dm644 ../$pkgname.desktop \
    "$pkgdir/usr/share/applications/$pkgname.desktop"

  # icons
  for _s in 16 22 32 48; do
    install -Dm644 doc/icon/$pkgname$_s.png \
      "$pkgdir/usr/share/icons/hicolor/${_s}x${_s}/apps/$pkgname.png"
  done

  # man
  install -Dm644 doc/man/page "$pkgdir/usr/share/man/man1/$pkgname.1"

  # docs
  install -d "$pkgdir/usr/share/doc/$pkgname"
  cp -a doc/*[^man] "$pkgdir/usr/share/doc/$pkgname"

  # data files and examples
  install -d "$pkgdir/usr/share/$pkgname"
  cp -a dat/* "$pkgdir/usr/share/$pkgname"

  # custom profile.d
  install -Dm755 "$srcdir/$pkgname.sh" \
    "$pkgdir/etc/profile.d/$pkgname.sh"
}
