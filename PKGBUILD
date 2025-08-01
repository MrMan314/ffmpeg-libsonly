# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Contributor: Bartłomiej Piotrowski <bpiotrowski@archlinux.org>
# Contributor: Ionut Biru <ibiru@archlinux.org>
# Contributor: Tom Newsom <Jeepster@gmx.co.uk>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=ffmpeg-libsonly
pkgver=7.1.1
pkgrel=5
epoch=2
pkgdesc='Complete solution to record, convert and stream audio and video'
arch=(x86_64)
url=https://ffmpeg.org
license=(GPL-3.0-only)
depends=(
  alsa-lib
  aom
  bzip2
  cairo
  dav1d
  fontconfig
  freetype2
  fribidi
  glib2
  glibc
  glslang
  gmp
  gnutls
  gsm
  harfbuzz
  jack
  lame
  libass
  libavc1394
  libbluray
  libbs2b
  libdrm
  libdvdnav
  libdvdread
  libgl
  libiec61883
  libjxl
  libmodplug
  libopenmpt
  libplacebo
  libpulse
  libraw1394
  librsvg
  libsoxr
  libssh
  libtheora
  libva
  libvdpau
  libvorbis
  libvpx
  libwebp
  libx11
  libxcb
  libxext
  libxml2
  libxv
  ocl-icd
  onevpl
  opencore-amr
  openjpeg2
  opus
  rav1e
  rubberband
  sdl2
  snappy
  speex
  srt
  svt-av1
  v4l-utils
  vapoursynth
  vid.stab
  vmaf
  vulkan-icd-loader
  x264
  x265
  xvidcore
  xz
  zeromq
  zimg
  zlib
)
makedepends=(
  amf-headers
  avisynthplus
  clang
  ffnvcodec-headers
  frei0r-plugins
  git
  ladspa
  mesa
  nasm
  opencl-headers
  vulkan-headers
)
optdepends=(
  'avisynthplus: AviSynthPlus support'
  'frei0r-plugins: Frei0r video effects support'
  'intel-media-sdk: Intel QuickSync support (legacy)'
  'ladspa: LADSPA filters'
  'nvidia-utils: Nvidia NVDEC/NVENC support'
  'onevpl-intel-gpu: Intel QuickSync support'
)
provides=(
  libavcodec.so
  libavdevice.so
  libavfilter.so
  libavformat.so
  libavutil.so
  libpostproc.so
  libswresample.so
  libswscale.so
)
_tag=a1328e68877e12ab5a6e5d92a84aefa566783ea5
source=(
  git+https://git.ffmpeg.org/ffmpeg.git?signed#tag=${_tag}
  0001-Add-av_stream_get_first_dts-for-Chromium.patch
  0002-avcodec-libsvtav1-unbreak-build-with-latest-svtav1.patch
  fix_build_with_v4l2_1.30.patch
)
b2sums=('c7b1a56593f123de8e18b3b93c81dca4aff439f5701935cc1fe6316543e8c3256acd7f95b4a533eb7ba30e346fa13bf0ad5bff54b7822c088ef3939882416a7c'
        'e5f7b79f7731be9ee5a7280a9221fb531ac5a2d9820fc5870b68b0eabea667dfbe8f39f41c1e1763a4c84982896afaa54c81ff57847d203b70afafd726689e5d'
        'a32aeff68032a78d661011654bbdba138002833f7d17d23bba6f95479ca22bef5697eb9e7e4cb9e0b5140fc23eab3aab16fc60962d62809c3c02f890599a8332'
        'a713b3a4243cc5de3867f7c210172c094f50bd614c0c8be2c99d6161b06d43d9183ae9c442ac3056bfe06c28419e276d129b1235471466eedd340bf0c4780acb')
validpgpkeys=(DD1EC9E8DE085C629B3E1846B18E8928B3948D64) # Michael Niedermayer <michael@niedermayer.cc>

