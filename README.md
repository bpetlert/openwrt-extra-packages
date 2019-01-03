# OpenWrt extra packages feed

## Description

This is the extra packags feed for OpenWrt.

## How to use

Add the following line to the feeds.conf.default in the OpenWrt buildroot:

`src-git extra https://github.com/bpetlert/openwrt-extra-packages.git`

And run update the feed:

`./scripts/feeds update extra`

And activate the specific package:

`./scripts/feeds install PACKAGE_NAME`

Or activate all packages from extra feed:

`./scripts/feeds install -a -p extra`

Activated package(s) should now appear in menuconfig.

## Example

This example shows how to build 'pdnsd' package using [OpenWrt SDK 18.06](https://downloads.openwrt.org/releases/18.06.1/targets/mvebu/cortexa9/) for [Linksys WRT1900AC v2](https://openwrt.org/toh/hwdata/linksys/linksys_wrt1900ac_v2).

```bash
export SDK=openwrt-sdk-18.06.1-mvebu-cortexa9_gcc-7.3.0_musl_eabi.Linux-x86_64

wget -c https://downloads.openwrt.org/releases/18.06.1/targets/mvebu/cortexa9/sha256sums
wget -c https://downloads.openwrt.org/releases/18.06.1/targets/mvebu/cortexa9/$SDK.tar.xz
wget -c https://downloads.openwrt.org/releases/18.06.1/targets/mvebu/cortexa9/config.seed

sha256sum --check --ignore-missing sha256sums

tar xf $SDK.tar.xz

cp config.seed $SDK/.config

cd $SDK
echo "src-git extra https://github.com/bpetlert/openwrt-extra-packages.git" >> feeds.conf.default

# Update feed 'extra'
LC_ALL=C ./scripts/feeds update extra

# Activate 'pdnsd' package from extra feed
LC_ALL=C ./scripts/feeds install pdnsd

# Build pdnsd package
make package/pdnsd/compile
```

## Packages

- [pdnsd](http://members.home.nl/p.a.rombouts/pdnsd/)
- [empty](http://empty.sourceforge.net/)
