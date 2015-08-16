# Maintainer: Charles Bos <charlesbos1 AT gmail>
# Contributor: Xiao-Long Chen <chenxiaolong@cxl.epac.to>

pkgname=indicator-printers
_ubuntu_rel=0ubuntu1
_actual_ver=0.1.7
_extra_ver=+14.04.20140213
_source_date=20140213
_translations=20130418
pkgver=${_actual_ver}.${_source_date}
pkgrel=2
pkgdesc="Indicator showing active print jobs"
arch=('i686' 'x86_64')
url="https://launchpad.net/indicator-printers"
license=('GPL')
groups=('unity')
depends=('cups' 'libdbusmenu-glib' 'libdbusmenu-gtk3' 'libindicator-bzr')
makedepends=('intltool' 'python2')
options=('!libtool')
source=("https://launchpad.net/ubuntu/+archive/primary/+files/indicator-printers_${_actual_ver}${_extra_ver}.orig.tar.gz"
        "https://launchpad.net/ubuntu/+archive/primary/+files/indicator-printers_${_actual_ver}${_extra_ver}-${_ubuntu_rel}.diff.gz"
        "https://dl.dropboxusercontent.com/u/486665/Translations/translations-${_translations}-indicator-printers.tar.gz")
sha512sums=('84d2642a1ffa27ce84dfb41dd92835a0c300fc648242721c3c8d9f39734863fc9cd174545af5443df7122bc410944b8aad15a51358c0205e3b73ac12f68bcdf6'
            '7fc4679ec3de22e694d60b700bfc0ac0390dec3b60a6688f984ca7494aa2a8384c27acbcd8bf5c92540096428287c120e0c1ece9af5dc7fe474b2f50ca7696cb'
            'edbf2e0db90b81b805f966ddc3e1d1fab76f50651eb5135f3c559daca30b6134e72b2fbd01ccdd357a3252d096345a42e17c62a986fe3c3477034d1cf7624759')

prepare() {
  cd "${srcdir}/${pkgname}-${_actual_ver}${_extra_ver}"

  # Apply Ubuntu's patches
  patch -p1 -i "${srcdir}/indicator-printers_${_actual_ver}${_extra_ver}-${_ubuntu_rel}.diff"

  msg "Merging translations from ${_translations}"
  rm -f po/LINGUAS po/*.pot
  mv "${srcdir}"/po/*.pot po/
  for i in "${srcdir}"/po/*.po; do
    FILE=$(sed -n "s|.*/${pkgname}-||p" <<< ${i})
    mv ${i} po/${FILE}
    echo ${FILE%.*} >> po/LINGUAS
  done
}

build() {
  cd "${srcdir}/${pkgname}-${_actual_ver}${_extra_ver}"

  autoreconf -vfi
  intltoolize -f
  ./configure --prefix=/usr --libexecdir=/usr/lib/${pkgname} --disable-static
  make
}

package() {
  cd "${srcdir}/${pkgname}-${_actual_ver}${_extra_ver}"

  make DESTDIR="${pkgdir}/" install
}

# vim:set ts=2 sw=2 et:
