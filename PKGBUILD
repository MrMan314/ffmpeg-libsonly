# Maintainer : Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg
pkgver=23328
pkgrel=1
pkgdesc="Complete and free Internet live audio and video broadcasting solution for Linux/Unix"
arch=('i686' 'x86_64')
url="http://ffmpeg.org/"
license=('GPL')
depends=('bzip2' 'lame' 'sdl' 'libvorbis' 'faad2>=2.7' 'faac' 'xvidcore' 'zlib' 'x264>=20100410' 'libtheora' 'opencore-amr>=0.1.2' 'alsa-lib' 'libvdpau' 'libxfixes' 'schroedinger>=1.0.9')
makedepends=('yasm')
#remake snapshot with: svn export svn://svn.ffmpeg.org/ffmpeg/trunk/@23328
source=(ftp://ftp.archlinux.org/other/ffmpeg/ffmpeg-${pkgver}.tar.xz)
#source=(http://ffmpeg.org/releases//releases/ffmpeg-${pkgver}.tar.bz2)
sha256sums=('0b9a9452106ee544bb095b1c61870f7b1c1176833220d12ffc52ba5fbf23c18a')

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
  --enable-libopencore_amrnb \
  --enable-libopencore_amrwb \
  --enable-libschroedinger \
  --enable-version3 \
  --enable-nonfree \
  --enable-runtime-cpudetect || return 1 # libfaac is nonfree

  make || return 1
  make tools/qt-faststart || return 1
  make doc/ff{mpeg,play,server}.1 || return 1

  make DESTDIR="$pkgdir" install install-man || return 1
  install -D -m755 tools/qt-faststart "$pkgdir/usr/bin/qt-faststart" || return 1

  # since makepkg currently declines to strip .a files, do this for now
  strip --strip-debug "$pkgdir"/usr/lib/*.a || return 1
}

# vim:set ts=2 sw=2 et:
