# Maintainer: Daniel Dias <dias AT archlinux DOT info>
pkgname=papi-git
_pkgname=papi
pkgver=r6164.5d9ed8d
pkgrel=1
pkgdesc='Performance Application Programming Interface'
arch=('any')
url="http://icl.cs.utk.edu/papi/"
license=('BSD')
depends=('glibc' 'linux-api-headers' 'gcc-fortran')
makedepends=('git')
provides=('papi')
conflicts=('papi')

source=('papi::git+https://icl.cs.utk.edu/git/papi.git')

md5sums=('SKIP')

pkgver() {
  cd "$_pkgname"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
	cd "$srcdir/$_pkgname/src"
	
	unset MAKEFLAGS

	sed -i '/$(LDCONFIG)/d' "$srcdir/$_pkgname/src/libpfm4/lib/Makefile"
	./configure --prefix=/usr --mandir=/usr/share/man --with-perf-events
	make
}

check() {
	cd "$srcdir/$_pkgname/src"
	make test
}

package() {
	cd "$srcdir/$_pkgname/src"
	make DESTDIR="$pkgdir" install
	chmod 644 $pkgdir/usr/share/papi/papi_events.csv
  	install -D -m644 $srcdir/$_pkgname/LICENSE.txt $pkgdir/usr/share/licenses/$pkgname/LICENSE
}
