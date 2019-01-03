
include $(TOPDIR)/rules.mk

PKG_NAME:=pdnsd
PKG_VERSION:=1.2.9a
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-par.tar.gz
PKG_SOURCE_URL:=http://members.home.nl/p.a.rombouts/pdnsd/releases
PKG_HASH:=bb5835d0caa8c4b31679d6fd6a1a090b71bdf70950db3b1d0cea9cf9cb7e2a7b

PKG_MAINTAINER:=Paul A. Rombouts <p.a.rombouts@home.nl>
PKG_LICENSE:=GPL
PKG_LICENSE_FILES:=COPYING COPYING.BSD

include $(INCLUDE_DIR)/package.mk

define Package/pdnsd
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Web Servers/Proxies
  DEPENDS:=+libpthread
  TITLE:=Proxy DNS server with permanent caching
  URL:=http://members.home.nl/p.a.rombouts/pdnsd/
endef

define Package/pdnsd/description
  pdnsd is a DNS server designed for persistent caching of DNS information.
  The cache contents are written to hard disk on exit. It can significantly
  increase browsing speed on a broadband connection.
endef

CONFIGURE_ARGS += \
	--prefix=/usr \
  --sysconfdir=/etc \
  --sbindir=/usr/sbin \
  --enable-ipv6 \
  --with-cachedir=/var/pdnsd \
  --with-query-method=tcpudp

TARGET_CFLAGS += -ffunction-sections -fdata-sections
TARGET_LDFLAGS += -Wl,--gc-sections

# Use Link time optimization
TARGET_CFLAGS += -flto
TARGET_LDFLAGS += -flto

define Package/pdnsd/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/pdnsd $(1)/usr/sbin/

	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/pdnsd-ctl/pdnsd-ctl $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/doc/pdnsd.conf $(1)/etc/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/pdnsd.init $(1)/etc/init.d/pdnsd
endef

$(eval $(call BuildPackage,pdnsd))
