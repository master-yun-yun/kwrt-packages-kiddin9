# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2021-2023 ImmortalWrt.org

include $(TOPDIR)/rules.mk

PKG_NAME:=gmediarender
PKG_RELEASE=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/hzeller/gmrender-resurrect.git
PKG_SOURCE_DATE:=2023-07-16
PKG_SOURCE_VERSION:=c26c5cdbc5ef3d0d0f24e6542dfdf35729a0bb9b
PKG_MIRROR_HASH:=skip

PKG_FIXUP:=autoreconf
PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/gmediarender
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=Resource efficient UPnP/DLNA renderer
  DEPENDS:=+glib2 +gstreamer1 +gstreamer1-utils +gst1-plugins-base \
    +gst1-plugins-bad +gst1-plugins-good +libupnp
endef

define Package/gmediarender/description
  gmediarender implements the server component that provides UPnP
  controllers a means to render media content (audio, video and images)
  from a UPnP media server.
endef

define Package/gmediarender/config
	select PACKAGE_gstreamer1-plugins-bad
	select PACKAGE_gstreamer1-plugins-good
endef

define Package/gmediarender/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/gmediarender $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/usr/share/gmediarender
	$(INSTALL_DATA) $(PKG_INSTALL_DIR)/usr/share/gmediarender/grender-*.png $(1)/usr/share/gmediarender/
endef

$(eval $(call BuildPackage,gmediarender))
