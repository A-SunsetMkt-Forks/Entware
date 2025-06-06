include $(TOPDIR)/rules.mk

PKG_NAME:=libunistring
PKG_VERSION:=1.2
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=@GNU/$(PKG_NAME)
PKG_HASH:=632bd65ed74a881ca8a0309a1001c428bd1cbd5cd7ddbf8cedcd2e65f4dcdc44

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILES:=COPYING
PKG_CPE_ID:=cpe:/a:gnu:$(PKG_NAME)

HOST_BUILD_DEPENDS:=libiconv-full/host

include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/package.mk

define Package/libunistring
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=libunistring
  URL:=https://www.gnu.org/software/libunistring
endef

define Package/libunistring/description
  This library provides functions for manipulating Unicode strings
  and for manipulating C strings according to the Unicode standard.
endef

HOST_CFLAGS += $(HOST_FPIC)

TARGET_CFLAGS += $(FPIC)

HOST_CONFIGURE_ARGS += \
	--enable-static \
	--disable-shared \
	--without-libiconv-prefix \
	--with-pic

CONFIGURE_ARGS += \
	--enable-static \
	--enable-shared \
	--without-libiconv-prefix \
	--with-pic

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/*.h $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/include/unistring
	$(CP) $(PKG_INSTALL_DIR)/opt/include/unistring/*.h $(1)/opt/include/unistring/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libunistring.{a,so*} $(1)/opt/lib/
endef

define Package/libunistring/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libunistring.so.* $(1)/opt/lib/
endef

$(eval $(call HostBuild))
$(eval $(call BuildPackage,libunistring))
