##This is a basic PKGBUILD for rdis to ease building RDIS in my Arch boxes
##Maintainer : TDKPS
pkgname=rdis-lua
pkgrel=1
pkgdesc="Scripts for the binary analysis tool rdis - implement GDB support"
pkgver=20121230
arch=(x86_64)
url="https://github.com/endeav0r/rdis-lua"
license=('GPLv3')
depends=(gtk3 luajit cairo jansson git lua51-socket rdis-git lua-lgi51-git)
_gitroot="https://github.com/endeav0r/rdis-lua.git"
_gitname="rdis-lua"
install=cleanup.install
#set path to .rdis.conf
path=        ##change this as needed

build() {

  #define folder placement variable
  where=/usr/share/rdis-lua
  cd "$srcdir"

  msg "Connecting to GIT server..."
  if [[ -d ${_gitname} ]]; then
    (cd ${_gitname} && git pull origin)
  else
    git clone ${_gitroot} ${_gitname}
  fi

  msg "GIT checkout done or server timeout"
  msg "Creating rdis-lua directory in $where"
  
  if [[ -d $where ]]; then
  
    cp $srcdir/rdis-lua/* $where
    rm -r $srcdir
  
  else 

      mkdir $where
      cp $srcdir/rdis-lua/* $where
      rm -r $srcdir
  fi

  msg "File copying done." 
  msg "Configurating .rdis.conf"
  msg "Setting path to rdis-lua to previously chosen location"
  #PATH_TO_RDIS_LUA = $where
  #These are initial configurations. Should you wish to modify it now, add your configuration to $inputconf or leave it the way it is 
  msg "These are the current $inputconf that'll be passed to .rdis.conf"
  inputconf="local PATH_TO_RDIS_LUA = '$where'
  package.path = package.path .. ';' .. PATH_TO_RDIS_LUA .. '/?.lua'
  dofile(PATH_TO_RDIS_LUA .. '/rdis.lua')"
  echo "$inputconf" > $path

  msg "Complete"

  }