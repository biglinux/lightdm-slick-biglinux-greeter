pkgname=lightdm-slick-biglinux-greeter
_pkgname=slick-greeter
pkgver=$(date +%y.%m.%d)
_pkgver=1.6.0
pkgrel=$(date +%H%M)
pkgdesc='A slick-biglinux-looking LightDM greeter'
arch=('x86_64')
url="https://github.com/linuxmint/slick-greeter"
license=('GPL3')
depends=('cairo' 'freetype2' 'gtk3' 'libcanberra' 'libxext' 'lightdm' 'pixman'
         'python' 'xorg-server')
conflicts=('lightdm-slick-greeter')
makedepends=('intltool' 'vala' 'gnome-common')
optdepends=('numlockx: enable numerical keypad on supported keyboard')
backup=("etc/lightdm/${_pkgname}.conf")
install="${_pkgname}.install"
source=("slick-greeter-$_pkgver.tar.gz::${url}/archive/${_pkgver}.tar.gz"
        "${_pkgname}.conf"
        "${_pkgname}.jpg"
        "${_pkgname}.png")
sha256sums=('SKIP'
            'SKIP'
            'SKIP'
            'SKIP')
prepare() {
    cd "${_pkgname}-${_pkgver}"
    NOCONFIGURE=1 ./autogen.sh
}

build() {
    cd "${_pkgname}-${_pkgver}"
    ./configure \
        --prefix=/usr \
        --sysconfdir=/etc \
        --sbindir=/usr/bin \
        --libexecdir=/usr/lib/lightdm
    make
}

package() {
    cd "${_pkgname}-${_pkgver}"
    make DESTDIR="${pkgdir}" install

    # adjust launcher name
    mv "${pkgdir}/usr/share/xgreeters/${_pkgname}.desktop" \
        "${pkgdir}/usr/share/xgreeters/$pkgname.desktop"

    # Install default conf
    install -Dm644 "${srcdir}/${_pkgname}.conf" -t "${pkgdir}/etc/lightdm/"
    install -Dm644 "${srcdir}/${_pkgname}.jpg" -t "${pkgdir}/usr/share/${_pkgname}/"  
    install -Dm644 "${srcdir}/${_pkgname}.png" -t "${pkgdir}/usr/share/${_pkgname}/"
}
