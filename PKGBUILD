pkgname=systemd-boot-manager
pkgver=2
pkgrel=1
pkgdesc='A simple tool to maintain systemd-boot & systemd-boot entries for CachyOS'
arch=(any)
url='https://github.com/cachyos/systemd-boot-manager'
license=(GPL2)
backup=('etc/sdboot-manage.conf')
depends=(systemd
         findutils
         grep
         gawk)
source=(git+$url.git)
sha256sums=('SKIP')
package()
{
    install -D -m755 "${srcdir}/${pkgname}/sdboot-manage" "${pkgdir}/usr/bin/sdboot-manage"
    install -D -m644 "${srcdir}/${pkgname}/sdboot-manage.conf" "${pkgdir}/etc/sdboot-manage.conf"
    install -D -m644 "${srcdir}/${pkgname}/sdboot-kernel-update.hook" "${pkgdir}/usr/share/libalpm/hooks/sdboot-kernel-update.hook"
    install -D -m644 "${srcdir}/${pkgname}/sdboot-kernel-remove.hook" "${pkgdir}/usr/share/libalpm/hooks/sdboot-kernel-remove.hook"
    install -D -m644 "${srcdir}/${pkgname}/sdboot-systemd-update.hook" "${pkgdir}/usr/share/libalpm/hooks/sdboot-systemd-update.hook"
}
