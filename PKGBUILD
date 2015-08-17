_basename=verynice
pkgname="${_basename}-fork"
pkgver=20120229
pkgrel=1
pkgdesc="A tool for dynamically adjusting nice & ionice levels, and CPU affinity masks of processes"
url="https://github.com/Cloudef/${pkgname}"
arch=('i686' 'x86_64')
license=('GPL')
makedepends=('git')
depends=('bash' 'util-linux' 'schedtool')
backup=("etc/${_basename}.conf")
provides=("${_basename}")
conflicts=("${_basename}")

_gitroot="git://${url/https:\/\/}.git"
_gitname="${pkgname}"

build() {

  cd ${srcdir}
  msg "Connecting to GIT server...."
  if [ -d ${_gitname} ] ; then
    cd ${_gitname} && git pull origin
    msg "The local files are updated."
  else
    git clone ${_gitroot} ${_gitname}
  fi

  msg "GIT checkout done or server timeout"
  rm -rf "${srcdir}/${_gitname}-build"
  git clone "${srcdir}/${_gitname}" "${srcdir}/${_gitname}-build"

  msg "Starting make..."
  cd "${srcdir}/${_gitname}-build"
  make PREFIX=/usr

}

package() {

  cd ${srcdir}
  install -D -m755 "${pkgname}-build"/${_basename} ${pkgdir}/usr/sbin/${_basename}
  install -D -m644 "${pkgname}-build"/${_basename}.conf ${pkgdir}/etc/${_basename}.conf
  install -D -m755 "${pkgname}-build"/${_basename}.init.arch ${pkgdir}/etc/rc.d/${_basename}

}

# vim: set ts=2 sw=2 tw=0 :
