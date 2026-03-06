# Maintainer: Supernovatux <thulashitharan.d at gmail dot com>
_electron=electron
_pkgname='mendeley-reference-manager'
pkgname=${_pkgname}-electron
pkgver=2.143.0
pkgrel=1
pkgdesc="Mendeley Reference Manager using system provided ${_electron} for increased security and performance"
arch=('x86_64')
provides=("${_pkgname}")
conflicts=("${_pkgname}")
depends=("${_electron}" 'harfbuzz' 'libgl' 'libxss')
url='https://www.mendeley.com/download-reference-manager'
license=('custom')

_file=${_pkgname}-${pkgver}-${CARCH}.AppImage
source=("https://static.mendeley.com/bin/desktop/${_file}")
sha256sums=('c563d8638a9f46362eb130b4f720db8bf310f7d46334788f7fdb8b72a59eb81f')

options=('!strip')

prepare() {
  # Some parts taken from the orginal mendeley-reference-manager package
  # Extract AppImage contents so we install bypassing every and all AppImage
  # desktop integration/deployment mechanisms
  chmod +x "${_file}"
  "./${_file}" --appimage-extract &>/dev/null
}

package() {
  install -d "$pkgdir"/usr/bin/
  install -d "$pkgdir"/usr/lib/${_pkgname}/
  install -d "$pkgdir"/usr/share/applications/
  install -d "$pkgdir"/usr/share/icons/
  echo '#!/bin/sh' >> "$pkgdir"/usr/bin/${_pkgname}
  echo "exec ${_electron} /usr/lib/${_pkgname}/app.asar \"\$@\"" >> "$pkgdir"/usr/bin/${_pkgname}
  chmod +x "${pkgdir}/usr/bin/${_pkgname}"
  
  install -m644 squashfs-root/mendeley-reference-manager.png "$pkgdir"/usr/share/icons/

  sed -i "s%Exec=AppRun%Exec=/usr/bin/${_pkgname}%g" squashfs-root/mendeley-reference-manager.desktop
  install -m644 squashfs-root/mendeley-reference-manager.desktop "$pkgdir"/usr/share/applications/
  install -m644 squashfs-root/resources/app.asar "$pkgdir"/usr/lib/${_pkgname}/
}

