# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=flun
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/flun
  TITLE:=MTK LinkIt Smart board support package
  HIDDEN:=1
  DEPENDS:=@TARGET_ramips_mt7688_FLun \
  	+avahi-nodbus-daemon +mountd \
	+spi-tools \
	+kmod-fs-vfat +kmod-fs-exfat +kmod-i2c-core +kmod-i2c-ralink \
	+kmod-nls-base +kmod-nls-cp437 +kmod-nls-iso8859-1 \
	+kmod-nls-iso8859-15 +kmod-nls-iso8859-2 +kmod-nls-utf8 \
	+kmod-sdhci-mt7620 +kmod-usb-storage \
	+kmod-sound-core +kmod-sound-mtk +madplay-alsa +alsa-utils \
	+flun-wifi

  CATEGORY:=Base system
  DEFAULT:=y
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Compile
        $(TARGET_CC) $(TARGET_CFLAGS) $(EXTRA_CFLAGS) -Wall -Werror -o $(PKG_BUILD_DIR)/pinmux src/pinmux.c ; \
        $(TARGET_CC) $(TARGET_CFLAGS) $(EXTRA_CFLAGS) -Wall -Werror -o $(PKG_BUILD_DIR)/refclk src/refclk.c
endef

define Package/flun/install
	$(INSTALL_DIR) $(1)/sbin
	
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pinmux $(1)/sbin/mt7688_pinmux
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/refclk $(1)/sbin/mt7688_reclk
	$(CP) ./files/* $(1)
endef

$(eval $(call BuildPackage,flun))
