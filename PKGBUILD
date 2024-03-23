# SPDX-FileCopyrightText: 2019 Max Mehl
# SPDX-FileCopyrightText: 2024 Pellegrino Prevete
# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer:  Truocolo <truocolo@aol.com>
# Maintainer:  Pellegrino Prevete <cGVsbGVncmlub3ByZXZldGVAZ21haWwuY29tCg== | base -d>
# Maintainer: George Rawlinson <grawlinson@archlinux.org>
# Contributor: Max Mehl <aur at mehl dot mx>

pkgname=python-license-expression
pkgver=30.2.0
pkgrel=1
pkgdesc='Utility to parse, normalize and compare license expressions'
arch=('any')
url='https://github.com/nexB/license-expression'
license=('Apache')
depends=(
  'python'
  'python-boolean.py'
)
makedepends=(
  'git'
  'python-build'
  'python-installer'
  'python-wheel'
  'python-setuptools-scm'
  'python-wheel'
)
checkdepends=(
  'python-pytest'
  'python-pytest-xdist'
)
_commit='db2c6539755408a069f4a38d11ee3e7d7f49adde'
source=("$pkgname::git+$url#commit=$_commit")
b2sums=('SKIP')

pkgver() {
  cd "$pkgname"

  git describe --tags | sed 's/^v//'
}

prepare() {
  cd "$pkgname"

  # Fix file to comply with PEP-440
  sed \
    -i pyproject.toml \
    -e "s/^fallback_version =.*/fallback_version = \"$pkgver\"/"
}

build() {
  cd "$pkgname"

  python -m build --wheel --no-isolation
}

check() {
  cd "$pkgname"

  pytest -v
}

package() {
  cd "$pkgname"

  python -m installer --destdir="$pkgdir" dist/*.whl
}

# vim:set sw=2 sts=-1 et:
