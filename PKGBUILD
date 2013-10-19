# Maintainer: Emil Lundberg <lundberg.emil@gmail.com> (AUR: Lorde; GitHub: emlun)
# Contrib Repo: https://github.com/emlun/bittorrent-sync
#
# Contributor: Dalton Miller
# Contributor: Kilian Lackhove kilian@lackhove.de
# Contributor: Justin Patera serialhex@gmail.com

pkgname=bittorrent-sync
pkgver=1.1.82
pkgrel=2
pkgdesc="BitTorrent Sync - automatically sync files via secure, distributed technology"
arch=('i686' 'x86_64' 'arm' 'armv6h' 'armv7h')
url="http://labs.bittorrent.com/experiments/sync.html"
license=('custom:bittorrent')
provides=('btsync')
backup=("etc/btsync.conf")
install="${pkgname}.install"
source=("${pkgname}.install"
    "btsync.service"
    "btsync@.service"
    "terms-of-use.html::http://www.bittorrent.com/legal/terms-of-use"
    "privacy-policy.html::http://www.bittorrent.com/legal/privacy"
    )
sha256sums=('0403721e2757f44bc6ca660d95d14d4bc1c99ffad3a0fa65ac8d0ef26011c3fa'
    'c2207bd8bf6c24242d41e55b62d31cb32d764e07e71930a5a10bb4181299dfa4'
    '7420b95e0bcd8ab45be11c89a0c11e0e6c8cb4e451dd98c08eb5933fb58e7303'
    'SKIP'
    'SKIP'
    )

if [ "$CARCH" == x86_64 ]; then
    source+=("http://syncapp.bittorrent.com/$pkgver/btsync_x64-$pkgver.tar.gz")
    sha256sums+=('3cefbef2af6323dfdb7ccfaad32f7d0c8ed5cb4ebbab58936a479f0c30804bbb')
elif [ "$CARCH" == i686 ]; then
    source+=("http://syncapp.bittorrent.com/$pkgver/btsync_i386-$pkgver.tar.gz")
    sha256sums+=('1b163881631d008ea5472b1f03a49e96f2a107b9565c5d8ae48124042e3a4def')
elif [ "$CARCH" == arm ] || [ "$CARCH" == armv6h ] || [ "$CARCH" == armv7h ]; then
    source+=("http://syncapp.bittorrent.com/$pkgver/btsync_arm-$pkgver.tar.gz")
    sha256sums+=('c1502fb7d907caf105c7aa5403f4d575f86aa8ca57817ca90aa4ba1398181a3e')
fi

build() {
    cd "${srcdir}"
    ./btsync --dump-sample-config | sed 's:/home/user/\.sync:/var/lib/btsync:g' > btsync.conf
}

package() {
    cd "${srcdir}"

    install -D -m 644 LICENSE.TXT "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.TXT"
    install -D -m 644 terms-of-use.html "${pkgdir}/usr/share/licenses/${pkgname}/terms-of-use.html"
    install -D -m 644 privacy-policy.html "${pkgdir}/usr/share/licenses/${pkgname}/privacy-policy.html"

    install -D -m 644 btsync.conf "${pkgdir}/etc/btsync.conf"

    install -D -m 755 btsync "${pkgdir}/usr/bin/btsync"

    install -D -m 644 btsync.service "${pkgdir}/usr/lib/systemd/system/btsync.service"
    install -D -m 644 btsync@.service "${pkgdir}/usr/lib/systemd/system/btsync@.service"
}

# vim: ts=4:sw=4:et
