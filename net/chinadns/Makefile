#
# Copyright (C) 2014-2018 OpenWrt-dist
# Copyright (C) 2014-2018 Jian Chang <aa65535@live.com>
#
# This is free software, licensed under the GNU General Public License v3.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=chinadns
PKG_VERSION:=1.3.3
PKG_RELEASE:=$(AUTORELEASE)

PKG_SRC_NAME:=ChinaDNS
PKG_SRC_VERSION:=00616680114011553881760e843b77a3519e8fbf
PKG_SOURCE:=$(PKG_SRC_NAME)-$(PKG_SRC_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/aa65535/$(PKG_SRC_NAME)/tar.gz/$(PKG_SRC_VERSION)?
PKG_HASH:=43852dd8910dc7fdabfdccf9b326ad01fbe4e45120d23cf3842da3f9cbf32580
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SRC_NAME)-$(PKG_SRC_VERSION)

PKG_LICENSE:=GPLv3
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=Jian Chang <aa65535@live.com>

PKG_INSTALL:=1
PKG_BUILD_DEPENDS:=cidr-merger/host
PKG_FIXUP:=autoreconf
PKG_USE_MIPS16:=0
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/chinadns
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Protect yourself against DNS poisoning in China.
  URL:=https://github.com/shadowsocks/ChinaDNS
endef

define Package/chinadns/description
Protect yourself against DNS poisoning in China.
endef

define Package/chinadns/conffiles
/etc/config/chinadns
/etc/chinadns_chnroute.txt
endef

define download_chnroute
	url="https://ftp.apnic.net/stats/apnic/`TZ=UTC date +%Y`/delegated-apnic-`TZ=UTC+24 date +%Y%m%d`.gz"; \
	if command -v curl >/dev/null; then curl -sSL "$$$$url"; else wget -qO- "$$$$url"; fi | \
		gzip -d | awk -F\| '!/^\s*(#.*)?$$$$/&&/CN\|ipv4/{print $$$$4 "/" 32-log($$$$5)/log(2)}' | \
		cidr-merger -eo '$(PKG_BUILD_DIR)/chnroute.txt'
endef

Hooks/Compile/Post+=download_chnroute

define Package/chinadns/install
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_DATA) ./files/chinadns.config $(1)/etc/config/chinadns
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/chinadns.init $(1)/etc/init.d/chinadns
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/chnroute.txt $(1)/etc/chinadns_chnroute.txt
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/chinadns $(1)/usr/bin/
endef

$(eval $(call BuildPackage,chinadns))
