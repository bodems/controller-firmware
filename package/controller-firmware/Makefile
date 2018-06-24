include $(TOPDIR)/rules.mk

PKG_NAME:=controller-firmware
PKG_VERSION:=0.0.1
PKG_RELEASE:=1

PKG_BUILD_DIR:=$(BUILD_DIR)/controller-firmware

include $(INCLUDE_DIR)/package.mk

define Package/controller-firmware
	SECTION:=base
	CATEGORY:=EVSE
	DEFAULT:=y
	TITLE:= Controller Firmware for EVSE
	URL:=https://github.com/bodems/controller-firmware
	DEPENDS:=+uhttpd +haserl +px5g +libustream-mbedtls
endef

define Build/Prepare
	echo "all: " > $(PKG_BUILD_DIR)/Makefile
endef

define Package/controller-firmware/install
	#nothing to do here
endef

define Package/freifunk/conffiles
	/etc/config/controller
endef

$(eval $(call BuildPackage,controller-firmware))
