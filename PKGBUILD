#$Id: PKGBUILD 96979 2010-10-25 20:35:44Z tpowa $
#Maintainer: Tobias Powalowski <tpowa@archlinux.org>

pkgname=ndiswrapper-ck
_kernver=2.6.36-ck
pkgver=1.56
pkgrel=2
pkgdesc="Module for NDIS (Windows Network Drivers) drivers supplied by vendors. For stock arch 2.6 kernel."
license=('GPL')
arch=(i686 x86_64)
url="http://ndiswrapper.sourceforge.net"
install="ndiswrapper.install"
depends=("ndiswrapper-utils=$pkgver" 'kernel26-ck>=2.6.36' 'kernel26-ck<2.6.37')
makedepends=('kernel26-ck-headers>=2.6.36' 'kernel26-ck-headers<2.6.37')
source=(http://downloads.sourceforge.net/sourceforge/ndiswrapper/ndiswrapper-$pkgver.tar.gz
        kernel-2.6.35.patch
        kernel-2.6.36.patch)
build()
{
  cd $srcdir/ndiswrapper-$pkgver/driver
  patch -Np2 -i $startdir/kernel-2.6.35.patch
  patch -Np2 -i $startdir/kernel-2.6.36.patch
  make KVERS=$_kernver
  make DESTDIR=$pkgdir KVERS=$_kernver install
  rm $pkgdir/lib/modules/$_kernver/modules.* #wtf?

  sed -i -e "s/KERNEL_VERSION='.*'/KERNEL_VERSION='${_kernver}'/" $startdir/*.install
  # move it to correct kernel directory
  mkdir -p $pkgdir/lib/modules/$_kernver/kernel/drivers/net/wireless/ndiswrapper
  mv $pkgdir/lib/modules/$_kernver/misc/* $pkgdir/lib/modules/$_kernver/kernel/drivers/net/wireless/ndiswrapper/
  rm -r $pkgdir/lib/modules/$_kernver/misc/
}

md5sums=('1431f7ed5f8e92e752d330bbb3aed333'
         '0a03d613b1fd545a75c5dd1a7c2aaec4'
         'cc16ed13449f17e90865df688b180b2c')
