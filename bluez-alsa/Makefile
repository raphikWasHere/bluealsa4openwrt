#
# Copyright (C) 2017-2018 Daniel Engberg <daniel.engberg.lists@pyret.net>
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=bluez-alsa
PKG_VERSION:=4.1.1
PKG_RELEASE:=1
PKG_MAINTAINER:=
PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE

#PKG_SOURCE_URL:=https://github.com/Arkq/bluez-alsa/archive/v4.1.1
#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_HASH:=b69a3e6dd69315194403ee930ac1553aed3fb9a3988e502ae5c24a8bfef70f9f
PKG_SOURCE_URL:=https://github.com/arkq/bluez-alsa/archive/refs/heads
PKG_SOURCE:=big-endian.tar.gz
PKG_HASH:=8083cb8df61ae7083b8f49c1d46b2cf789c550dca661ebe4905357c8a3554b0c

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/bluez-alsa
  SECTION:=sound
  CATEGORY:=Sound
  DEPENDS:=+alsa-lib +bluez-daemon +glib2 +sbc
  TITLE:=Bluetooth Audio ALSA backend
  URL:=https://github.com/Arkq/bluez-alsa
endef

define Package/bluez-alsa/description
  ALSA plugin supporting Bluetooth audio
endef

CONFIGURE_ARGS += --enable-a2dpconf --disable-rfcomm --enable-debug

define Package/bluez-alsa/install
	$(INSTALL_DIR) $(1)/etc/alsa/conf.d/
	$(CP) $(PKG_BUILD_DIR)/src/asound/20-bluealsa.conf $(1)/etc/alsa/conf.d/
	$(INSTALL_DIR) $(1)/usr/lib/alsa-lib
	$(CP) $(PKG_BUILD_DIR)/src/asound/.libs/libasound_module_*_bluealsa.so $(1)/usr/lib/alsa-lib
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/bluealsa $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/utils/aplay/bluealsa-aplay $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/bluealsa.init $(1)/etc/init.d/bluealsa
	$(INSTALL_DIR) $(1)/etc/dbus-1/system.d/
	$(INSTALL_BIN) ./files/bluealsa.conf $(1)/etc/dbus-1/system.d/
endef

$(eval $(call BuildPackage,bluez-alsa))
