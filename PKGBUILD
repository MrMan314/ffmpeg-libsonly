# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Maintainer: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=20081220
pkgrel=1
pkgdesc="Complete and free Internet live audio and video broadcasting solution for Linux/Unix"
arch=(i686 x86_64)
url="http://ffmpeg.mplayerhq.hu/"
license=('LGPL')
depends=('lame' 'sdl' 'libvorbis' 'faad2>=2.6.1' 'faac' 'xvidcore' 'zlib' 'imlib2' 'x264>=20090108' 'libtheora')
#remake snapshot with: svn export svn://svn.mplayerhq.hu/ffmpeg/trunk@14236
source=(ftp://ftp.archlinux.org/other/ffmpeg/ffmpeg-${pkgver}-16503.tar.bz2)
md5sums=('3df85782e9fbbb4a40c6b807baaf6808')

build() {
  cd "$srcdir/$pkgname" || return 1

  ./configure \
  --prefix=/usr \
  --enable-gpl \
  --enable-libmp3lame \
  --enable-libvorbis \
  --enable-libfaac \
  --enable-libfaad \
  --enable-libxvid \
  --enable-libx264 \
  --enable-libtheora \
  --enable-postproc \
  --enable-shared \
  --enable-pthreads \
  --enable-x11grab \
  --enable-swscale \
  || return 1

  make || return 1
  make doc/ff{mpeg,play,server}.1 || return 1

  make DESTDIR="$pkgdir" install install-man || return 1

  # since makepkg currently declines to strip .a files, do this for now
  strip --strip-debug $startdir/pkg/usr/lib/*.a || return 1
}

# vim:set ts=2 sw=2 et:
