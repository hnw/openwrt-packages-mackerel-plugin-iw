# openwrt-packages-mackerel-agent-iw

This is `mackerel-agent-iw` package for OpenWrt 15.05.1 / LEDE 17.01.3

# How to install binary package

Download appropriate package for the architecture of your target machine from "[Releases](https://github.com/hnw/openwrt-packages-mackerel-agent/releases)" and copy the package to the target machine.

For example:

```
$ wget https://github.com/hnw/openwrt-packages-mackerel-agent/releases/download/0.45.0-2/lede-17.01.2-ar71xx-mackerel-agent_0.45.0-2_mips_24kc.ipk
$ scp lede-17.01.2-ar71xx-mackerel-agent_0.45.0-2_mips_24kc.ipk lede:/tmp
$ ssh lede
# opkg update
# opkg install /tmp/lede-17.01.2-ar71xx-mackerel-agent_0.45.0-2_mips_24kc.ipk
```

# How to build

To build these packages, add the following line to the feeds.conf in the OpenWrt buildroot:

```
$ echo 'src-git hnw_mackerel-agent https://github.com/hnw/openwrt-packages-mackerel-agent.git' >> feeds.conf
$ echo 'src-git hnw_mackerel-agent-iw https://github.com/hnw/openwrt-packages-mackerel-agent-iw.git' >> feeds.conf
```

Then you can build packages as follows:

```
$ ./scripts/feeds update -a
$ ./scripts/feeds install mackerel-agent
$ ./scripts/feeds install mackerel-agent-iw
$ make packages/mackerel-agent-iw/compile
```
