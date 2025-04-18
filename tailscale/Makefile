#
# Copyright (C) 2021 CZ.NIC, z. s. p. o. (https://www.nic.cz/)
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tailscale
PKG_VERSION:=1.32.3
PKG_RELEASE:=19

PKG_SOURCE:=tailscale-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/tailscale/tailscale/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=skip

PKG_MAINTAINER:=Jan Pavlinec <jan.pavlinec1@gmail.com>
PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE

PKG_BUILD_DIR:=$(BUILD_DIR)/tailscale-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=\
	tailscale.com/cmd/tailscale \
	tailscale.com/cmd/tailscaled
GO_PKG_LDFLAGS:=-X 'tailscale.com/version.Long=$(PKG_VERSION)-$(PKG_RELEASE) (OpenWrt)'
GO_PKG_LDFLAGS_X:=tailscale.com/version.Short=$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/tailscale/Default
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=VPN
  TITLE:=Zero config VPN
  URL:=https://tailscale.com
  DEPENDS:=$(GO_ARCH_DEPENDS)
endef

define Package/tailscaled
  $(call Package/tailscale/Default)
  TITLE+= (daemon)
  DEPENDS+= +ca-bundle +kmod-tun
endef

define Package/tailscale
  $(call Package/tailscale/Default)
  TITLE+= (utility)
  DEPENDS+= +tailscaled
endef

define Package/tailscale/description
  It creates a secure network between your servers, computers,
  and cloud instances. Even when separated by firewalls or subnets.
endef

Package/tailscaled/description:=$(Package/tailscale/description)

define Package/tailscale/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/tailscale $(1)/usr/sbin
endef

define Package/tailscaled/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/tailscaled $(1)/usr/sbin
	$(INSTALL_DIR) $(1)/etc/init.d/
	$(INSTALL_BIN) ./files//tailscale.init $(1)/etc/init.d/tailscale
	$(INSTALL_DIR) $(1)/etc/config/
	$(INSTALL_DATA) ./files//tailscale.conf $(1)/etc/config/tailscale
endef

define Package/tailscaled/conffiles
/etc/config/tailscale
/etc/tailscale/tailscaled.state
endef

$(eval $(call BuildPackage,tailscale))
$(eval $(call BuildPackage,tailscaled))
