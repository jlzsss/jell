include $(TOPDIR)/rules.mk

PKG_NAME:=trojan-plus
PKG_VERSION:=10.0.3
PKG_RELEASE:=5

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/peter-tank/trojan-plus/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=skip

PKG_BUILD_PARALLEL:=1
PKG_BUILD_DEPENDS:=openssl

PKG_LICENSE:=GPL-3.0
PKG_LICENSE_FILE:=LICENSE
PKG_MAINTAINER:=Trojan-Plus-Group

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

TARGET_CXXFLAGS += -Wall -Wextra
TARGET_CXXFLAGS += $(FPIC)

# LTO
TARGET_CXXFLAGS += -flto
TARGET_LDFLAGS += -flto

# CXX standard
TARGET_CXXFLAGS += -std=c++11
TARGET_CXXFLAGS := $(filter-out -O%,$(TARGET_CXXFLAGS)) -O3
TARGET_CXXFLAGS += -ffunction-sections -fdata-sections
TARGET_LDFLAGS += -Wl,--gc-sections

CMAKE_OPTIONS += \
	-DENABLE_MYSQL=OFF \
	-DENABLE_NAT=ON \
	-DENABLE_REUSE_PORT=ON \
	-DENABLE_SSL_KEYLOG=ON \
	-DENABLE_TLS13_CIPHERSUITES=ON \
	-DFORCE_TCP_FASTOPEN=OFF \
	-DSYSTEMD_SERVICE=OFF \
	-DOPENSSL_USE_STATIC_LIBS=FALSE \
	-DBoost_DEBUG=ON \
	-DBoost_NO_BOOST_CMAKE=ON

define Package/trojan-plus
	SECTION:=net
	CATEGORY:=Network
	TITLE:=An unidentifiable mechanism that helps you bypass GFW. It's compatible with original trojan with experimental features.
	URL:=https://github.com/Trojan-Plus-Group/trojan-plus
	DEPENDS:= \
		+libpthread +libstdcpp +libopenssl \
		+boost +boost-system +boost-program_options
endef

define Package/trojan-plus/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/trojan $(1)/usr/sbin/trojan-plus
endef

$(eval $(call BuildPackage,trojan-plus))
