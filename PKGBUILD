pkgname=bindery
pkgver=20120913
pkgrel=2
pkgdesc="Interactive digital document binding tool for post-processed scanned images"

arch=('any')
url="http://blender3d.github.com/Bindery/"
license=('GPL')

depends=('python' 'pyqt' 'djvulibre' 'minidjvu' 'jbig2enc-git' 'djvubind')
makedepends=('git')
optdepends=('tesseract: OCR engine'
            'cuneiform: OCR engine')

install='bindery.install'

_gitroot="git://github.com/Blender3D/Bindery.git"
_gitname="bindery"

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone --depth=1 $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
}

package() {
  mkdir -p $pkgdir/usr/{share,bin}
  mkdir -p $pkgdir/usr/share/{icons,applications}

  mv $pkgname $pkgdir/usr/share/
  cp $pkgdir/usr/share/bindery/ui/icons/logo.png $pkgdir/usr/share/icons/bindery.png
  cp $pkgdir/usr/share/bindery/distro/linux/arch/bindery.desktop $pkgdir/usr/share/applications/

  rm -R $pkgdir/usr/share/$pkgname/distro

  echo "#/bin/bash" > $pkgdir/usr/bin/bindery
  echo "cd /usr/share/bindery/" >> $pkgdir/usr/bin/bindery
  echo "python main.py" >> $pkgdir/usr/bin/bindery

  chmod +x $pkgdir/usr/bin/bindery
}
