# Maintainer : Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=2.0.2
pkgrel=1
epoch=1
pkgdesc="Complete and free Internet live audio and video broadcasting solution for Linux/Unix"
arch=('i686' 'x86_64')
url="http://ffmpeg.org/"
license=('GPL')
depends=(
      'alsa-lib' 'bzip2' 'fontconfig' 'gsm' 'lame' 'libass'
      'libbluray' 'libmodplug' 'libpulse' 'libtheora' 'libva' 'libvorbis' 'libvpx'
      'opencore-amr' 'openjpeg' 'opus' 'rtmpdump' 'schroedinger' 'sdl' 'speex'
      'v4l-utils' 'x264' 'xvidcore' 'zlib'
      )
makedepends=('libvdpau' 'yasm')
source=(http://ffmpeg.org/releases/$pkgname-$pkgver.tar.bz2)
sha256sums=('986f63dc0785f473b1832d0eead502e39c9706fbe7f9677bbea0dad6fe0fab4a')

build() {
  cd $pkgname-$pkgver

  ./configure \
    --prefix=/usr \
    --disable-debug \
    --disable-static \
    --enable-avresample \
    --enable-dxva2 \
    --enable-fontconfig \
    --enable-gpl \
    --enable-libass \
    --enable-libbluray \
    --enable-libfreetype \
    --enable-libgsm \
    --enable-libmodplug \
    --enable-libmp3lame \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libopenjpeg \
    --enable-libopus \
    --enable-libpulse \
    --enable-librtmp \
    --enable-libschroedinger \
    --enable-libspeex \
    --enable-libtheora \
    --enable-libv4l2 \
    --enable-libvorbis \
    --enable-libvpx \
    --enable-libx264 \
    --enable-libxvid \
    --enable-pic \
    --enable-postproc \
    --enable-runtime-cpudetect \
    --enable-shared \
    --enable-swresample \
    --enable-vdpau \
    --enable-version3 \
    --enable-x11grab

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
