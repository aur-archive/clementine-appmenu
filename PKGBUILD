# $Id$
#Maintainer: Stéphane Gaudreault <stephane@archlinux.org>
#Contributor: BlackEagle <ike.devolder@gmail.com>
#Contributor: Dany Martineau <dany.luc.martineau@gmail.com>

pkgname=clementine-appmenu
pkgdown=clementine
pkgver=1.0.1
pkgrel=8
pkgdesc="A music player and library organizer (with appmenu support)"
url="http://www.clementine-player.org/"
license=('GPL')
arch=('i686' 'x86_64')
depends=('gstreamer0.10-base' 'taglib' 'glew' 'liblastfm' 'libgpod'
         'libmtp' 'libplist' 'hicolor-icon-theme' 'qt' 'libimobiledevice'
         'qjson' 'libcdio' 'protobuf' 'qca' 'qca-ossl' 'gvfs')
makedepends=('cmake' 'boost')
conflicts=('clementine')
provides=('clementine')
replaces=('clementine')
optdepends=('gstreamer0.10-base-plugins: for more open formats'
            'gstreamer0.10-good-plugins: for use with "Good" plugin libraries'
            'gstreamer0.10-bad-plugins: for use with "Bad" plugin libraries'
            'gstreamer0.10-ugly-plugins: for use with "Ugly" plugin libraries')
source=(http://clementine-player.googlecode.com/files/${pkgdown}-${pkgver}.tar.gz
        clementine-fix-albumcoverfetch-crash.patch
        clementine-fresh-start.patch
        imobiledevice.patch
        appmenu.patch
        clementine_nvidia.patch)
sha1sums=('e05320da689e2fad744fd3e68518bc4103ecf0fd'
          'fddd2e784181ce1dcc7809e7122cbade0af7b01f'
          'd8abab4b8fb2d5284a2f43107505325e62d4af5f'
          'd1917fc81d297bb3dd8f277bf5e2bcd6a57ec3bb'
	  'c8470b9873a7eaa0e10564715904e744f4136d6f'
          'db7410f151032144c58c5a7600d04a4d27add9ee')
install=clementine.install

build() {
   cd "${srcdir}/${pkgdown}-${pkgver}"

   # https://bugs.gentoo.org/401713?id=401713
   patch -Np1 -i ../clementine-fresh-start.patch

   # http://code.google.com/p/clementine-player/issues/detail?id=2752
   patch -Np1 -i ../clementine-fix-albumcoverfetch-crash.patch

   # Use libimobiledevice new "udid" field instead of "uuid".
   patch -Np1 -i ../imobiledevice.patch

   # Re enable appmenu
   patch -Np1 -i ../appmenu.patch

   # NVIDIA SUX  
   patch -Np1 -i ../clementine_nvidia.patch

   cmake . -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release
   make
}

package() {
   cd "${srcdir}/${pkgdown}-${pkgver}"
   make DESTDIR="${pkgdir}" install
}
