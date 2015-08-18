# Maintainer: Robert La Spina <rkidlaspina at gmail dot com>
# Based on the skulltag package by Mikael Eriksson <mikael_eriksson@miffe.org>
# and Sean Streeter <anubis2591 at gmail dot com>
pkgname=zandronum
pkgver=2.0
pkgrel=1
pkgdesc="OpenGL ZDoom port with Client/Server multiplayer."
arch=('i686' 'x86_64')
url="http://zandronum.com/"
license=('custom')
conflicts=('zandronum-hg')
#makedepends=('cmake' 'mercurial' 'yasm' 'mesa') # Not sure if it needs yasm.
depends=('sdl' 'gtk2' 'libjpeg6-turbo' 'glu' 'openssl')
optdepends=('timidity++: midi support'
            'freedoom: free IWAD')
install=zandronum.install

if [ "$CARCH" == "i686" ];then
    source=(
        "http://zandronum.com/downloads/${pkgname}${pkgver}-linux-x86.tar.bz2"
        "LICENSE.txt"
    )
    md5sums=(
        '5e4c65146c82111eb404ae0aef69fbcf'
        '58c2c8b15c886b838dc2ed5186361507'
    )
    _64=
fi

if [ "$CARCH" == "x86_64" ]; then
    source=(
        "http://zandronum.com/downloads/${pkgname}${pkgver}-linux-x86_64.tar.bz2"
        "LICENSE.txt"
    )
    md5sums=(
        '60b97dbc4f521d7c218c14d17cdf6841'
        '58c2c8b15c886b838dc2ed5186361507'
    )
    _64=64
fi


build() {
  cd $srcdir
 
  cat > zandronum.sh << EOF
#!/bin/sh
export LD_LIBRARY_PATH=/usr/share/zandronum/lib
exec /usr/share/zandronum/zandronum "\$@"
EOF

  cat > zandronum-server.sh << EOF
#!/bin/sh
export LD_LIBRARY_PATH=/usr/share/zandronum/lib
exec /usr/share/zandronum/zandronum-server "\$@"
EOF

}

package(){ 
  cd $srcdir
  
  install -Dm644 "zandronum.pk3" "$pkgdir/usr/share/zandronum/zandronum.pk3"
  #install -Dm644 "brightmaps.pk3" "$pkgdir/usr/share/zandronum/brightmaps.pk3"
  install -Dm644 "skulltag_actors.pk3" "$pkgdir/usr/share/zandronum/skulltag_actors.pk3"
  install -Dm755 "liboutput_sdl.so" "$pkgdir/usr/share/zandronum/lib/liboutput_sdl.so"
  install -Dm755 "zandronum" "$pkgdir/usr/share/zandronum/zandronum"
  install -Dm755 "zandronum-server" "$pkgdir/usr/share/zandronum/zandronum-server"
  install -Dm755 "zandronum.sh" "$pkgdir/usr/bin/zandronum"
  install -Dm755 "zandronum-server.sh" "$pkgdir/usr/bin/zandronum-server"
  install -Dm755 "libfmodex${_64}-4.24.16.so" "$pkgdir/usr/share/zandronum/lib/libfmodex${_64}-4.24.16.so"

#  ln -s "/usr/lib/libcrypto.so" "$pkgdir/usr/share/zandronum/lib/libcrypto.so.0.9.8"
#  ln -s "/usr/lib/libssl.so" "$pkgdir/usr/share/zandronum/lib/libssl.so.0.9.8"

  install -Dm644 "LICENSE.txt" "$pkgdir/usr/share/licenses/${pkgname}/LICENSE"
}

# vim:set ts=2 sw=2 et:
