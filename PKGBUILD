# $Id$
# Maintainer: Alex Ryzhkov <junkntrash AT tutanota.com>
# Contributor: Hans-Nikolai Viessmann <hv15 AT hw.ac.uk>
# Contributor: Vladimir Protasov <eoranged@ya.ru>
# Contributor: Eric Bélanger <eric@archlinux.org>

pkgname='moc-pulse'
_pkgname='moc'
pkgver=2.5.2
pkgrel=2
pkgdesc='An ncurses console audio player with support for pulseaudio'
arch=('x86_64')
url="http://moc.daper.net/"
license=('GPL')
depends=('libmad' 'libid3tag' 'jack' 'curl' 'libltdl' 'file' 'pulseaudio')
makedepends=('speex' 'ffmpeg' 'taglib' 'libmpcdec' 'wavpack' 'libmodplug' 'faad2')
optdepends=('speex: for using the speex plugin'
	        'ffmpeg: for using the ffmpeg plugin'
	        'taglib: for using the musepack plugin'
	        'libmpcdec: for using the musepack plugin'
            'wavpack: for using the wavpack plugin'
            'faad2: for using the aac plugin'
	        'libmodplug: for using the modplug plugin')
provides=('moc')
conflicts=('moc')
source=(http://ftp.daper.net/pub/soft/moc/stable/${_pkgname}-${pkgver}.tar.bz2{,.sig}
        'pulseaudio.patch'
        'moc-ffmpeg4.patch'
        'always-playlist.patch')
sha1sums=('9d27a929b63099416263471c16367997c0ae6dba'
          'SKIP'
          '5c6385760ba40ee8a330d28d520c44eac2cbbae1'
          '007a0580ac754e1c318a0d0b6f0d403883797eaf'
          '5b2abd148e23fc374623c8aee07605f08291cc9c')
validpgpkeys=('59359B80406D9E73E80599BEF3121E4F2885A7AA')

prepare() {
  cd "${_pkgname}-${pkgver}"
  # Fix build with ffmpeg 4 (taken from official release on ArchLinux)
  patch -p0 -i ../moc-ffmpeg4.patch
  # Add pulseaudio backend
  patch -p1 -i ../pulseaudio.patch
  # Make Moc start in playlist view by default
  patch -p0 -i ../always-playlist.patch

}

build() {
  cd "${_pkgname}-${pkgver}"

  msg "Re-creating ./configure script"
  aclocal
  automake --add-missing
  autoreconf

  msg "Begin configuring"
  ./configure --prefix=/usr --without-rcc \
    --with-pulse --with-oss --with-alsa --with-jack --with-aac \
    --with-mp3 --with-musepack --with-vorbis --with-flac \
    --with-wavpack --with-sndfile --with-modplug --with-ffmpeg \
    --with-speex --with-samplerate --with-curl  --disable-cache \
    --disable-debug
  make
}

package() {
  cd ${_pkgname}-${pkgver}
  make DESTDIR="${pkgdir}" install
}

# vim: ts=2 sw=2
