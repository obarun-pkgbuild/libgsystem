# Maintainer: Eric Vidal <eric@obarun.org>
# based on the original https://git.archlinux.org/svntogit/packages.git/log/trunk?h=packages/libgsystem
# 						Maintainer: Jan Alexander Steffens (heftig) <jan.steffens@gmail.com>

pkgname=libgsystem
pkgver=2015.2+4+gd606bec
pkgrel=2
pkgdesc='"Copylib" for system service modules using GLib with GCC'
url="https://wiki.gnome.org/Projects/LibGSystem"
license=(GPL2)
arch=(x86_64)
depends=(glib2 attr)
makedepends=(gobject-introspection gtk-doc git)
_commit=d606bec68ddfea78de4b03c3f3568afb71bdc1ce  # master
source=("git+https://git.gnome.org/browse/libgsystem#commit=$_commit"
        "git+https://git.gnome.org/browse/libglnx")
sha256sums=('SKIP'
            'SKIP')
validpgpkeys=('6DD4217456569BA711566AC7F06E8FDE7B45DAAC') # Eric Vidal

pkgver() {
  cd $pkgname
  git describe --tags | sed 's/^v//;s/-/+/g'
}

prepare() {
  cd $pkgname

  git submodule init
  git config --local submodule.libglnx.url "$srcdir/libglnx"
  git submodule update

  NOCONFIGURE=1 ./autogen.sh
}

build() {
  cd $pkgname
  ./configure	--prefix=/usr \
				--disable-static \
				--enable-gtk-doc \
				--without-systemd-journal
  make
}

check() {
  cd $pkgname
  make check
}

package() {
  cd $pkgname
  make DESTDIR="$pkgdir" install
}
