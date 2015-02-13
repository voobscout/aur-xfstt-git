# Maintainer: Voobscout <voobscout+aur@gmail.com>
pkgname=xorg-xfstt-git
pkgver=1.9.1
pkgrel=1
pkgdesc="X Font Server TrueType"
arch=('i686' 'x86_64')
license=('GPL2')
makedepends=('git' 'pkg-config' 'autoconf' 'automake' 'gettext')
url="http://www.hadrons.org/software/xfstt"
provides=('xorg-xfstt')
optdepends=('xorg-server')
source=('git://git.hadrons.org/git/xfstt.git')
sha256sums=('SKIP')

pkgver() {
	cd ${srcdir}/${pkgname%%-*}
	git describe --always | sed 's/-/./g'
}

install=xfstt.install
options=(!strip)

_gitroot="git://git.hadrons.org/git/xfstt.git"
_gitname="xfstt"

build() {

  msg "Connecting to ${_gitroot}..."

  if [ -d ${srcdir}/${_gitname} ] ; then
      cd ${srcdir}/${_gitname} && git pull origin master
  else
    git clone $_gitroot
  fi

  msg "GIT checkout done or server timeout"

  cd ${srcdir}/${_gitname}

  msg "Preparing XFSTT sources..."
  autoreconf -Wall -f -i

  msg "Configuring XFSTT..."
  ./configure --prefix=/usr

  msg "Compiling XFSTT... "
  make

}

package() {
  msg "Installing XFSTT"
  cd ${srcdir}/${_gitname}
  make DESTDIR=${pkgdir} install
}
# vim:set ts=2 sw=2 et:
