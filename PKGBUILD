# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Eric Bélanger <eric@archlinux.org>

pkgname=xscreensaver-federation-logo
appname=xscreensaver
pkgver=5.44
pkgrel=1
pkgdesc='Screen saver and locker for the X Window System'
url='https://www.jwz.org/xscreensaver/'
arch=('x86_64')
license=('BSD')
depends=('libglade' 'libxmu' 'glu' 'xorg-appres' 'perl-libwww' 'libsystemd.so'
         'libxcrypt' 'libcrypt.so' 'libxi' 'libxxf86vm' 'libxrandr' 'libxinerama'
         'libxt' 'libx11' 'libxext' 'pam' 'glibc' 'gdk-pixbuf-xlib')
makedepends=('bc' 'intltool' 'libxpm' 'gdm' 'systemd' 'systemd-libs')
optdepends=('gdm: for login manager support')
backup=('etc/pam.d/xscreensaver')
source=(https://www.jwz.org/xscreensaver/${appname}-${pkgver}.tar.gz
        LICENSE
        xanalogtv-fix.diff
        logo-50.xpm
        logo-180.xpm)
sha512sums=('9d9144dec6f075c2d6a1c3cd45123a98d6d0cd732d6c3e3389e97b3f802b8f8765a188d1e35f97f123ca0a64661ea616b7b710577063c311da3d99d8439f1dae'
            '863c699479b2ec2775a0d1cba22e615929194a14af164b3513e46a0c04229da6547255a4da8f7f1bbb40906898c124ed3c9ec2436b76b62affcb62385af9783e'
            '41d98351adc515401db15894cfec6f625ff9a60c6523997ddfecf7cefcefd2dd8342ba59ed321257ca13e54dd2329722caf506555c0b1391eda2129b7a3301da'
            'a02126dd0e18f6bd56944e407f1cfa325fb3c5f5945d633490d3a8c0964f9fa35ba7766f759edfb5d8711997a34e45bac6632c0b9a4c96d2bdbfde7630c7f483'
            'f5730a4146b18e1fdfedec93fd1a27a6f2a02a665adb5b965403db964233028a4231d45b0afdd951d78d4936db55e9dcc728cd0e45596c1507f9e682755c53f3')
conflicts=('xscreensaver')
provides=('xscreensaver')

prepare() {
  cd ${appname}-${pkgver}
  patch -p0 -i "${srcdir}/xanalogtv-fix.diff"
  install -Dm644 "$srcdir"/logo-50.xpm  "${srcdir}"/${appname}-${pkgver}/utils/images/logo-50.xpm
  install -Dm644 "$srcdir"/logo-180.xpm  "${srcdir}"/${appname}-${pkgver}/utils/images/logo-180.xpm
  sed 's|-std=c89||' -i configure.in
  autoreconf -fiv
}

build() {
  cd ${appname}-${pkgver}
  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --localstatedir=/var \
    --libexecdir=/usr/lib \
    --with-x-app-defaults=/usr/share/X11/app-defaults \
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
  # remove sticky bit
  chmod 755 "${pkgdir}/usr/bin/xscreensaver"
  echo "NotShowIn=KDE;GNOME;" >> "${pkgdir}/usr/share/applications/xscreensaver-properties.desktop"
}

# vim: ts=2 sw=2 et:
