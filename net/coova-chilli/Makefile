#
# Copyright (C) 2007-2013 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=coova-chilli
PKG_VERSION:=1.3.0
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://ap.coova.org/chilli
PKG_MD5SUM:=dc0037e3cdebcb60508081b4e42e984a

PKG_INSTALL:=1

PKG_CONFIG_DEPENDS := \
  COOVACHILLI_MINIPORTAL \
  COOVACHILLI_REDIR \
  COOVACHILLI_USERAGENT \
  COOVACHILLI_DNSLOG \
  COOVACHILLI_UAMDOMAINFILE

include $(INCLUDE_DIR)/package.mk

define Package/coova-chilli
  SUBMENU:=Captive Portals
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+kmod-tun +librt
  TITLE:=Wireless LAN HotSpot controller (Coova Chilli Version)
  URL:=http://www.coova.org/CoovaChilli
  MAINTAINER:=Imre Kaloz <kaloz@openwrt.org>
  MENU:=1
endef

define Package/coova-chilli/description
	CoovaChilli is an open source access controller for wireless LAN
	access points and is based on ChilliSpot. It is used for authenticating
	users of a wireless (or wired) LAN. It supports web based login (UAM)
	which is today's standard for public HotSpots and it supports Wireless
	Protected Access (WPA) which is the standard of the future.
	Authentication,	authorization and accounting (AAA) is handled by your
	favorite radius server.
endef

define Package/coova-chilli/config
  source "$(SOURCE)/Config.in"
endef

define Build/Configure
	$(call Build/Configure/Default, \
	$(if $(CONFIG_COOVACHILLI_REDIR),--enable,--disable)-chilliredir \
	$(if $(CONFIG_COOVACHILLI_DNSLOG),--enable,--disable)-dnslog \
	$(if $(CONFIG_COOVACHILLI_MINIPORTAL),--enable,--disable)-miniportal \
	$(if $(CONFIG_COOVACHILLI_USERAGENT),--enable,--disable)-useragent \
	$(if $(CONFIG_COOVACHILLI_UAMDOMAINFILE),--enable,--disable)-uamdomainfile \
	)
endef

define Package/coova-chilli/conffiles
/etc/chilli.conf
endef

define Package/coova-chilli/install
	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) $(PKG_INSTALL_DIR)/etc/chilli.conf $(1)/etc/
	$(INSTALL_DIR) $(1)/etc/chilli
	$(CP) $(PKG_INSTALL_DIR)/etc/chilli/* $(1)/etc/chilli/
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/sbin/chilli* $(1)/usr/sbin/
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/lib*.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,coova-chilli))
