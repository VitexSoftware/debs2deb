DEBs2Deb
========

Offline repository as debian package

![debs2deb](debs2deb.svg?raw=true)

Usage
-----

```shell
debs2deb /debs/path/ packagename
```

Script recursively find debian packages in path and build debian package from it.
Package contains also its /etc/apt/sources.list.d/PACKNAME.list for easy installation of packages

```shell
vitex@exiv:~$ debs2deb /tmp/crio
generating crio.deb from /tmp/crio
 dpkg-buildpackage -us -uc -ui -i -b
dpkg-buildpackage: info: source package crio
dpkg-buildpackage: info: source version 1627134198
dpkg-buildpackage: info: source distribution UNRELEASED
dpkg-buildpackage: info: source changed by Vitex <info@vitexsoftware.cz>
 dpkg-source -i --before-build .
dpkg-buildpackage: info: host architecture amd64
 fakeroot debian/rules clean
dh clean
   dh_clean
 debian/rules build
dh build
   dh_update_autotools_config
   dh_autoreconf
   create-stamp debian/debhelper-build-stamp
 fakeroot debian/rules binary
dh binary
   dh_testroot
   dh_prep
   debian/rules override_dh_install
make[1]: Vstupuje se do adresáře „/var/tmp/debs2deb/crio_1627134198“
dh_install
mkdir -p /var/tmp/debs2deb/crio_1627134198/debian/crio/var/lib/debs2deb/crio
mkdir -p /var/tmp/debs2deb/crio_1627134198/debian/crio/etc/apt/sources.list.d/
cp /tmp/crio/conmon_100%3a2.0.27-1_amd64.deb  /var/tmp/debs2deb/crio_1627134198/debian/crio/var/lib/debs2deb/crio
cp /tmp/crio/containers-common_100%3a1-17_all.deb  /var/tmp/debs2deb/crio_1627134198/debian/crio/var/lib/debs2deb/crio
cp /tmp/crio/cri-o-runc_1.0.0-1_amd64.deb  /var/tmp/debs2deb/crio_1627134198/debian/crio/var/lib/debs2deb/crio
cp /tmp/crio/cri-o_1.20.3~0_amd64.deb  /var/tmp/debs2deb/crio_1627134198/debian/crio/var/lib/debs2deb/crio
echo "Remove me using: apt-get remove crio" > /var/tmp/debs2deb/crio_1627134198/debian/crio/etc/apt/sources.list.d/crio.list
echo "deb [trusted=yes] file:///var/lib/debs2deb/ crio/" > /var/tmp/debs2deb/crio_1627134198/debian/crio/etc/apt/sources.list.d/crio.list
dpkg-scanpackages --multiversion /var/tmp/debs2deb/crio_1627134198/debian/crio/var/lib/debs2deb/crio /dev/null | sed  's#/var/tmp/debs2deb/crio_1627134198/debian/crio/var/lib/debs2deb/crio#crio#g' > /var/tmp/debs2deb/crio_1627134198/debian/crio/var/lib/debs2deb/crio/Packages
dpkg-scanpackages: warning: Packages in archive but missing from override file:
dpkg-scanpackages: warning:   conmon containers-common cri-o cri-o-runc
dpkg-scanpackages: info: Wrote 4 entries to output Packages file.
make[1]: Opouští se adresář „/var/tmp/debs2deb/crio_1627134198“
   dh_installdocs
   dh_installchangelogs
   dh_perl
   dh_link
   dh_strip_nondeterminism
   dh_compress
   dh_fixperms
   dh_missing
   dh_installdeb
   dh_gencontrol
   dh_md5sums
   dh_builddeb
dpkg-deb: vytvářím balík „crio“ v „../crio_1627134198_all.deb“.
 dpkg-genbuildinfo --build=binary
 dpkg-genchanges --build=binary >../crio_1627134198_amd64.changes
dpkg-genchanges: info: binary-only upload (no source code included)
 dpkg-source -i --after-build .
dpkg-buildpackage: info: binary-only upload (no source included)
/home/vitex
-rw-r--r-- 1 vitex vitex 22M čec 24 15:43 /home/vitex/crio_1627134198_all.deb
```

Now you can transfer resutlting package into remote system to install using **dpkg** or **gdebi**:




Installation
------------

```shell
sudo apt install lsb-release wget apt-transport-https bzip2

sudo wget -O /usr/share/keyrings/vitexsoftware.gpg https://repo.vitexsoftware.cz/keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/vitexsoftware.gpg]  https://repo.vitexsoftware.cz  $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/vitexsoftware.list
sudo apt update

sudo apt install debs2deb
```
