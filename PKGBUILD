pkgname=systemd-boot-manager
pkgver=0.8
pkgrel=1
pkgdesc='A simple tool to maintain systemd-boot & systemd-boot entries for Manjaro'
arch=(any)
url='https://gitlab.com/dalto.8/systemd-boot-manager'
license=(GPL2)
backup=('etc/sdboot-manage.conf')
depends=(systemd
         findutils
         grep
         gawk)
source=(git+https://gitlab.com/dalto.8/systemd-boot-manager.git#tag=$pkgver)
sha256sums=('SKIP')
package()
{
    install -D -m755 "${srcdir}/${pkgname}/sdboot-manage" "${pkgdir}/usr/bin/sdboot-manage"
    install -D -m644 "${srcdir}/${pkgname}/sdboot-manage.conf" "${pkgdir}/etc/sdboot-manage.conf"
    install -D -m644 "${srcdir}/${pkgname}/sdboot-kernel-update.hook" "${pkgdir}/usr/share/libalpm/hooks/sdboot-kernel-update.hook"
    install -D -m644 "${srcdir}/${pkgname}/sdboot-kernel-remove.hook" "${pkgdir}/usr/share/libalpm/hooks/sdboot-kernel-remove.hook"
    install -D -m644 "${srcdir}/${pkgname}/sdboot-systemd-update.hook" "${pkgdir}/usr/share/libalpm/hooks/sdboot-systemd-update.hook"
}
