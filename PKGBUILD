# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Eric Bélanger <eric@archlinux.org>

pkgname=xscreensaver-federation-logo
appname=xscreensaver
pkgver=6.00
pkgrel=1
pkgdesc='Screen saver and locker for the X Window System'
url='https://www.jwz.org/xscreensaver/'
arch=('x86_64')
license=('BSD')
depends=(
  'gtk2' 'glu' 'xorg-appres' 'libglvnd' 'libjpeg-turbo' 'libjpeg.so'
  'libsystemd.so' 'libx11' 'libxcrypt' 'libcrypt.so' 'libxext' 'libxft' 'libxi'
  'libxinerama' 'libxmu' 'libxrandr' 'libxt' 'libxxf86vm' 'perl-libwww' 'pam'
  'libpam.so' 'glibc' 'glib2' 'gdk-pixbuf2' 'gdk-pixbuf-xlib'
)
makedepends=('bc' 'intltool' 'libxpm' 'gdm' 'systemd' 'systemd-libs')
optdepends=('gdm: for login manager support')
backup=('etc/pam.d/xscreensaver')
source=(https://www.jwz.org/xscreensaver/${appname}-${pkgver}.tar.gz
        LICENSE
        logo-50.xpm
        logo-180.xpm)
sha512sums=('7292bacf633137b5c0eb2de9a99dc238b2012a113e62c86d4be19fc2fd4fea7133bd950253ca2d3a4ab27af4b4dc9a40a857e8d3dc714946ccfa7efcd043ded6'
            '863c699479b2ec2775a0d1cba22e615929194a14af164b3513e46a0c04229da6547255a4da8f7f1bbb40906898c124ed3c9ec2436b76b62affcb62385af9783e'
            'a02126dd0e18f6bd56944e407f1cfa325fb3c5f5945d633490d3a8c0964f9fa35ba7766f759edfb5d8711997a34e45bac6632c0b9a4c96d2bdbfde7630c7f483'
            'f5730a4146b18e1fdfedec93fd1a27a6f2a02a665adb5b965403db964233028a4231d45b0afdd951d78d4936db55e9dcc728cd0e45596c1507f9e682755c53f3')
conflicts=('xscreensaver')
provides=('xscreensaver')

prepare() {
  cd ${appname}-${pkgver}
  ls -la "${srcdir}"/${appname}-${pkgver}/utils/images/
  install -Dm644 "$srcdir"/logo-50.xpm  "${srcdir}"/${appname}-${pkgver}/utils/images/logo-50.xpm
  install -Dm644 "$srcdir"/logo-180.xpm  "${srcdir}"/${appname}-${pkgver}/utils/images/logo-180.xpm
}

build() {
  cd ${appname}-${pkgver}
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --localstatedir=/var \
    --libexecdir=/usr/lib \
    --with-x-app-defaults=/usr/share/X11/app-defaults \
    --without-setuid-hacks \
    --without-setcap-hacks \
    --with-pam \
    --with-login-manager \
    --with-gtk \
    --with-gl \
    --without-gle \
    --with-pixbuf \
    --with-jpeg
  make
}

package() {
  cd ${appname}-${pkgver}
  install -d "${pkgdir}/etc/pam.d"
  make install_prefix="${pkgdir}" install
  install -Dm 644 ../LICENSE -t "${pkgdir}/usr/share/licenses/${appname}"
  echo "NotShowIn=KDE;GNOME;" >> "${pkgdir}/usr/share/applications/xscreensaver-properties.desktop"
}

# vim: ts=2 sw=2 et:
