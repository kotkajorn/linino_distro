#
# Copyright (C) 2014 Dog Hunter AG
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=arduino-files
PKG_VERSION:=1.7.2
PKG_RELEASE:=4

PKG_SOURCE_URL:=http://download.linino.org/pkg-src/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_MD5SUM:=9f8af7912d1859a164e7c49c3a640bb5

PKG_FILE:="$(STAGING_DIR)/pkginfo/libc.provides"
PKG_CAT=`cat $(PKG_FILE) | grep libc.so.6`

include $(INCLUDE_DIR)/package.mk

define Package/arduino-files
	SECTION:=devel
	CATEGORY:=Development
	TITLE:=Configuration Files for Arduino IDE
	DEPENDS:=+zlib +libstdcpp +libc
endef

define Package/arduino-files/description
	Configuration Files for Arduino IDE
endef

define Build/Prepare
    (if [ ! $(PKG_CAT) ];then echo "libc.so.6" >> $(PKG_FILE); fi)
	mkdir -p $(PKG_BUILD_DIR)/temp
	/bin/tar xvf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR)/temp --strip-components=1
endef

define Build/Configure
	# NOOP
endef

define Build/Compile
	# NOOP
endef

define Package/arduino-files/install
	$(INSTALL_DIR) $(1)/arduino
	
	$(CP) -av $(PKG_BUILD_DIR)/temp/* $(1)/arduino
endef

define Package/arduino-files/postrm
#!/bin/sh
# check if we are on a real system
if [ -d /opt/arduino ]
then
	rm -rvf /opt/arduino
fi
endef

$(eval $(call BuildPackage,arduino-files))
