

include $(TOPDIR)/rules.mk


LUCI_TITLE:=LuCI support for Plex
LUCI_PKGARCH:=all
LUCI_DEPENDS:=+lsblk +docker +luci-lib-taskd +luci-lib-docker

define Package/luci-app-plex/conffiles
/etc/config/plex
endef

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
