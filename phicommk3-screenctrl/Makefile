include $(TOPDIR)/rules.mk

PKG_NAME:=phicommk3-screenctrl
PKG_VERSION:=3257090decf7de1e70ef6e7bf28d0491ffe78854
PKG_RELEASE:=4

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Hill-98/k3screenctrl.git
PKG_SOURCE_VERSION:=3257090decf7de1e70ef6e7bf28d0491ffe78854
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_SOURCE_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.xz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)
PKG_MAINTAINER:=Dennis <op@tossp.com>

include $(INCLUDE_DIR)/package.mk

TARGET_CFLAGS+= -D_GNU_SOURCE

define Package/$(PKG_NAME)
  SECTION:=utils
  CATEGORY:=Utilities
  DEPENDS:=@TARGET_bcm53xx_DEVICE_phicomm-k3 +wget +iputils-arping
  TITLE:=LCD screen controller on PHICOMM K3
  URL:=https://github.com/Hill-98/k3screenctrl
endef

define Package/$(PKG_NAME)/description
 K3 Screen Controller (k3screenctrl) is a program utilizing
the LCD screen on PHICOMM K3 to display some stats.
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/lib/k3screenctrl
	$(INSTALL_DIR) $(1)/lib/k3screenctrl/oui
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_DIR) $(1)/etc/config

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/k3screenctrl $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lib/k3screenctrl/oui/update_oui.sh $(1)/lib/k3screenctrl/oui/

	$(INSTALL_DATA) $(PKG_BUILD_DIR)/lib/k3screenctrl/oui/oui.txt $(1)/lib/k3screenctrl/oui/
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/lib/k3screenctrl/oui/oui.txt.md5 $(1)/lib/k3screenctrl/oui/

	$(INSTALL_BIN) ./files/k3screenctrl.init $(1)/etc/init.d/k3screenctrl
	$(INSTALL_BIN) ./files/device_online.sh $(1)/lib/k3screenctrl/
	$(INSTALL_BIN) ./files/device_custom.sh $(1)/lib/k3screenctrl/
	$(INSTALL_BIN) ./files/host.sh $(1)/lib/k3screenctrl/
	$(INSTALL_BIN) ./files/basic.sh $(1)/lib/k3screenctrl/
	$(INSTALL_BIN) ./files/port.sh $(1)/lib/k3screenctrl/
	$(INSTALL_BIN) ./files/wifi.sh $(1)/lib/k3screenctrl/
	$(INSTALL_BIN) ./files/wan.sh $(1)/lib/k3screenctrl/

	$(INSTALL_CONF) ./files/config $(1)/etc/config/k3screenctrl
endef

$(eval $(call BuildPackage,$(PKG_NAME)))