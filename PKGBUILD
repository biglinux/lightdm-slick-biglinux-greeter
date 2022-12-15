pkgname='lightdm-slick-biglinux-greeter'
_pkgname='slick-biglinux-greeter'
pkgver=$(date +%y.%m.%d)
_pkgver=1.6.0
pkgrel=$(date +%H%M)
pkgdesc='A slick-looking LightDM greeter for BigLinux'
arch=(i686 x86_64)
url="https://github.com/linuxmint/slick-greeter"
license=('GPL3')
https://github.com/linuxmint/slick-greeter/archive/refs/tags/1.6.0.tar.gz
source=("${url}/archive/${_pkgver}.tar.gz"
    "${_pkgname}.conf"
    "${_pkgname}.png"
    'schema-defaults.patch')
depends=('cairo' 'freetype2' 'gtk3' 'libcanberra' 'libxext' 'lightdm' 'pixman')
makedepends=('intltool' 'gnome-common' 'vala')
backup=('etc/lightdm/slick-greeter.conf')
sha256sums=('SKIP')
install=slick-biglinux-greeter.install

prepare() {
    cd ${_pkgname}-${_pkgver}
    patch -p1 -i ../schema-defaults.patch
}

build() {
    cd ${_pkgname}-${_pkgver}
    aclocal --install
    autoreconf -vfi
    intltoolize -f
    ./configure \
        --prefix=/usr \
        --sysconfdir=/etc \
        --sbindir=/usr/bin \
        --libexecdir=/usr/lib/lightdm
    make
}

package() {
    cd ${_pkgname}-${_pkgver}
    make DESTDIR="${pkgdir}" install
    # adjust launcher name
    mv $pkgdir/usr/share/xgreeters/slick-greeter.desktop \
      $pkgdir/usr/share/xgreeters/lightdm-slick-greeter.desktop
    # Install default conf 
    install -Dm644 $srcdir/$_pkgname.conf $pkgdir/etc/lightdm/$_pkgname.conf
    install -Dm644 $srcdir/$_pkgname.png $pkgdir/usr/share/slick-greeter/$_pkgname.png
}
