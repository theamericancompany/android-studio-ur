# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>
# Contributor:  danyf90 <daniele.formichelli@gmail.com>
# Contributor: Philipp 'TamCore' B. <philipp [at] tamcore [dot] eu>
# Contributor: Jakub Schmidtke <sjakub-at-gmail-dot-com>
# Contributor: Christoph Brill <egore911-at-gmail-dot-com>
# Contributor: Lubomir 'Kuci' Kucera <kuci24-at-gmail-dot-com>
# Contributor: Tad Fisher <tadfisher at gmail dot com>
# Contributor: Philippe Hürlimann <p@hurlimann.org>
# Contributor: Julian Raufelder <aur@raufelder.com>
# Contributor: Dhina17 <dhinalogu@gmail.com>
# Maintainer: Kordian Bruck <k@bruck.me>

_proj="android"
pkgname="${_proj}-studio"
pkgver=2024.2.2.13
pkgrel=1
pkgdesc="The official Android IDE (Stable branch)"
arch=(
  'i686'
  'x86_64'
  'arm'
  'aarch64'
  'armv7l'
  'mips'
  'pentium4'
)
url="https://developer.${_proj}.com"
license=(
  'APACHE'
)
makedepends=()
depends=(
  'alsa-lib'
  'freetype2'
  'libxrender'
  'libxtst'
  'which'
)
optdepends=(
  'gtk2: GTK+ look and feel'
  'libgl: emulator support'
  'ncurses5-compat-libs: native debugger support'
)
options=(
  '!strip'
)
source=(
  "https://dl.google.com/dl/android/studio/ide-zips/$pkgver/android-studio-$pkgver-linux.tar.gz"
  "$pkgname.desktop"
  "license.html"
)
sha256sums=(
  'b7fe1ed4a7959bdaca7a8fd57461dbbf9a205eb23cc218ed828ed88e8b998cb5'
  '73cd2dde1d0f99aaba5baad1e2b91c834edd5db3c817f6fb78868d102360d3c4'
  '9a7563f7fb88c9a83df6cee9731660dc73a039ab594747e9e774916275b2e23e'
)

if [ "$CARCH" = "i686" ]; then
  depends+=('java-environment')
fi

package() {
  local \
    _files=()
  _files=(
    "bin"
    "lib"
    "jbr"
    "plugins"
    "license"
    "LICENSE.txt"
    "build.txt"
    "product-info.json"
  )
  cd \
    "${srcdir}/${pkgname}"
  # Install the application
  install \
    -d \
      "${pkgdir}/"{"opt/${pkgname}","usr/bin"}
  cp \
    -a \
    "${_files[@]}" \
    "${pkgdir}/opt/${pkgname}"
  ln \
    -s \
    "/opt/${pkgname}/bin/studio" \
    "${pkgdir}/usr/bin/${pkgname}"
  # Copy licenses
  install \
    -Dm644 \
    "LICENSE.txt" \
    "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE.txt"
  install \
    -Dm644 \
    "${srcdir}/license.html" \
    "${pkgdir}/usr/share/licenses/${pkgname}/license.html"
  # Add the icon and desktop file
  install \
    -Dm644 \
    "bin/studio.png" \
    "${pkgdir}/usr/share/pixmaps/${pkgname}.png"
  install \
    -Dm644 \
    "${srcdir}/${pkgname}.desktop" \
    "${pkgdir}/usr/share/applications/${pkgname}.desktop"
  chmod \
    -R \
    "ugo+rX" \
    "${pkgdir}/opt"
}
