#
# Copyright (C) 2006-2015 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=screen
PKG_VERSION:=4.9.0
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@GNU/screen
PKG_HASH:=f9335281bb4d1538ed078df78a20c2f39d3af9a4e91c57d084271e0289c730f4

PKG_MAINTAINER:=Etienne CHAMPETIER <champetier.etienne@gmail.com>
PKG_LICENSE:=GPL-3.0-or-later
PKG_LICENSE_FILES:=COPYING
PKG_CPE_ID:=cpe:/a:gnu:screen

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/screen
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Terminal
  DEPENDS:=+libncurses
  TITLE:=Full-screen terminal window manager
  URL:=https://www.gnu.org/software/screen/
endef

define Package/screen/description
	Screen is a full-screen window manager that multiplexes a physical
	terminal between several processes, typically interactive shells.
endef

CONFIGURE_ARGS += \
	--enable-colors256 \
	--with-sys-screenrc=/etc/screenrc

define Package/screen/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/screen $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_DATA) ./files/etc/screenrc $(1)/etc/screenrc
endef

define Package/screen/conffiles
/etc/screenrc
endef

$(eval $(call BuildPackage,screen))
