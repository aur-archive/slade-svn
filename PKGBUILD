# Contributor: Jan Cholasta <grubber at grubber cz>
# Maintainer: Jan Cholasta <grubber at grubber cz>

pkgname=slade-svn
pkgver=1421
pkgrel=1
pkgdesc="SLADE3 Doom editor."
arch=('i686' 'x86_64')
url="http://slade.mancubus.net/"
license=('GPL')
depends=('fluidsynth' 'freeimage' 'ftgl' 'libmodplug' 'sfml' 'wxgtk2.9')
makedepends=('cmake' 'imagemagick' 'subversion' 'zip')
conflicts=('slade')
provides=('slade')
source=(slade::svn+http://mancubus.net/svn/hosted/slade/trunk/ \
        slade.desktop)
md5sums=('SKIP'
         '49eb1692463e2aa93ea2754a5df7a6e4')

pkgver() {
  svn info slade --xml | sed -rn '/<entry/{:0;s/^.*revision="//;t1;N;b0;:1;s/".*$//;p}'
}

build() {
  cd slade

  cmake -DwxWidgets_CONFIG_EXECUTABLE=/usr/bin/wx-config-2.9 \
        -DwxWidgets_wxrc_EXECUTABLE=/usr/bin/wxrc-2.9 \
        -DCMAKE_CXX_FLAGS=-DNDEBUG \
        .
  make

  pushd dist/res
  zip -r ../slade.pk3 *
  popd

  convert "slade.ico[0]" slade.png
}

package() {
  cd slade

  install -Dm755 slade "$pkgdir/usr/bin/slade"
  install -Dm644 dist/slade.pk3 "$pkgdir/usr/share/slade3/slade.pk3"

  install -Dm644 slade.png "$pkgdir/usr/share/pixmaps/slade.png"
  install -Dm644 "$srcdir/slade.desktop" "$pkgdir/usr/share/applications/slade.desktop"
}
