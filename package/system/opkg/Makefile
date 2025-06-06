# SPDX-License-Identifier: GPL-2.0-or-later
#
# Copyright (C) 2006-2021 OpenWrt.org
#
# Entware specific: static linkage against libubox, opkg upgrade (all) support
# no MENU, no DEPENDS

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=opkg
PKG_RELEASE:=1
#PKG_FLAGS:=essential

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL=$(PROJECT_GIT)/project/opkg-lede.git
PKG_SOURCE_DATE:=2024-10-16
PKG_SOURCE_VERSION:=38eccbb1fd694d4798ac1baf88f9ba83d1eac616
PKG_MIRROR_HASH:=de58ff1c99c14789f9ba8946623c8c1e58d022e7e2a659d6f97c6fde54f2c4f4

PKG_LICENSE:=GPL-2.0
PKG_LICENSE_FILES:=COPYING

PKG_MAINTAINER:=Jo-Philipp Wich <jo@mein.io>

# Extend depends from version.mk
PKG_CONFIG_DEPENDS += \
	CONFIG_SIGNATURE_CHECK \
	CONFIG_TARGET_INIT_PATH

HOST_BUILD_DEPENDS:=libubox/host
PKG_BUILD_DEPENDS:=libubox

PKG_BUILD_FLAGS:=gc-sections

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/host-build.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/opkg
  SECTION:=base
  CATEGORY:=Base system
  TITLE:=opkg package manager
  DEFAULT:=y if !USE_APK
  URL:=$(PKG_SOURCE_URL)
  PKG_DEFAULT_DEPENDS:=
endef

define Package/opkg/description
  Lightweight package management system
  opkg is the opkg Package Management System, for handling
  installation and removal of packages on a system. It can
  recursively follow dependencies and download all packages
  necessary to install a particular package.

  opkg knows how to install both .ipk and .deb packages.
endef

#define Package/opkg/conffiles
#/etc/opkg.conf
#/etc/opkg/keys/
#/etc/opkg/customfeeds.conf
#endef

TARGET_CFLAGS += -D_LARGEFILE_SOURCE -D_LARGEFILE64_SOURCE -D_FILE_OFFSET_BITS=64
EXTRA_CFLAGS += $(TARGET_CPPFLAGS)

CMAKE_OPTIONS += \
	-DSTATIC=ON \
	-DSTATIC_UBOX=ON \
	-DBUILD_TESTS=OFF \
	-DHOST_CPU=$(PKGARCH) \
	-DLOCK_FILE=/opt/tmp/opkg.lock \
	-DPATH_SPEC="$(TARGET_INIT_PATH)" \
	-DVERSION="$(PKG_SOURCE_VERSION) ($(PKG_SOURCE_DATE))"

CMAKE_HOST_OPTIONS += \
	-DSTATIC_UBOX=ON \
	-DBUILD_TESTS=OFF \
	-DHOST_CPU=$(PKGARCH) \
	-DLOCK_FILE=/tmp/opkg.lock \
	-DVERSION="$(PKG_SOURCE_VERSION) ($(PKG_SOURCE_DATE))"

define Package/opkg/install
#	$(INSTALL_DIR) $(1)/usr/lib/opkg
	$(INSTALL_DIR) $(1)/opt/bin
#	$(INSTALL_DIR) $(1)/etc/opkg
#	$(INSTALL_DIR) $(1)/etc/uci-defaults
#	$(INSTALL_DATA) ./files/customfeeds.conf $(1)/etc/opkg/customfeeds.conf
#	$(INSTALL_DATA) ./files/opkg$(2).conf $(1)/etc/opkg.conf
#	$(INSTALL_BIN) ./files/20_migrate-feeds $(1)/etc/uci-defaults/
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/opkg-cl $(1)/opt/bin/opkg
#  ifneq ($(CONFIG_SIGNATURE_CHECK),)
#	echo "option check_signature" >> $(1)/etc/opkg.conf
#  endif
#	$(INSTALL_DIR) $(1)/usr/sbin
#	$(INSTALL_BIN) ./files/opkg-key $(1)/usr/sbin/
endef

define Host/Install
	$(INSTALL_BIN) $(HOST_BUILD_DIR)/src/opkg-cl $(STAGING_DIR_HOST)/bin/opkg
endef

$(eval $(call BuildPackage,opkg))
$(eval $(call HostBuild))
