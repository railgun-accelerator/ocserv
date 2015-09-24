# Maintainer: Brian Bidulock <bidulock@openss7.org>
pkgname=ocserv
pkgver=0.10.8
pkgrel=1
pkgdesc="OpenConnect VPN Server"
arch=('i686' 'x86_64')
url="http://www.infradead.org/ocserv/"
license=('GPL2')
depends=('autogen' 'libpcl' 'gnutls' 'http-parser' 'libnl' 'libsystemd' 'pam' 'protobuf-c' 'talloc' 'libseccomp' 'freeradius-client')
makedepends=('freeradius')
backup=('etc/ocserv.config' 'etc/ocserv-passwd')
# source=("ftp://ftp.infradead.org/pub/ocserv/ocserv-$pkgver.tar.xz") # official website is down now.
source=("https://fossies.org/linux/privat/ocserv-$pkgver.tar.gz")
sha256sums=('12f26ecf1d6458285cfe0c1c51ebf5dcd60463da5cff31b1d65a46a7d124b64d')

build() {
  cd ${pkgname}-${pkgver}
  ./configure --prefix=/usr --sbindir=/usr/bin
  make
}

package() {
  cd ${pkgname}-${pkgver}
  make DESTDIR="$pkgdir" install
  install -Dm0644 doc/sample.config "$pkgdir/etc/ocserv.config"
  install -Dm0600 doc/sample.passwd "$pkgdir/etc/ocserv-passwd"
  sed -i 's/\/etc\/ocserv\/ocserv.conf/\/etc\/ocserv.config/' doc/systemd/standalone/ocserv.service # patch
  install -Dm0644 doc/systemd/standalone/ocserv.service "$pkgdir/usr/lib/systemd/system/ocserv.service"
}
