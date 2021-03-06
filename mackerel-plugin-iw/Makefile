include $(TOPDIR)/rules.mk

PKG_NAME:=mackerel-plugin-iw
PKG_VERSION:=0.1.1
PKG_RELEASE:=3

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=v$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/hnw/mackerel-plugin-iw/archive/
PKG_MD5SUM:=480732e837397b8442cd70eeeb3e6870

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1
PKG_USE_MIPS16:=0

PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Yoshio HANAWA <for-openwrt@hnw.jp>

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=admin
  CATEGORY:=Administration
  TITLE:=iw custom metrics plugin for mackerel-agent
  URL:=https://github.com/hnw/mackerel-plugin-iw
  DEPENDS:=+mackerel-agent
endef

define Package/$(PKG_NAME)/description
  iw custom metrics plugin for mackerel-agent
endef

# golang cross-compile architecture (GOARCH)
GOARCH:=

# golang soft-float support (GOARM/GOMIPS)
GOSOFTFLOAT:=

# set GOARCH and GOARM/GOMIPS by $(ARCH)
ifeq ($(ARCH),mips)		# for MIPS big-endianess SoC
  GOARCH:=mips
  GOSOFTFLOAT:=GOMIPS=softfloat
endif
ifeq ($(ARCH),mipsel)		# for MIPS little-endianess SoC
  GOARCH:=mipsle
  GOSOFTFLOAT:=GOMIPS=softfloat
endif
ifeq ($(ARCH),mips64)		# for MIPS64 big-endianess SoC
  GOARCH:=mips64
  GOSOFTFLOAT:=GOMIPS=softfloat
endif
ifeq ($(ARCH),arm)		# for ARM SoC
  GOARCH:=arm
  GOSOFTFLOAT:=GOARM=5
endif
ifeq ($(ARCH),i386)		# for x86 (i386) SoC/CPU
  GOARCH:=386
endif
ifeq ($(ARCH),x86_64)		# for x86_64 (amd64) SoC/CPU
  GOARCH:=amd64
endif

CROSS_COMPILE_GOENVS:=GOOS=linux GOARCH=$(GOARCH) $(GOSOFTFLOAT)
GO_LDFLAGS:=-ldflags="-s -w"

define Build/Configure
	true
endef

define Build/Compile
	cd $(PKG_BUILD_DIR) && go get -d -v ./... && $(CROSS_COMPILE_GOENVS) go build $(GO_LDFLAGS) -o build/$(PKG_NAME)
	upx --best $(PKG_BUILD_DIR)/build/$(PKG_NAME)
endef

define Build/Install
	true
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/build/$(PKG_NAME) $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/mackerel-agent
	$(INSTALL_CONF) ./files/$(PKG_NAME).conf $(1)/etc/mackerel-agent/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
