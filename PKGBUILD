# Maintainer : Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=20110622
pkgrel=1
pkgdesc="Complete and free Internet live audio and video broadcasting solution for Linux/Unix"
arch=('i686' 'x86_64')
url="http://ffmpeg.org/"
license=('GPL')
depends=('bzip2' 'lame' 'sdl' 'libvorbis' 'xvidcore' 'zlib' 'x264' 'libtheora' 'opencore-amr' 'alsa-lib' 'libvdpau' 'libxfixes' 'schroedinger' 'libvpx' 'libva' 'openjpeg' 'rtmpdump')
makedepends=('yasm' 'git')
#git clone git://git.videolan.org/ffmpeg.git
source=(ftp://ftp.archlinux.org/other/ffmpeg/${pkgname}-${pkgver}.tar.xz)
md5sums=('ff3636c6601f68cdcc777fadaf0eba46')

build() {
  cd "$srcdir/$pkgname"

  ./configure \
    --prefix=/usr \
    --enable-libmp3lame \
    --enable-libvorbis \
    --enable-libxvid \
    --enable-libx264 \
    --enable-libvpx \
    --enable-libtheora \
    --enable-postproc \
    --enable-shared \
    --enable-x11grab \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libschroedinger \
    --enable-libopenjpeg \
    --enable-librtmp \
    --enable-gpl \
    --enable-version3 \
    --enable-runtime-cpudetect \
    --disable-debug

  make
  make tools/qt-faststart
  make doc/ff{mpeg,play,server}.1

  make DESTDIR="$pkgdir" install install-man
  install -D -m755 tools/qt-faststart "$pkgdir/usr/bin/qt-faststart"
}

# vim:set ts=2 sw=2 et:
md5sums=('6003afa1f87857db729d697e3ec1be36')
