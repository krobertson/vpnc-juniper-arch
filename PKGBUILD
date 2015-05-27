# $Id$
# Maintainer: Dave Reisner <dreisner@archlinux.org>
# Contributor: Thomas Baechler <thomas@archlinux.org>

pkgname=vpnc-juniper
pkgver=0.5.3.juniper2
pkgrel=1
pkgdesc="VPN client for cisco3000 VPN Concentrators"
url="http://www.unix-ag.uni-kl.de/~massar/vpnc/"
license=('GPL')
depends=('libgcrypt' 'openssl' 'iproute2')
makedepends=('git')
optdepends=('openresolv: Let vpnc manage resolv.conf')
arch=('i686' 'x86_64')
provides=(vpnc)
conflicts=(vpnc)
source=("vpnc::git://github.com/krobertson/vpnc-juniper.git"
        "vpnc-scripts::git://git.infradead.org/users/dwmw2/vpnc-scripts.git#commit=df5808b"
        'vpnc.conf'
        'vpnc@.service')
backup=('etc/vpnc/default.conf')
md5sums=('SKIP'
         'SKIP'
         'a3f4e0cc682f437e310a1c86ae198e45'
         '09cfded435c43dd2adb5a8863bd74cfc')

prepare() {
  # Build hybrid support
  sed -i 's|^#OPENSSL|OPENSSL|g' vpnc/Makefile

  # fix resolvconf location for community/openresolv
  sed -i 's|/sbin/resolvconf|/usr&|g' vpnc-scripts/vpnc-script
}

build() {
  cd vpnc
  make
}

package() {
  cd vpnc

  make DESTDIR="$pkgdir" PREFIX=/usr SBINDIR=/usr/bin install

  install -Dm644 "$srcdir"/vpnc.conf "$pkgdir"/etc/vpnc/default.conf
  install -Dm755 "$srcdir"/vpnc-scripts/vpnc-script "$pkgdir"/etc/vpnc/vpnc-script

  install -Dm644 "$srcdir"/vpnc@.service "$pkgdir"/usr/lib/systemd/system/vpnc@.service
}
