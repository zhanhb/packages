#
# Copyright (c) 2021 Gregory L. Dietsche <Gregory.Dietsche@cuw.edu>
# This is free software, licensed under the MIT License
#

include $(TOPDIR)/rules.mk

PKG_NAME:=safe-search
PKG_VERSION:=3.0.0
PKG_RELEASE:=$(AUTORELEASE)
PKG_LICENSE:=MIT
PKG_MAINTAINER:=Gregory L. Dietsche <Gregory.Dietsche@cuw.edu>

include $(INCLUDE_DIR)/package.mk

define Package/safe-search
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Safe Search
  PKGARCH:=all
endef

define Package/safe-search/description
This package prevents adult content from appearing in search results by
configuring dnsmasq to force all devices on your network to use Google and
Bing's Safe Search IP addresses. This is designed to be approperiate for most
businesses and families. The default filtering rules do not interfere with
normal web browsing.
endef

define Package/safe-search/conffiles
/etc/config/safe-search
endef

define Build/Compile
endef

define Package/safe-search/install
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/safe-search.conf $(1)/etc/config/safe-search

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/safe-search.init $(1)/etc/init.d/safe-search

	$(INSTALL_DIR) $(1)/etc/safe-search/domains
	$(INSTALL_DATA) files/domains/* $(1)/etc/safe-search/domains/

	$(INSTALL_DIR) $(1)/etc/safe-search/provider
	$(INSTALL_DATA) files/provider/* $(1)/etc/safe-search/provider/
endef

define Package/safe-search/postrm
#!/bin/sh
rmdir "$$IPKG_INSTROOT/etc/safe-search/domains"
rmdir "$$IPKG_INSTROOT/etc/safe-search/provider"
rmdir "$$IPKG_INSTROOT/etc/safe-search/"
exit 0
endef

$(eval $(call BuildPackage,safe-search))
