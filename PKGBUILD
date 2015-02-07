# Maintainer: Voobscout <voobscout+aur@gmail.com>
# Original maintainer: M Rawash <mrawash@gmail.com>
# Contributor: olvar <beren dot olvar (at) gmail dot com>
# Contributor: Andrew Antle <andrew dot antle at gmail dot com>
# Contributor: joyfulgirl <joyfulgirl (at) archlinux.us>
# Contributor: Jonathan Friedman <jonf@gojon.com>

pkgname=xfstt-git
pkgver=1.9.1
pkgrel=1
pkgdesc="X Font Server TrueType"
arch=('i686' 'x86_64')
license=('GPL2')
depends=()
makedepends=('git' 'pkg-config' 'autoconf' 'automake' 'gettext' 'texinfo')
url=""
provides=('stumpwm')
optdepends=('emacs: Edit and eval stumpwm code with M-x stumpwm-mode'
            'stumpwm-contrib: A collection of StumpWM modules'
           )

source=('git://git.hadrons.org/git/xfstt.git'
        # 'xfstt.install'
       )

sha256sums=('SKIP'
            # 'b51d5ecf4c22fe739089461381396fea227ef4b12c5214d14b87375ec047b2dc'
           )

pkgver() {
	cd ${srcdir}/${pkgname%%-*}
	git describe --always | sed 's/-/./g'
}

install=xfstt.install
options=(!strip)  # Thanks to sidereus for pointing this out

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

  # msg "Installing StumpWM xsession"
  # install -Dm 0644 ${srcdir}/stumpwm.desktop ${pkgdir}/usr/share/xsessions/stumpwm.desktop

  # msg "Installing stumpwmrc.sample"
  # install -Dm 0644 sample-stumpwmrc.lisp ${pkgdir}/etc/stumpwmrc.sample

  # msg "Installing stumpish"
  # cd ${srcdir}
  # wget -c https://raw.githubusercontent.com/stumpwm/stumpwm-contrib/master/util/stumpish/stumpish
  # install -Dm 0755 ${srcdir}/stumpish ${pkgdir}/usr/bin/stumpish
 }
