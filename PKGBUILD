# Maintainer: Philippe Hürlimann <p@hurlimann.org>
pkgname=haskell-ide-engine
pkgver=1.1
pkgrel=3
pkgdesc="The engine for haskell ide-integration. Not an IDE"
arch=('x86_64')
url="https://github.com/haskell/haskell-ide-engine"
license=('custom:BSD3')
makedepends=('stack')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/haskell/${pkgname}/archive/${pkgver}.tar.gz")
sha384sums=('066cbac86f8a2bdcb68463188effa1a5f1d6804afa251caa351673a541eced306ed028fe8a5ba8c30e953a6fbb02fa4e')

# Supported are '8.4.2' '8.4.3' '8.4.4' '8.6.4' '8.6.5' '8.8.1' '8.8.2'
# activated by default are the ones also used in a stackage snapshot. Removing
# versions you do not use will greatly reduce the compilation time of this
# package
_enabled_ghc_versions=('8.4.3' '8.4.4' '8.6.4' '8.6.5' '8.8.2')

build() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    for ver in "${_enabled_ghc_versions[@]}"; do
        stack --stack-yaml=stack-${ver}.yaml build
    done
}

package() {
    cd "${srcdir}/${pkgname}-${pkgver}"
    install -D -m 644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"

    for ver in "${_enabled_ghc_versions[@]}"; do
        stack --stack-yaml=stack-${ver}.yaml --local-bin-path "${pkgdir}/usr/bin/" install \
        && mv "${pkgdir}/usr/bin/hie" "${pkgdir}/usr/bin/hie-${ver}"
    done
}
