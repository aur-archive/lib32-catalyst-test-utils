# Maintainer: Jameson Pugh <imntreal@gmail.com>
# Contributor: Vi0L0 <vi0l093@gmail.com>
# Partly based on original PKGBUILD by Mikko Seppala <t-r-a-y@mbnet.fi>
# Contributor: Manuel Gaul <inkaine@hotmail.com>
# Contributor: Enverex & kidoz
# Contributor: Alexander von Gluck IV

_pkgsourcename=catalyst-test-utils
pkgname=lib32-$_pkgsourcename
pkgver=13.7
pkgrel=1
pkgdesc="AMD/ATI catalyst driver utilities and libraries. (32-bit)"
url="http://www.amd.com"
arch=(x86_64)
license=('custom')
groups=('lib32')
depends=('lib32-libxext' 'lib32-libdrm' 'catalyst-utils')
conflicts=('lib32-libgl' 'lib32-nvidia-utils' 'lib32-ati-dri' 'lib32-catalyst-utils-pxp')
provides=('lib32-libgl' 'lib32-dri' 'lib32-libtxc_dxtn')
source=(http://www2.ati.com/drivers/beta/amd-catalyst-13.15.100.1-linux-x86.x86_64.zip
    lib32-catalyst.sh)
install=${pkgname}.install
sha256sums=('589e3b9ef4b148bc3170d97db5cd339c820a3b2615c8340565947c6dbf8780fe'
            '1f4f611ed80e2626ef39486020a06c328c15dad76e1365a4bd553342060ff409')

build() {
     /bin/sh ./amd-*.run --extract archive_files
}

package() {
      cd ${srcdir}
      install -D -m755 lib32-catalyst.sh ${pkgdir}/etc/profile.d/lib32-catalyst.sh
      cd ${srcdir}/archive_files/arch/x86/usr
      install -dm755 ${pkgdir}/usr/lib32
      install -dm755 ${pkgdir}/usr/lib32/fglrx
      install -dm755 ${pkgdir}/usr/lib32/xorg/modules/dri
      install -m755 lib/*.so* ${pkgdir}/usr/lib32
      install -m755 X11R6/lib/fglrx/fglrx-libGL.so.1.2 ${pkgdir}/usr/lib32/fglrx
      ln -sf /usr/lib32/fglrx/fglrx-libGL.so.1.2 ${pkgdir}/usr/lib32/fglrx/libGL.so.1.2
      ln -sf /usr/lib32/fglrx/fglrx-libGL.so.1.2 ${pkgdir}/usr/lib32/fglrx-libGL.so.1.2
      ln -sf /usr/lib32/fglrx/fglrx-libGL.so.1.2 ${pkgdir}/usr/lib32/libGL.so.1.2
      ln -sf /usr/lib32/fglrx/fglrx-libGL.so.1.2 ${pkgdir}/usr/lib32/libGL.so.1
      ln -sf /usr/lib32/fglrx/fglrx-libGL.so.1.2 ${pkgdir}/usr/lib32/libGL.so
      install -m755 X11R6/lib/libAMDXvBA.so.1.0 ${pkgdir}/usr/lib32
      install -m755 X11R6/lib/libatiadlxx.so ${pkgdir}/usr/lib32
      install -m755 X11R6/lib/libfglrx_dm.so.1.0 ${pkgdir}/usr/lib32
      install -m755 X11R6/lib/libXvBAW.so.1.0 ${pkgdir}/usr/lib32
      install -m755 X11R6/lib/modules/dri/*.so ${pkgdir}/usr/lib32/xorg/modules/dri
      ln -snf /usr/lib32/xorg/modules/dri ${pkgdir}/usr/lib32/dri

      cd $pkgdir/usr/lib32
      ln -sf libfglrx_dm.so.1.0 libfglrx_dm.so.1
      ln -sf libAMDXvBA.so.1.0 libAMDXvBA.so.1
      ln -sf libXvBAW.so.1.0 libXvBAW.so.1
      ln -sf libatiuki.so.1.0 libatiuki.so.1
      ln -sf libatiuki.so.1.0 libatiuki.so
      ln -sf libOpenCL.so.1 libOpenCL.so

      # OpenCL
      install -m755 -d ${pkgdir}/etc/OpenCL/vendors
      install -m644 ${srcdir}/archive_files/arch/x86/etc/OpenCL/vendors/amdocl32.icd ${pkgdir}/etc/OpenCL/vendors

      # License
      install -m755 -d ${pkgdir}/usr/share/licenses/${pkgname}
      install -m644 ${srcdir}/archive_files/LICENSE.TXT ${pkgdir}/usr/share/licenses/${pkgname}
}
