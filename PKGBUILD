pkgname=eos-movrec
pkgver=svn
pkgrel=133
pkgdesc="Write short movies with your Canon EOS directly to computer using the live view mode."
url="http://sourceforge.net/projects/eos-movrec/"
arch=('i686' 'x86_64')
license=('GPLv3')
depends=('libgphoto2' 'qt4')
#optdepends=('')
makedepends=('cmake' 'gcc')
#source=()
#sha1sums=()

_svn_URL="https://eos-movrec.svn.sourceforge.net/svnroot/eos-movrec/trunk"

build() {
	cd "${srcdir}"
	if [ -d "${pkgname}/.svn" ]; then
		msg "Starting SVN update..."
		(cd "${pkgname}" && svn up)
	else
		msg "Starting SVN checkout..."
		svn co "${_svn_URL}" --config-dir ./ "${pkgname}"
	fi
	msg "SVN checkout done or server timeout"
	cd "${pkgname}"
	if [ ! -d build ]; then
		mkdir build
	fi
	cd build
	cmake -DCMAKE_INSTALL_PREFIX:PATH=/usr -DCMAKE_BUILD_TYPE=Release ..
	make

}

package() {
	cd "${srcdir}/${pkgname}/build"
	make DESTDIR="${pkgdir}" install
}

