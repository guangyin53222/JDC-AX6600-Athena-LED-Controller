#
# Copyright (C) 2025 guangyin53222
#
# This is free software, licensed under the Apache-2.0 License.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=athena-led
PKG_VERSION:=2.5.0
PKG_RELEASE:=1

PKG_MAINTAINER:=guangyin53222 <https://github.com/guangyin53222>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

# 彻底移除 PKG_SOURCE / PKG_SOURCE_URL / PKG_HASH
# 依赖本地 files/ 目录打包，无需下载，无哈希校验问题

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=utils
  CATEGORY:=Utilities
  # 限制为 AX6600 (ipq807x) aarch64 架构，避免其他平台误选报错
  DEPENDS:=@TARGET_qualcommax_ipq807x +libc
  TITLE:=Athena LED controller (backend)
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./files/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	# 预编译二进制，无需编译
	true
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/athena_led.init $(1)/etc/init.d/athena_led

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/athena_led.config $(1)/etc/config/athena_led

	$(INSTALL_DIR) $(1)/usr/bin
	# 确保 files/ 下有此二进制
	$(INSTALL_BIN) ./files/athena_led $(1)/usr/bin/athena_led

	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) ./files/find_button.sh $(1)/usr/sbin/find_button.sh
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
