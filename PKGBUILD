# $Id: PKGBUILD 140263 2011-10-11 07:46:57Z eric $
# Maintainer: greg+devel@marvid.fr
# Contributor: Jochem Kossen <j.kossen@home.nl>

pkgname=rowks
pkgver=2.11
pkgrel=3
pkgdesc="A version of rox file manager with a coherent naming scheme for background modes"
arch=('i686' 'x86_64')
license=('GPL')
url="http://roscidus.com/desktop/"
depends=('sh' 'libsm' 'gtk2')
makedepends=('librsvg' 'python2')
replaces=('rox')
conflicts=('rox')
source=("http://downloads.sourceforge.net/rox/rox-filer-${pkgver}.tar.bz2"
        'rox.desktop' 'rox.svg' 'rox.sh'
        '0001_coherent_naming_scheme_for_backdrops.patch'
        '0002_libs_required_to_compile.patch')
md5sums=('0eebf05a67f7932367750ebf9faf215d'
         'de05c906395abd4402b0470c1bc2ae6e'
         '658c8648b51e215558e13e6afb2b5c76'
         '31578a90b241f0a8d09c9f8587608d00'
         'd87712985d962aee9fe819101d6afe35'
         'd81cfce9407163a5a034143e63c5f41b')

build() {
  cd "${srcdir}/rox-filer-${pkgver}"
  
  patch -d ./ROX-Filer/src < "${srcdir}/0001_coherent_naming_scheme_for_backdrops.patch"
  patch -d ./ROX-Filer/src < "${srcdir}/0002_libs_required_to_compile.patch"
  ./ROX-Filer/AppRun --compile
# finally we render a png as fallback for svg unaware menu applications
# Attention: always make sure you check the dimensions of the source-svg,
# you can read the dimensions via inkscape's export function
  rsvg-convert -w 48 -h 38 -f png -o "${srcdir}/rox.png" "${srcdir}/rox.svg"
}

package() {
  cd "${srcdir}/rox-filer-${pkgver}"
  install -d "${pkgdir}/usr/share/Choices/MIME-types"
  install -m755 Choices/MIME-types/* "${pkgdir}/usr/share/Choices/MIME-types/"
  cp -rp ROX-Filer "${pkgdir}/usr/share/"
  rm -fr "${pkgdir}"/usr/share/ROX-Filer/{src,build}
 
  install -D -m755 "${srcdir}/rox.sh" "${pkgdir}/usr/bin/rox"
  install -D -m644 rox.1 "${pkgdir}/usr/share/man/man1/rox.1"
  ln -sf rox.1 "${pkgdir}/usr/share/man/man1/ROX-Filer.1"

  install -D -m644 "${srcdir}/rox.desktop" "${pkgdir}/usr/share/applications/rox.desktop"
  install -D -m644 "${srcdir}/rox.svg" "${pkgdir}/usr/share/pixmaps/rox.svg"
  install -D -m644 "${srcdir}/rox.png" "${pkgdir}/usr/share/pixmaps/rox.png"
}


