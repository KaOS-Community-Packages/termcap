pkgname=termcap
pkgver=1.3.1
pkgrel=1
pkgdesc="Enables programs to use display computer terminals in a device-independent manner"
arch=('x86_64')
url="http://www.catb.org/~esr/terminfo/"
license=('GPL')
depends=('glibc')
source=("http://ftp.gnu.org/gnu/${pkgname}/${pkgname}-${pkgver}.tar.gz")
md5sums=('ffe6f86e63a3a29fa53ac645faaabdfa')

build() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    gcc -fPIC -c "${srcdir}/${pkgname}-${pkgver}/${pkgname}.c" \
        -o "${srcdir}"/"${pkgname}.o" \
        -DHAVE_STRING_H=1 -DHAVE_UNISTD_H=1 -DSTDC_HEADERS=1 || return 1
    gcc -shared -Wl,-soname,"lib${pkgname}.so" \
        -o "${srcdir}/lib${pkgname}.so.${pkgver}" "${srcdir}/${pkgname}.o" || return 1
}

package() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    mkdir -p "${pkgdir}/usr/lib"
    install -Dm755 "${srcdir}/lib${pkgname}.so.${pkgver}" "${pkgdir}/usr/lib/lib${pkgname}.so.${pkgver}"
    ln -s "/usr/lib/lib${pkgname}.so.${pkgver}" "${pkgdir}/usr/lib/lib${pkgname}.so"
    for infofile in ${pkgname}.info*
        do install -Dm644 "${srcdir}/${pkgname}-${pkgver}/${infofile}" "${pkgdir}/usr/share/info/${infofile}"
    done
}
