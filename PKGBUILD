# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>

_offline="false"
_git="false"
_py="python"
_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=ethereum-mnemonic-utils
pkgname="${_pkg}"
pkgver=0.0.0.0.0.0.0.0.0.0.0.1.1.1.1.1
_commit="a176f1331a69c370dae6a21365bdb0aa66f4ac03"
pkgrel=1
_pkgdesc=(
  "Convert Ethereum mnemonic keys into regular private keys."
)
pkgdesc="${_pkgdesc[*]}"
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'armv7l'
  'armv6l'
  'i686'
  'mips'
  'powerpc'
  'pentium4'
)
_http="https://github.com"
_ns="themartiancompany"
url="${_http}/${_ns}/${pkgname}"
license=(
  'AGPL3'
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
  "${_py}-base58"
  "${_py}-ecdsa"
)
_os="$( \
  uname \
    -o)"
[[ "${_os}" != "GNU/Linux" ]] && \
[[ "${_os}" == "Android" ]] && \
  depends+=(
  )
optdepends=(
)
[[ "${_os}" == 'Android' ]] && \
  optdepends+=(
  )
makedepends=(
  "${_py}-setuptools"
  "cython"
)
checkdepends=(
  "shellcheck"
)
provides=(
  "${_py}-${_pkg}=${pkgver}"
)
conflicts=(
  "${_py}-${_pkg}"
)
_url="${url}"
_tag="${_commit}"
_tag_name="commit"
_tarname="${pkgname}-${_tag}"
[[ "${_offline}" == "true" ]] && \
  _url="file://${HOME}/${pkgname}"
if [[ "${_git}" == true ]]; then
  makedepends+=(
    "git"
  )
  _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
  _sum="SKIP"
elif [[ "${_git}" == false ]]; then
  if [[ "${_tag_name}" == 'pkgver' ]]; then
    _src="${_tarname}.tar.gz::${_url}/archive/refs/tags/${_tag}.tar.gz"
    _sum="d4f4179c6e4ce1702c5fe6af132669e8ec4d0378428f69518f2926b969663a91"
  elif [[ "${_tag_name}" == "commit" ]]; then
    _src="${_tarname}.zip::${_url}/archive/${_commit}.zip"
    _sum='2884604eaad35725523518f81ac1796d8f572f78e63c842f938c22457466f91e'
  fi
fi
source=(
  "${_src}"
)
sha256sums=(
  "${_sum}"
)
validpgpkeys=(
  # Truocolo <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
)

check() {
  cd \
    "${_tarname}"
  make \
    -k \
    check
}

# shellcheck disable=SC2154
package() {
  cd \
    "${_tarname}"
  "${_py}" \
    setup.py \
    install \
    --root="${pkgdir}" \
    --optimize=1
}

# vim: ft=sh syn=sh et
