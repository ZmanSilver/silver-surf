# Maintainer: Zachary Silver <zmansilver@gmail.com>

pkgname=silver-surf
pkgver=2.0
pkgrel=1
pkgdesc="a customized version of a WebKit based browser"
arch=('i686' 'x86_64')
url="https://github.com/ZmanSilver/silver-surf"
license=('MIT')
depends=('webkit2gtk' 'gcr' 'xorg-xprop')
makedepends=('git')
optdepends=('dmenu: url bar and search'
            'tabbed: tab browsing'
            'ca-certificates: SSL verification'
            'st: default terminal for the download handler'
            'curl: default download handler'
            'mpv: default video player')
provides=($pkgname)
conflicts=($pkgname)
source=(https://www.dropbox.com/s/zq9jdu7yc6oknwu/silver-surf.tar.gz
        config.h)
md5sums=('6115859b5387db15570c8ac57e156a7c'
         'b6d2c7c87caa1139d1e44e05ef7109db')

prepare() {
  cd $pkgname
  for file in "${source[@]}"; do
      if [[ "$file" == "config.h" ]]; then
          # add config.h if present in source array
          cp "$srcdir/$file" .
      elif [[ "$file" == *.diff || "$file" == *.patch ]]; then
          # add all patches present in source array
          patch -Np1 < "$srcdir/$(basename ${file})"
      fi
   done
}

build() {
  cd "$pkgname"
  make PREFIX=/usr DESTDIR="$pkgdir"
}

package() {
  cd "$pkgname"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
