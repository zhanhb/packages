include $(TOPDIR)/rules.mk

PKG_NAME:=cidr-merger
PKG_VERSION:=0.1
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=https://repo.martian.tk/openwrt/cidr-merger-c.git
PKG_SOURCE_VERSION:=v$(PKG_VERSION)
PKG_MIRROR_HASH:=1c5ca435bebe7592dfdec33203b7a3ad3d77b3bd5751f935a2557f144abbaf7e

CMAKE_INSTALL:=1

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/cidr-merger
  SECTION:=utils
  CATEGORY:=Utilities
  URL:=https://repo.martian.tk/openwrt/cidr-merger-c
  TITLE:=cidr-merger
endef

Package/cidr-merger/install = $(Build/InstallDev/cmake)

$(eval $(call HostBuild))
$(eval $(call BuildPackage,cidr-merger))
