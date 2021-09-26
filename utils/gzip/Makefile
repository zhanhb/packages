#
# Copyright (C) 2006-2016 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=gzip
PKG_VERSION:=1.12
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@GNU/gzip
PKG_HASH:=ce5e03e519f637e1f814011ace35c4f87b33c0bbabeec35baf5fbd3479e91956
PKG_LICENSE:=GPL-3.0-or-later
PKG_CPE_ID:=cpe:/a:gnu:gzip

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/gzip/Default
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=Compression
  URL:=https://www.gnu.org/software/gzip/
  MAINTAINER:=Christian Beier <dontmind@freeshell.org>
endef

define Package/gzip
  $(call Package/gzip/Default)
  TITLE:=gzip (GNU zip) is a compression utility.
  DEPENDS:=
  ALTERNATIVES:=\
    300:/bin/gunzip:/usr/libexec/gunzip-gnu \
    300:/bin/gzip:/usr/libexec/gzip-gnu \
    300:/bin/zcat:/usr/libexec/zcat-gnu
endef

define Package/gzip/description
	gzip (GNU zip) is a compression utility designed to be a \
	replacement for compress.
endef

define Package/zdiff
  $(call Package/gzip/Default)
  TITLE:=GNU zip zcmp/zdiff utility.
  DEPENDS:=+diffutils +gzip
endef

define Package/zdiff/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/{zcmp,zdiff} $(1)/usr/bin
endef

define Package/zless
  $(call Package/gzip/Default)
  TITLE:=GNU zip zless utility.
  DEPENDS:=+gzip +less
endef

define Package/zless/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/zless $(1)/usr/bin
endef

define Package/zmore
  $(call Package/gzip/Default)
  TITLE:=GNU zip zmore utility.
  DEPENDS:=+gzip +more
endef

define Package/zmore/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/zmore $(1)/usr/bin
endef

CONFIGURE_VARS += \
	gl_cv_func_getopt_gnu=yes \
	ac_cv_path_GREP=/bin/grep \
	ac_cv_search_clock_gettime=no

define Package/gzip/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/{gzexe,zegrep,zfgrep,zforce,zgrep,znew} $(1)/usr/bin
	$(INSTALL_DIR) $(1)/usr/libexec
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/gunzip $(1)/usr/libexec/gunzip-gnu
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/gzip $(1)/usr/libexec/gzip-gnu
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/zcat $(1)/usr/libexec/zcat-gnu
endef

$(eval $(call BuildPackage,gzip))
$(eval $(call BuildPackage,zdiff))
$(eval $(call BuildPackage,zless))
$(eval $(call BuildPackage,zmore))
