# Copyright 2017-2018 Stan Grishin (stangri@melmac.net)
# This is free software, licensed under the GNU General Public License v3.

include $(TOPDIR)/rules.mk

PKG_NAME:=vpn-policy-routing
PKG_VERSION:=0.3.4
PKG_RELEASE:=9
PKG_LICENSE:=GPL-3.0-or-later
PKG_MAINTAINER:=Stan Grishin <stangri@melmac.net>

include $(INCLUDE_DIR)/package.mk

define Package/vpn-policy-routing
	SECTION:=net
	CATEGORY:=Network
	TITLE:=VPN Policy-Based Routing Service
	URL:=https://docs.openwrt.melmac.net/vpn-policy-routing/
	DEPENDS:=+jshn +ipset +iptables +resolveip +kmod-ipt-ipset +iptables-mod-ipopt +ip-full
	PKGARCH:=all
endef

define Package/vpn-policy-routing/description
This service allows policy-based routing for L2TP, Openconnect, OpenVPN, PPTP and Wireguard tunnels and WAN interface.
Policies can specify domains, local IPs/subnets and ports, as well as remote IPs/subnets and ports.
endef

define Package/vpn-policy-routing/conffiles
/etc/config/vpn-policy-routing
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/vpn-policy-routing/install
	$(INSTALL_DIR) $(1)/etc/init.d $(1)/etc/config $(1)/etc/hotplug.d/firewall $(1)/etc/
	$(INSTALL_BIN) ./files/vpn-policy-routing.init $(1)/etc/init.d/vpn-policy-routing
	$(SED) "s|^\(PKG_VERSION\).*|\1='$(PKG_VERSION)-$(PKG_RELEASE)'|" $(1)/etc/init.d/vpn-policy-routing
	$(INSTALL_CONF) ./files/vpn-policy-routing.config $(1)/etc/config/vpn-policy-routing
	$(INSTALL_DATA) ./files/vpn-policy-routing.firewall.hotplug $(1)/etc/hotplug.d/firewall/70-vpn-policy-routing
	$(INSTALL_DATA) ./files/vpn-policy-routing.aws.user $(1)/etc/vpn-policy-routing.aws.user
	$(INSTALL_DATA) ./files/vpn-policy-routing.netflix.user $(1)/etc/vpn-policy-routing.netflix.user
endef

$(eval $(call BuildPackage,vpn-policy-routing))
