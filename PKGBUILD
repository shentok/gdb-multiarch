# Maintainer: Aviel Warschawski <aviel.warschawski@gmail.com>

pkgname=gdb-multiarch
pkgver=8.0.1
pkgrel=1
pkgdesc='The GNU Debugger for all gdb supported architectures targets (i386/arm/mips...)'
arch=(i686 x86_64)
url='http://www.gnu.org/software/gdb/'
license=(GPL3)
depends=(xz ncurses expat python guile2.0 gdb-common)
options=(!emptydirs)
source=(ftp://ftp.gnu.org/gnu/gdb/gdb-$pkgver.tar.xz{,.sig})
sha256sums=('3dbd5f93e36ba2815ad0efab030dcd0c7b211d7b353a40a53f4c02d7d56295e3'
            'SKIP')
validpgpkeys=('F40ADB902B24264AA42E50BF92EDB04BFF325CF3') # Joel Brobecker <brobecker@adacore.com>

prepare() {
  cd gdb-$pkgver
  sed -i "/ac_cpp=/s/\$CPPFLAGS/\$CPPFLAGS -O2/" libiberty/configure
}

build() {
  cd gdb-$pkgver

  ./configure \
    --enable-targets=all \
    --prefix=/build \
    --enable-languages=c,c++ \
    --enable-multilib \
    --enable-interwork \
    --with-system-readline \
    --disable-nls \
    --with-python=/usr/bin/python3 \
    --with-guile=guile-2.0 \
    --with-system-gdbinit=/etc/gdb/gdbinit

  make
}

package() {
  cd gdb-$pkgver

  make DESTDIR="$pkgdir" install

  # Following files conflict with 'gdb' package
  mkdir -p "$pkgdir"/usr/bin
  mv "$pkgdir"/build/bin/gdb "$pkgdir"/usr/bin/gdb-multiarch
  rm -r "$pkgdir"/build
}