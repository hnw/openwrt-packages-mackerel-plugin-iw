# openwrt-packages-mackerel-plugin-iw [![Build Status](https://secure.travis-ci.org/hnw/openwrt-packages-mackerel-plugin-iw.svg?branch=master)](https://travis-ci.org/hnw/openwrt-packages-mackerel-plugin-iw)

This is [mackerel-plugin-iw](https://github.com/hnw/mackerel-plugin-iw/) package for OpenWrt, tested on OpenWrt 15.05.1 / LEDE 17.01.4.

# How to install binary package

```
$ opkg install mackerel-plugin-iw
$ /etc/init.d/mackerel-agent stop
$ /etc/init.d/mackerel-agent start
```

See Also [hnw/openwrt-packages](https://github.com/hnw/openwrt-packages).

# How to build

To build these packages, add the following line to the feeds.conf in the OpenWrt buildroot:

```
$ echo 'src-git hnw_mackerel-plugin-iw https://github.com/hnw/openwrt-packages-mackerel-plugin-iw.git' >> feeds.conf
```

Then you can build packages as follows:

```
$ ./scripts/feeds update -a
$ ./scripts/feeds install mackerel-plugin-iw
$ make packages/mackerel-plugin-iw/compile
```
