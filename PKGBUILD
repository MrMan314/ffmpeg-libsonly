# Maintainer : Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=1.0
pkgrel=2
epoch=1
pkgdesc="Complete and free Internet live audio and video broadcasting solution for Linux/Unix"
arch=('i686' 'x86_64')
url="http://ffmpeg.org/"
license=('GPL')
depends=(alsa-lib bzip2 gsm lame libpulse libtheora libva libvorbis libvpx opencore-amr openjpeg rtmpdump schroedinger sdl speex v4l-utils x264 xvidcore zlib)
makedepends=('yasm' 'git' 'libvdpau')
source=(http://ffmpeg.org/releases/$pkgname-$pkgver.tar.bz2)
md5sums=('3ed526cea20c1bffb5a37f7730f710bd')

build() {
  cd $pkgname-$pkgver

  ./configure \
    --prefix=/usr \
    --enable-libmp3lame \
    --enable-libvorbis \
    --enable-libxvid \
    --enable-libx264 \
    --enable-libvpx \
    --enable-libtheora \
    --enable-libgsm \
    --enable-libspeex \
    --enable-postproc \
    --enable-shared \
    --enable-x11grab \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libschroedinger \
    --enable-libopenjpeg \
    --enable-librtmp \
    --enable-libpulse \
    --enable-libv4l2 \
    --enable-gpl \
    --enable-version3 \
    --enable-runtime-cpudetect \
    --disable-debug \
    --disable-static

  make
  make tools/qt-faststart
  make doc/ff{mpeg,play,server}.1
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install install-man
  install -D -m755 tools/qt-faststart "$pkgdir/usr/bin/qt-faststart"
}

# vim:set ts=2 sw=2 et:
