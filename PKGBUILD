#!/bin/bash

# Based on original packaging by Felix Barz <skycoder42.de@gmx.de>

# Disable various shellcheck rules that produce false positives in this file.
# Repository rules should be added to the .shellcheckrc file located in the
# repository root directory, see https://github.com/koalaman/shellcheck/wiki
# and https://archiv8.github.io for further information.
# shellcheck disable=SC2034,SC2154
# ToDo: Add files: User documentation
# ToDo: Add files: Tooling
# FixMe: Namcap warnings and errors

# Maintainer: Ross Clark <https://github.com/Archiv8/repkg/discussions>
# Contributor: Ross Clark <https://github.com/Archiv8/repkg/discussions>

pkgname=repkg
pkgver=1.4.0
pkgrel=2
pkgdesc="A tool to manage rebuilding of AUR packages based on their dependencies"
arch=(
  "i686"
  "x86_64"
)
url="https://github.com/Skycoder42/repkg"
license=(
  "BSD"
)
depends=(
  "qt5-base"
  "pacman"
)
makedepends=(
  "qt5-tools"
  "git"
  "qdep"
)
optdepends=(
  "yay: The recommended frontend for the AUR to use with repkg"
)
source=(
  "${pkgname}-${pkgver}.tar.gz"::"https://github.com/Skycoder42/${pkgname}/archive/refs/tags/${pkgver}.tar.gz"
  "${pkgname}.rule"
)
sha512sums=(
  "ddaf0c7e751f9dbe8a90c2f8f5138fcdb19d33892d3dd191d301fef62e565f6ebf3370a36d9fd1c2d691ee3f57e9f9b7bb7369dfdd1e90f304deb6229f82b513"
  "6ed319288c075b805292f8d41361e36481fee2de33adcec4ee5e906bf5e7e21a81a747566442db7e6e5e9402f58aa6a20521c348effe08bf0c787eb071725e9c"
)

prepare() {

  mkdir -p build
}

build() {

  cd build

  qmake "../${pkgname}-${pkgver}/"
  make
}

package() {

  cd build

  make INSTALL_ROOT="${pkgdir}" install

  cd "../${pkgname}-${pkgver}"

  install -D -m644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
  install -D -m644 "../${pkgname}.rule" "${pkgdir}/etc/repkg/rules/system/${pkgname}.rule"
}
