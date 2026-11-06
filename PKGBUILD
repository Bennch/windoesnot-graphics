# WinDoesNot Graphics: LACT (GPU control) with the WinDoesNot look and language.
pkgname=windoesnot-graphics
pkgver=0.10.1
pkgrel=1
pkgdesc='WinDoesNot Graphics, adapted from LACT (AMD, NVIDIA and Intel GPU control)'
arch=(x86_64)
url='https://github.com/Bennch/windoesnot-graphics'
license=('MIT')
depends=(gtk4 libadwaita hwdata libdisplay-info vulkan-tools ocl-icd)
makedepends=(rust pkgconf clang)
# Same daemon and files as the upstream package, so the two cannot be installed together.
provides=(lact)
conflicts=(lact)
options=('!lto' '!debug')
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/$pkgver.tar.gz")
sha256sums=('SKIP')
prepare() {
 cd "$srcdir/$pkgname-$pkgver"
 cargo fetch --locked
}
build() {
 cd "$srcdir/$pkgname-$pkgver"
 cargo build --release --locked -p lact
}
check() {
 cd "$srcdir/$pkgname-$pkgver"
 cargo test --release --locked -p lact-gui desktop::tests
}
package() {
 cd "$srcdir/$pkgname-$pkgver"
 install -Dm755 target/release/lact "$pkgdir/usr/bin/lact"
 install -Dm644 res/lactd.service "$pkgdir/usr/lib/systemd/system/lactd.service"
 install -Dm644 res/io.github.ilya_zlobintsev.LACT.policy "$pkgdir/usr/share/polkit-1/actions/io.github.ilya_zlobintsev.LACT.policy"
 install -Dm644 packaging/me.windoesnot.Graphics.desktop "$pkgdir/usr/share/applications/me.windoesnot.Graphics.desktop"
 install -Dm644 packaging/me.windoesnot.Graphics.svg "$pkgdir/usr/share/icons/hicolor/scalable/apps/me.windoesnot.Graphics.svg"
 install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
