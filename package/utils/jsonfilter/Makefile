include $(TOPDIR)/rules.mk

PKG_NAME:=jsonfilter
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=$(PROJECT_GIT)/project/jsonpath.git
PKG_SOURCE_DATE:=2025-04-18
PKG_SOURCE_VERSION:=8a86fb78235b5d7925b762b7b0934517890cc034
PKG_MIRROR_HASH:=06b763387d00faae0e62af68626588ff2b8f12e0e6821950ae5422033df32757
CMAKE_INSTALL:=1

PKG_MAINTAINER:=Jo-Philipp Wich <jo@mein.io>
PKG_LICENSE:=ISC

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/jsonfilter
  SECTION:=base
  CATEGORY:=Base system
  DEPENDS:=+libubox +libjson-c
  TITLE:=OpenWrt JSON filter utility
  URL:=$(PKG_SOURCE_URL)
endef

define Package/jsonfilter/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/jsonpath $(1)/opt/bin/jsonfilter
endef

$(eval $(call BuildPackage,jsonfilter))
