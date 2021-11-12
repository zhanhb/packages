# Copyright 2017-2018 Stan Grishin (stangri@melmac.net)
# This is free software, licensed under the GNU General Public License v3.

include $(TOPDIR)/rules.mk

PKG_NAME:=vpnbypass
PKG_VERSION:=1.3.2
PKG_RELEASE:=$(AUTORELEASE)
PKG_LICENSE:=GPL-3.0-or-later
PKG_MAINTAINER:=Stan Grishin <stangri@melmac.net>

include $(INCLUDE_DIR)/package.mk

define Package/vpnbypass
	SECTION:=net
	CATEGORY:=Network
	TITLE:=VPN Bypass Service
	URL:=https://docs.openwrt.melmac.net/vpnbypass/
	DEPENDS:=+ipset +iptables
	PKGARCH:=all
endef

define Package/vpnbypass/description
This service can be used to enable simple VPN split tunnelling.
Supports accessing domains, IP ranges outside of your VPN tunnel.
Also supports dedicating local ports/IP ranges for direct
internet access (outside of your VPN tunnel).
Please see the README for further information.
endef

define Package/vpnbypass/conffiles
/etc/config/vpnbypass
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/vpnbypass/install
	$(INSTALL_DIR) $(1)/etc/init.d $(1)/etc/config $(1)/etc/hotplug.d/firewall
	$(INSTALL_BIN) ./files/vpnbypass.init $(1)/etc/init.d/vpnbypass
	$(SED) "s|^\(PKG_VERSION\).*|\1='$(PKG_VERSION)-$(PKG_RELEASE)'|" $(1)/etc/init.d/vpnbypass
	$(INSTALL_CONF) ./files/vpnbypass.config $(1)/etc/config/vpnbypass
	$(INSTALL_DATA) ./files/vpnbypass.hotplug $(1)/etc/hotplug.d/firewall/94-vpnbypass
endef

$(eval $(call BuildPackage,vpnbypass))
