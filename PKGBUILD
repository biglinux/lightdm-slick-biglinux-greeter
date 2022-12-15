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
sha256sums=('9f0ca551dc921c83e6c302fa8582b615ff1423c691eb7fa711719af64ee8166c'
            'a015a40fcd2ba09d3744aff7126041d3f2ce2ae6e2939f07b45cd7ae0a482894'
            '1295fc79a111af0834ab95ea2a3a9d2684c42a062b21d88a1a0c88da9ed5ca16'
            '119e0b5f449a66946ae257ce80d6a7b2a19d2f9bdfd53c2a52c1a47b676829c3')
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