prepare() {
  cd ffmpeg

  # Fix build with v4l2 >= 1.30
  # https://trac.ffmpeg.org/ticket/11570
  patch -Np1 -i "${srcdir}/fix_build_with_v4l2_1.30.patch"

  # https://crbug.com/1251779
  git apply -3 ../0001-Add-av_stream_get_first_dts-for-Chromium.patch

  # Fix for svt-av1
  # Taken from https://github.com/FFmpeg/FFmpeg/commit/d1ed5c06e3edc5f2b5f3664c80121fa55b0baa95.patch
  git apply -3 ../0002-avcodec-libsvtav1-unbreak-build-with-latest-svtav1.patch

  # VAAPI HEVC encode alignment fix
  git cherry-pick -n bcfbf2bac8f9eeeedc407b40596f5c7aaa0d5b47
  git cherry-pick -n d0facac679faf45d3356dff2e2cb382580d7a521
}

pkgver() {
  cd ffmpeg
  git describe --tags | sed 's/^n//'
}

build() {
  export PKG_CONFIG_PATH='/usr/lib/mbedtls2/pkgconfig'
  cd ffmpeg
  ./configure \
    --prefix=/usr \
    --incdir=/usr/include/ffmpeg${pkgver} \
    --libdir=/usr/lib/ffmpeg${pkgver} \
    --disable-debug \
    --disable-doc \
    --disable-programs \
    --disable-static \
    --disable-stripping \
    --enable-amf \
    --enable-avisynth \
    --enable-cuda-llvm \
    --enable-lto \
    --enable-fontconfig \
    --enable-frei0r \
    --enable-gmp \
    --enable-gnutls \
    --enable-gpl \
    --enable-ladspa \
    --enable-libaom \
    --enable-libass \
    --enable-libbluray \
    --enable-libbs2b \
    --enable-libdav1d \
    --enable-libdrm \
    --enable-libdvdnav \
    --enable-libdvdread \
    --enable-libfreetype \
    --enable-libfribidi \
    --enable-libglslang \
    --enable-libgsm \
    --enable-libharfbuzz \
    --enable-libiec61883 \
    --enable-libjack \
    --enable-libjxl \
    --enable-libmodplug \
    --enable-libmp3lame \
    --enable-libopencore_amrnb \
    --enable-libopencore_amrwb \
    --enable-libopenjpeg \
    --enable-libopenmpt \
    --enable-libopus \
    --enable-libplacebo \
    --enable-libpulse \
    --enable-librav1e \
    --enable-librsvg \
    --enable-librubberband \
    --enable-libsnappy \
    --enable-libsoxr \
    --enable-libspeex \
    --enable-libsrt \
    --enable-libssh \
    --enable-libsvtav1 \
    --enable-libtheora \
    --enable-libv4l2 \
    --enable-libvidstab \
    --enable-libvmaf \
    --enable-libvorbis \
    --enable-libvpl \
    --enable-libvpx \
    --enable-libwebp \
    --enable-libx264 \
    --enable-libx265 \
    --enable-libxcb \
    --enable-libxml2 \
    --enable-libxvid \
    --enable-libzimg \
    --enable-libzmq \
    --enable-nvdec \
    --enable-nvenc \
    --enable-opencl \
    --enable-opengl \
    --enable-shared \
    --enable-vapoursynth \
    --enable-version3 \
    --enable-vulkan
  make
#  make tools/qt-faststart
#  make doc/ff{mpeg,play}.1
}

package() {
  depends+=(
    libass.so
    libbluray.so
    libbs2b.so
    libdav1d.so
    libfreetype.so
    libharfbuzz.so
    libjxl.so
    libopenmpt.so
    libplacebo.so
    librav1e.so
    librsvg-2.so
    librubberband.so
    libva.so
    libva-drm.so
    libva-x11.so
    libvidstab.so
    libvorbisenc.so
    libvorbis.so
    libvpx.so
    libx264.so
    libx265.so
    libxvidcore.so
    libzimg.so
    libzmq.so
  )
  mkdir -p "${pkgdir}"/usr/bin/
  make DESTDIR="${pkgdir}" -C ffmpeg install
  cd "${pkgdir}"

  local f
  for f in usr/lib/ffmpeg${pkgver}/*; do
    if [[ $f == *.so ]]; then
      ln -srf -- usr/lib/"$(readlink "$f")" "$f"
    elif [[ ! -d $f ]]; then
      mv "$f" usr/lib
	fi
  done
  rm -r usr/share
}

# vim: ts=2 sw=2 et:
