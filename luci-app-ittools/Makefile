

include $(TOPDIR)/rules.mk


LUCI_TITLE:=LuCI support for ITTools
LUCI_PKGARCH:=all
LUCI_DEPENDS:=+lsblk +docker +luci-lib-taskd +luci-lib-docker

define Package/luci-app-ittools/conffiles
/etc/config/ittools
endef

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
