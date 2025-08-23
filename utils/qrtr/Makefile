#
# Copyright (C) 2020-2021 HandsomeMod Project
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=qrtr
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/andersson/qrtr.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_VERSION:=9dc7a88548c27983e06465d3fbba2ba27d4bc050
PKG_MIRROR_HASH:=0de3e2200bc6f2ecc45cd16d6413b9426b15dc00acf14b66ed3884701da232d6

PKG_LICENSE:=BSD-3-Clause

include $(INCLUDE_DIR)/package.mk

define Package/libqrtr
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Userspace reference for net/qrtr in the Linux kernel
endef

define Package/qrtr-ns
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=+libqrtr
  TITLE:=qrtr daemon
endef

define Build/Compile
	$(call Build/Compile/Default,prefix=/usr all)
endef

define Build/Install
	$(call Build/Install/Default,prefix=/usr DESTDIR="$(PKG_INSTALL_DIR)" install)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/libqrtr.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef


define Package/libqrtr/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/* $(1)/usr/lib/
endef

define Package/qrtr-ns/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/qrtr.init $(1)/etc/init.d/qrtr

	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/qrtr-* $(1)/usr/bin/
endef

$(eval $(call BuildPackage,libqrtr))
$(eval $(call BuildPackage,qrtr-ns))
