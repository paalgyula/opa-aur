# Maintainer: Brian Atkinson <brian@atkinson.mn>
# Prior Maintainer: David Birks <david@birks.dev>

pkgname=opa
pkgver=0.46.1
pkgrel=1
pkgdesc='Command-line utility and REPL for Open Policy Agent'
arch=(x86_64)
url='https://github.com/open-policy-agent/opa'
license=(Apache)
makedepends=('go')
source=("$pkgname-$pkgver.tar.gz::https://github.com/open-policy-agent/opa/archive/v$pkgver.tar.gz")
sha256sums=('5e2cfdff17877d42d4c68a6aae925a131f12b4d45d74a17c4a81a0d9383ee997')

build() {
  cd "$pkgname-$pkgver"

  export CGO_CPPFLAGS="${CPPFLAGS}"
  export CGO_CFLAGS="${CFLAGS}"
  export CGO_CXXFLAGS="${CXXFLAGS}"
  export CGO_LDFLAGS="${LDFLAGS}"
  export GOFLAGS="-buildmode=pie -trimpath -ldflags=-linkmode=external -modcacherw"

  go build \
  -ldflags "-X github.com/open-policy-agent/opa/version.Version=$pkgver" \
  -o "$pkgname" \
  .

  mkdir completion
  "./$pkgname" completion bash > "completion/$pkgname"
  "./$pkgname" completion zsh > "completion/_$pkgname"
}

package() {
  install -Dm 755 "$srcdir/$pkgname-$pkgver/$pkgname" "$pkgdir/usr/bin/$pkgname"
  install -vDm 644 "$srcdir/$pkgname-$pkgver/completion/$pkgname" -t "$pkgdir/usr/share/bash-completion/completions/"
  install -vDm 644 "$srcdir/$pkgname-$pkgver/completion/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions/"
}
