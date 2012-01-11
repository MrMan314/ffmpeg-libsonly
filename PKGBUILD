# Maintainer : Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=20120111
pkgrel=1
pkgdesc="Complete and free Internet live audio and video broadcasting solution for Linux/Unix"
arch=('i686' 'x86_64')
url="http://ffmpeg.org/"
license=('GPL')
depends=(alsa-lib bzip2 gsm lame libpulse libtheora libva libvorbis libvpx opencore-amr openjpeg rtmpdump schroedinger sdl speex x264 xvidcore zlib)
makedepends=('yasm' 'git' 'libvdpau')
#git clone git://git.videolan.org/ffmpeg.git
source=(ftp://ftp.archlinux.org/other/ffmpeg/$pkgname-$pkgver.tar.xz
        revert-enabling-threads.patch)
md5sums=('7a54b2b1af86a746696d1c0b2a79979c'
         '79cc22bc2ac3e67d96c340cb7061e64d')

build() {
  cd "$srcdir/$pkgname"

  patch -Np1 -R -i "$srcdir/revert-enabling-threads.patch"

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
  cd "$srcdir/$pkgname"
  make DESTDIR="$pkgdir" install install-man
  install -D -m755 tools/qt-faststart "$pkgdir/usr/bin/qt-faststart"
}

# vim:set ts=2 sw=2 et:
