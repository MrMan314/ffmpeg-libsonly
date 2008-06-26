# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Maintainer: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=20080625
pkgrel=1
pkgdesc="Complete and free Internet live audio and video broadcasting solution for Linux/Unix"
arch=(i686 x86_64)
url="http://ffmpeg.mplayerhq.hu/"
license=('LGPL')
depends=('lame' 'sdl' 'libvorbis' 'a52dec' 'faad2' 'faac' 'xvidcore' 'zlib' 'imlib2' 'x264>=20080625' 'libtheora')
source=(http://ffmpeg.mplayerhq.hu/ffmpeg-export-snapshot.tar.bz2)
source=(ftp://ftp.archlinux.org/other/ffmpeg/ffmpeg-20080625-13984.tar.bz2)
md5sums=('ed92592b2024a5ad8aa484e2c87dfd61')

build() {
  cd "$srcdir/$pkgname" || return 1

  ./configure \
  --prefix=/usr \
  --enable-gpl \
  --enable-libmp3lame \
  --enable-libvorbis \
  --enable-libfaac \
  --enable-libfaad \
  --enable-liba52 \
  --enable-libxvid \
  --enable-libx264 \
  --enable-libtheora \
  --enable-postproc \
  --enable-shared \
  --enable-pthreads \
  --enable-x11grab \
  --enable-swscale \
  || return 1

  make -j 2 || return 1
  make doc/ff{mpeg,play,server}.1 || return 1

  make DESTDIR="$pkgdir" install || return 1
  make DESTDIR="$pkgdir" install-man || return 1
}

# vim:set ts=2 sw=2 et:
