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

PKG_SOURCE_PROTO:=none
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=@TARGET_qualcommax
  TITLE:=Athena LED controller (backend)
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) ./files/* $(PKG_BUILD_DIR)/
endef

define Build/Compile
	true
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/athena_led.init $(1)/etc/init.d/athena_led

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/athena_led.config $(1)/etc/config/athena_led

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) ./files/athena-led $(1)/usr/bin/athena_led

	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) ./files/find_button.sh $(1)/usr/sbin/find_button.sh

	$(INSTALL_DIR) $(1)/usr/share/athena-led/anim
	[ -d ./files/anim ] && $(CP) ./files/anim/* $(1)/usr/share/athena-led/anim/ || true
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
