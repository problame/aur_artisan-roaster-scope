# Maintainer: Christian Schwarz <me@cschwarz.com>
pkgname=artisan-roaster-scope
pkgver=0.9.7
_commit="a6bdeffafb54b0382191dcbff4a682a845274bcb"
pkgrel=1
pkgdesc="Artisan is a software that helps coffee roasters record, analyze, and control roast profiles."
arch=("any")
url="https://github.com/artisan-roaster-scope/artisan"
license=('GPL3')
depends=( "python2"
          "python2-sip"
          "python2-numpy"
          "python2-cx_freeze"
          "python2-pyserial"
          "python2-requests"
          "python2-pyqt4"
          "python2-matplotlib"
          "python2-qrcode"
          "python2-bottle"
          "python2-gevent"
          "python2-gevent-websocket"
          "python2-phidgets"
          "python2-pymodbus"
          "python2-yoctopuce"
)
makedepends=('git')
source=("git+https://github.com/artisan-roaster-scope/artisan.git#commit=${_commit}")
md5sums=('SKIP')
#generate with 'makepkg -g'

install="$pkgname.install"

prepare() {
  
  cd "$srcdir/artisan"

  # Package thinks /usr/bin/env python returns python2 
  find .  -name "*.py" -exec sed -i \
            "s/#\!\/usr\/bin\/env python[\s\n]*/#\!\/usr\/bin\/env python2/" {} +
  find .  -name "*.py" -exec sed -i \
            "s/#\!\/usr\/bin\/python/#\!\/usr\/bin\/python2/" {} +

}

package() {
  
  cd "$srcdir/artisan"

  # Copy the relevant project files to usr/share/artisan  
  cp -r debian/usr "$pkgdir/"
  
  usrshr="$pkgdir/usr/share/artisan"

  install -m755 -d "$usrshr"

  cp -r artisanlib "$usrshr"
  cp artisan*.{icns,ico,xml,png,pro,py} "$usrshr"
  cp Comm*.py "$usrshr"
  cp -r const "$usrshr"
  cp -r icons "$usrshr"
  cp -r includes "$usrshr"
  cp KERNpython3.py "$usrshr"
  cp LICENSE.txt "$usrshr"
  cp qt.conf "$usrshr"
  cp -r translations "$usrshr"
  cp -r Wheels "$usrshr"

  # Make main script executable
  chmod +x "$usrshr/artisan.py"
  
  # Create a symlink to the main python script in usr/bin
  install -m755 -d "$pkgdir/usr/bin"
  cd "$pkgdir/usr/bin"
  ln -sf "../share/artisan/artisan.py" artisan

}

# vim:set ts=2 sw=2 et: