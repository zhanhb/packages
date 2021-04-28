#
# Copyright (C) 2006-2010 OpenWrt.org
# Copyright (C) 2016 Stijn Segers
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=net-tools
PKG_VERSION:=2.10
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://sourceforge.net/projects/net-tools/files/
PKG_HASH:=b262435a5241e89bfa51c3cabd5133753952f7a7b7b93f32e08cb9d96f580d69

PKG_MAINTAINER:=Stijn Segers <borromini.reg@protonmail.com>
PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING

include $(INCLUDE_DIR)/package.mk

define Package/net-tools/Default
  SECTION:=net
  CATEGORY:=Network
  URL:=http://net-tools.sourceforge.net/
endef

define Package/mii-tool
  $(call Package/net-tools/Default)
  TITLE:=configure media type using MII commands
endef

define Package/mii-tool/description
 The mii-tool command allows you to set or autodetect the media type
 or mii chipset-based ethernet devices. It traditionally had been
 distributed in the net-tools package. This is a single distribution
 optimized for embedded systems and fully automated cross/-sysroot-builds
endef

define Package/hostname
  $(call Package/net-tools/Default)
  TITLE:=Utility to set/show the host name or domain name
endef

define Package/hostname/description
 This package provides commands which can be used to display the system's
 DNS name, and to display or set its hostname or NIS domain name.
endef

# Remove hostname mii-tool from NET_TOOLS_APPLETS which is already defined
NET_TOOLS_APPLETS := \
    arp ifconfig ipmaddr iptunnel \
    nameif netstat plipconfig rarp route slattach

DIR_BIN := netstat
DIR_SBIN := arp ifconfig iptunnel nameif route slattach

# hostname ipmaddr mii-tool plipconfig rarp
DIR_OTHERS := $(filter-out $(DIR_BIN) $(DIR_SBIN),$(NET_TOOLS_APPLETS))

$(eval $(foreach a,$(DIR_BIN),ALTS_$(a):=300:/bin/$(a):/usr/libexec/$(a)-net-tools$(newline)))
$(eval $(foreach a,$(DIR_SBIN),ALTS_$(a):=300:/sbin/$(a):/usr/libexec/$(a)-net-tools$(newline)))

define Package/net-tools
  $(call Package/net-tools/Default)
  DEPENDS:=+hostname +mii-tool $(NET_TOOLS_APPLETS:%=+net-tools-%)
  TITLE:=Basic networking tools
  MENU:=1
endef

define Package/net-tools/description
 The net-tools package contains basic networking tools,
 including ifconfig, netstat, route, and others.
 Most of them are obsolete. For replacement check iproute package.
endef

define Package/net-tools/description/Default-busybox
 Replace busybox version of the $(1) command with the full net-tools
 version. This is normally not needed as busybox is smaller and provides
 sufficient functionality, but some users may want or need the full
 functionality of the net-tools variant (e.g. AF_X25).
endef

define Package/net-tools/description/Default
 net-tools - $(1) utility
endef

define GenPlugin
 define Package/net-tools-$(1)
   $$(call Package/net-tools/Default)
   TITLE:=net-tools - $(1) utility
   PROVIDES:=$(1)
   ALTERNATIVES:=$$(ALTS_$(1))
 endef

 Package/net-tools-$(1)/description=$$(call Package/net-tools/description/Default$$(if $$(ALTS_$(1)),-busybox),$(1))
endef

$(foreach a,$(NET_TOOLS_APPLETS),$(eval $(call GenPlugin,$(a))))

define Build/Configure
	# Failed configure.sh leaves stub config.h around.
	rm -f $(PKG_BUILD_DIR)/config.h
	( cd $(PKG_BUILD_DIR); yes '' | ./configure.sh config.in )
endef

define Package/net-tools/install
	true
endef

define Package/mii-tool/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/mii-tool $(1)/usr/sbin/
endef

hostnameprogs := dnsdomainname domainname nisdomainname ypdomainname

define Package/hostname/install
	$(INSTALL_DIR) $(1)/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hostname $(1)/bin
	$(foreach prog,$(hostnameprogs),$(LN) hostname $(1)/bin/$(prog);)
endef

define BuildPlugin
  define Package/net-tools-$(1)/install
	$$(INSTALL_DIR) $$(1)$(if $(ALTS_$(1)),/usr/libexec,/usr/sbin)
	$$(INSTALL_BIN) $$(PKG_BUILD_DIR)/$(1) $$(1)$(if $(ALTS_$(1)),/usr/libexec/$(1)-net-tools,/usr/sbin/$(1))
  endef

  $$(eval $$(call BuildPackage,net-tools-$(1)))
endef

$(eval $(call BuildPackage,mii-tool))
$(eval $(call BuildPackage,hostname))
$(foreach a,$(NET_TOOLS_APPLETS),$(eval $(call BuildPlugin,$(a))))
$(eval $(call BuildPackage,net-tools))
