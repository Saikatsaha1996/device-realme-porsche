# Reference: <https://postmarketos.org/devicepkg>
pkgname=device-realme-porsche
pkgdesc="Realme GT 2 (Porsche)"
pkgver=0.1
pkgrel=1
url="https://postmarketos.org"
license="MIT"
arch="aarch64"
options="!check !archcheck"
depends="
	linux-postmarketos-qcom-sm8350
	mkbootimg
	postmarketos-base
	soc-qcom-sm8350
"
makedepends="
	devicepkg-dev
	dtc
	android-tools
"
source="
	deviceinfo
	empty-realme-porsche.dts
"
subpackages="$pkgname-nonfree-firmware:nonfree_firmware"

build() {
	devicepkg_build $startdir $pkgname

	dtc -O dtb -o "$srcdir/empty-realme-porsche.dtbo" -b 0 -@ \
		"$srcdir/empty-realme-porsche.dts"

	mkdtboimg create "$srcdir/dtbo.img" --page_size=4096 \
		"$srcdir/empty-realme-porsche.dtbo"
}

package() {
	devicepkg_package $startdir $pkgname
	install -Dm644 "$srcdir/dtbo.img" "$pkgdir/boot/dtbo.img"
}

nonfree_firmware() {
	pkgdesc="Modem, WiFi, and GPU Firmware"
	depends="firmware-realme-porsche"
	mkdir "$subpkgdir"
}

sha512sums=""
