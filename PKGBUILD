# Maintainer: Yarema aka Knedlyk <yupadmin@gmail.com>

pkgname=texstudio-svn
pkgver=4145
pkgrel=1
pkgdesc="TeXstudio is a fork of the LaTeX IDE TexMaker. Gives you an environment where you can easily create and manage LaTeX documents."
arch=('i686' 'x86_64')
url="http://texstudio.sourceforge.net"
license=('GPL')
depends=('qt4' 'poppler-qt4')
conflicts=('texmakerx' 'texstudio')

_svntrunk=svn://svn.code.sf.net/p/texstudio/code/trunk 
_svnmod=texstudio

package() {
cd "$srcdir"

  if [ -d $_svnmod/.svn ]; then
    (cd $_svnmod && svn up -r $pkgver)
  else
    svn co $_svntrunk --config-dir ./ -r $pkgver $_svnmod
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"
  pwd
    qmake-qt4 texstudio.pro || return 1
    make || return 1
    make INSTALL_ROOT="$pkgdir" install || return 1
    sed -i $pkgdir/usr/share/applications/texstudio.desktop -e "s:texmakerx:texstudio:" 
}