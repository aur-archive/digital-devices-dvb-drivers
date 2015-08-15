# Submitter:   Wessel Dirksen "p-we" <wdirksen at gmail dot com>

pkgname=digital-devices-dvb-drivers
pkgver=0.9.10
pkgrel=2
pkgdesc="Digital Devices proprietary DVB drivers"
url="http://www.digitaldevices.de"
arch=('i686' 'x86_64')
license=('GPLv2')
makedepends=('linux-headers')
conflicts=('ffdecsawrapper' 'digital-devices-dvb-drivers')
provides=('digital-devices-dvb-drivers')
install='digital-devices-dvb-drivers.install'
_dddvbver=dddvb-0.9.10

source=(http://download.digital-devices.de/download/linux/$_dddvbver.tar.bz2 \
	digital-devices-dvb-drivers.install)

sha256sums=('6fb881bd52296669f56d63fd960264644b519d9b7815013f2964b5726a9984ab'
            'd191c1c6c8389988053b6498af26190f304c34910917b2e8360c2434da1b7f4b')

pkgver() {

	_kernel=`uname -r | sed -r 's/-/_/g'`
	echo 0.9.10_$_kernel
}

build() {

	rm -rf "$srcdir/$_dddvbver-build"
	cp -r "$srcdir/$_dddvbver" "$srcdir/$_dddvbver-build"
	
	cd "$srcdir/$_dddvbver-build"
	make all
}

package() {

	mkdir -p $pkgdir/usr/lib/modules/`uname -r`/updates/dddvb
	find "$srcdir/$_dddvbver-build" -name '*.ko' -exec cp {} $pkgdir/usr/lib/modules/`uname -r`/updates/dddvb \;

	find "$pkgdir" -name '*.ko' -exec gzip -9 {} \;
	chmod 644 -R $pkgdir/usr/lib/modules/`uname -r`/updates
}
