#
# Copyright (C) 2013 Stratosphere
#
# This is free software, licensed under the GNU General Public License v2.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=trema-switch
PKG_RELEASE:=1

PKG_SOURCE:=master.zip
PKG_SOURCE_URL:=https://github.com/trema/trema-edge/archive/
PKG_MAINTAINER:=Hiroaki KAWAI <kawai@stratosphere.co.jp>

PKG_LICENSE:=GPLv2

include $(INCLUDE_DIR)/package.mk

PKG_UNPACK:=unzip -d $(PKG_BUILD_DIR)/ $(DL_DIR)/$(PKG_SOURCE)

define Package/trema-switch
  SECTION:=net
  CATEGORY:=Network
  TITLE:=trema edge openflow 1.3 software switch
  DEPENDS:=+libsqlite3 +librt +libpthread
endef

define Package/trema-switch/description
  Trema-edge is a successor of trema openflow project. 
endef

define Build/Compile
  (cd $(PKG_BUILD_DIR)/trema-edge-master; \
    $(TARGET_CC) $(TARGET_CFLAGS) -std=gnu99 -D_GNU_SOURCE -DNOT_TESTED \
      -Isrc/lib -Isrc/switch/datapath -Isrc/switch/switch \
      src/lib/*.c src/switch/datapath/*.c src/switch/switch/*.c \
      -lsqlite3 -lpthread -lrt -o $(PKG_BUILD_DIR)/trema-switch)
endef

define Package/trema/switch/install
  $(INSTALL_DIR) $(1)/sbin
  $(INSTALL_BIN) $(PKG_BUILD_DIR)/trema-switch $(1)/sbin
  $(INSTALL_DIR) $(1)/etc/config
  $(INSTALL_DATA) ./files/trema-switch.conf $(1)/etc/config/trema-switch
  $(INSTALL_DIR) $(1)//etc/init.d
  $(INSTALL_BIN) ./files/trema-switch.init $(1)/etc/init.d/trema-switch
endef

$(eval $(call BuildPackage,trema-switch))

