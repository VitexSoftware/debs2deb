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
Package contains als /etc/apt/sources.list.d/PACKNAME.list for easy installation of packages


Installation
------------

```shell
sudo apt install lsb-release wget apt-transport-https bzip2

sudo wget -O /usr/share/keyrings/vitexsoftware.gpg https://repo.vitexsoftware.cz/keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/vitexsoftware.gpg]  https://repo.vitexsoftware.cz  $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/vitexsoftware.list
sudo apt update

sudo apt install debs2deb
```
