# Copyright (C) 2020 Lienol <lawlienol@gmail.com>
#
# This is free software, licensed under the GNU General Public License v3.
#

###include $(TOPDIR)/rules.mk

###PKG_NAME:=luci-app-socat

###PKG_MAINTAINER:=Lienol <lawlienol@gmail.com>

###LUCI_TITLE:=LuCI support for Socat
###LUCI_DEPENDS:=+socat
###LUCI_PKGARCH:=all

###define Package/$(PKG_NAME)/conffiles
###/etc/config/socat
###endef

###include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature

#----------以上原有，恢复时取消“###”，以下修改后的---------------#
# Copyright (C) 2020 Lienol <lawlienol@gmail.com>
#
# This is free software, licensed under the GNU General Public License v3.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-socat

PKG_MAINTAINER:=Lienol <lawlienol@gmail.com>

LUCI_TITLE:=LuCI support for Socat
LUCI_DEPENDS:=+socat       # 声明依赖 socat 包（但需避免文件覆盖）
LUCI_PKGARCH:=all

define Package/$(PKG_NAME)/conffiles
/etc/config/socat          # 声明配置文件（需确保不会与 socat 包冲突）
endef

# 自定义安装逻辑（核心修改点）
define Package/$(PKG_NAME)/install
    # 创建 /etc/config 目录（若不存在）
    $(INSTALL_DIR) $(1)/etc/config

    # 关键修复：仅在目标文件不存在时安装配置文件
    # 避免覆盖 socat 包已有的 /etc/config/socat 文件
    if [ ! -f $(1)/etc/config/socat ]; then \
        $(INSTALL_CONF) ./files/socat.config $(1)/etc/config/socat; \
        echo "Installed new socat.config"; \
    else \
        echo "Skipped existing socat.config to avoid conflict"; \
    fi

    # 安装 LuCI 相关文件（保持原有逻辑）
    $(INSTALL_DIR) $(1)/usr/lib/lua/luci/controller
    $(INSTALL_DATA) ./luasrc/controller/socat.lua $(1)/usr/lib/lua/luci/controller/
    
    $(INSTALL_DIR) $(1)/usr/lib/lua/luci/model/cbi
    $(INSTALL_DATA) ./luasrc/model/cbi/socat.lua $(1)/usr/lib/lua/luci/model/cbi/
    
    $(INSTALL_DIR) $(1)/usr/lib/lua/luci/view/socat
    $(INSTALL_DATA) ./luasrc/view/socat.htm $(1)/usr/lib/lua/luci/view/socat/
endef

include $(TOPDIR)/feeds/luci/luci.mk
