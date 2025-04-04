#
# This is free software, licensed under the Apache License, Version 2.0 .
#

include $(TOPDIR)/rules.mk

LUCI_TITLE:=LuCI based ipk store
LUCI_DESCRIPTION:=luci-app-store is a ipk store developed by LinkEase team
LUCI_DEPENDS:=@(x86_64||aarch64) +curl +opkg +luci-lib-ipkg +tar +libuci-lua +mount-utils +luci-lib-taskd
LUCI_EXTRA_DEPENDS:=luci-lib-taskd (>=1.0.19)
LUCI_PKGARCH:=all

# 修改点1：分离版本号和修订号
PKG_VERSION:=0.1.27   # 上游版本号（仅含主/次版本）
PKG_RELEASE:=4        # 包修订号（避免使用连字符）

ISTORE_UI_VERSION:=0.1.27
ISTORE_UI_RELEASE:=2
PKG_HASH:=skip

PKG_SOURCE_URL_FILE:=v$(ISTORE_UI_VERSION)-$(ISTORE_UI_RELEASE).tar.gz
PKG_SOURCE:=istore-ui-$(PKG_SOURCE_URL_FILE)
PKG_SOURCE_URL:=https://github.com/linkease/istore-ui/archive/refs/tags

PKG_MAINTAINER:=jjm2473 <jjm2473@gmail.com>

TARGET_CONFIGURE_OPTS= FRONTEND_DIST="$(BUILD_DIR)/istore-ui-$(ISTORE_UI_VERSION)-$(ISTORE_UI_RELEASE)/app-store-ui/src/dist" APP_STORE_VERSION="$(PKG_VERSION)"
TARGET_CONFIGURE_OPTS+= SED="$(SED)"

define Package/luci-app-store/conffiles
/etc/.app_store.id
/etc/config/istore
endef

# 修改点2：定义 Package 时组合版本号
define Package/luci-app-store
  SECTION:=luci
  CATEGORY:=LuCI
  TITLE:=LuCI support for store
  VERSION:=$(PKG_VERSION)-$(PKG_RELEASE)  # 正确格式：主版本-修订号
  DEPENDS:=$(LUCI_DEPENDS)
endef

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
