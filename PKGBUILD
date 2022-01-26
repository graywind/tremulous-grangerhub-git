origname=tremulous
pkgname="${origname}-grangerhub-git"
origver=1.3.0
pkgver=v1.3.0_alpha.0.13_13_g33b28b6f
pkgrel=1
pkgdesc='Team based FPS/RTS hybrid built on the open ioq3 engine.'
url='http://tremulous.net'
arch=('x86_64' 'i686' 'aarch64')
license=('GPL')
depends=('sdl' 'openal' 'libgl' "tremulous-data=1.1.0" "freetype2" 'glu')
makedepends=('git' 'mesa')
provides=("tremulous-updated=${origver}-${pkgrel}")
conflicts=('tremulous-updated')
replaces=('trem-backport' 'tremulous-updated')
source=(git+https://github.com/graywind/tremulous.git#branch=arm64-aur-fixes
        autogen.cfg
        tremdedrc
        tremded.sh
        tremulous.sh
        tremulous.desktop
        tremulous.xpm)

backup=('etc/tremdedrc')

_arch="${CARCH/i686/x86}"

pkgver() {
  cd "${srcdir}/${origname}"
#  echo "${origver}.r$(git rev-list --count HEAD).$(git rev-parse --short HEAD)"
# Use same version info expected in upstream Makefile
  echo "$(git describe --tag | sed -e 's/-/_/g')"
}

build() {
  cd "${srcdir}/${origname}"
#  export USE_INTERNAL_JPEG=0
  make release
}

package() {
  cd "${srcdir}/${origname}"
  install -D -m644 "${srcdir}/autogen.cfg"  "${pkgdir}/opt/tremulous/autogen.cfg"
  install -D -m644 "${srcdir}/tremdedrc"    "${pkgdir}/etc/tremdedrc"
  install -D -m755 "${srcdir}/tremded.sh"   "${pkgdir}/usr/bin/tremded"
  install -D -m755 "${srcdir}/tremulous.sh" "${pkgdir}/usr/bin/tremulous"

  install -D -m755 "build/release-linux-${_arch}/tremded" \
    "${pkgdir}/opt/tremulous/tremded"
  install -D -m755 "build/release-linux-${_arch}/tremulous" \
    "${pkgdir}/opt/tremulous/tremulous"
  install -D -m755 "build/release-linux-${_arch}/renderer_opengl1.so" \
    "${pkgdir}/opt/tremulous/renderer_opengl1.so"
  install -D -m755 "build/release-linux-${_arch}/renderer_opengl2.so" \
    "${pkgdir}/opt/tremulous/renderer_opengl2.so"
  install -D -m755 "build/release-linux-${_arch}/gpp/data-${pkgver}.pk3" \
    "${pkgdir}/opt/tremulous/base/data-${pkgver}.pk3"
  install -D -m755 "build/release-linux-${_arch}/gpp_11/vms-${pkgver}.pk3" \
    "${pkgdir}/opt/tremulous/base/vms-${pkgver}.pk3"

  # Install the .desktop and icon files
  install -D -m644 "${srcdir}/tremulous.xpm"     "${pkgdir}/usr/share/pixmaps/tremulous.xpm"
  install -D -m644 "${srcdir}/tremulous.desktop" "${pkgdir}/usr/share/applications/tremulous.desktop"
}

sha256sums=('SKIP'
            '6a41333f4b2a4937b91cd26bc257575ee55c1f1c8dae1324c880c4fad32c6c0f'
            '7393025b937812220a0e6a3e16112ae3a7f1297ad4fcdebd3d944676ca26697c'
            '2c6eda990fa4f244ce5019a15874cf8bd7d103ca8941582213881098b01d5349'
            '59dd383809cfe1064505adf436c921b0783eb542720e97a73291746b17f85399'
            '9af436e7f004abeb043276de6948d6142a8a4cfb554993b7aa8d9e09e41acafa'
            '0770cc5e153b25e00d42077e3f0e7f813264f1db468efca2a26083a5d38301d1'
)
