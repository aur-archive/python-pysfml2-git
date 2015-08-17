# Maintainer: Thomas Glamsch <thomas.glamsch@gmail.com>
# Contributor: Philippe Huerlimann <phihue@gmail.com>
pkgname=python-pysfml2-git
pkgver=20130303
pkgrel=1
pkgdesc="A Python 3 binding for SFML 2, written with Cython."
arch=('i686' 'x86_64')
url="http://pysfml2-cython.readthedocs.org/"
license=('BSD')
depends=('sfml-git' 'python')
makedepends=('cython' 'git')
source=()
md5sums=()

_gitroot='git://github.com/bastienleonard/pysfml-cython.git'
_gitname='pysfml2-cython'

build() {
	cd "$srcdir"
	msg "Connecting to GIT server...."

	if [ -d $_gitname ] ; then
		cd $_gitname && git pull origin
		msg "The local files are updated."
	else
		git clone $_gitroot $_gitname
	fi

	msg "GIT checkout done or server timeout"
	msg "Starting make..."

	rm -rf "$srcdir/$_gitname-build"
	git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
	cd "$srcdir/$_gitname-build"

        # See issue #17 (https://github.com/bastienleonard/pysfml2-cython/issues/17)
	python setup3k.py build || ./patch.py && python setup3k.py build
}

package() {
	cd "$srcdir/$_gitname-build"
	python setup3k.py install --root="${pkgdir}" --prefix=/usr

	# Copying the License file
	install -D -m644 "$srcdir/$_gitname-build/LICENSE.txt" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
