
include $(TOPDIR)/rules.mk

PKG_NAME:=empty
PKG_VERSION:=0.6.20b
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tgz
PKG_SOURCE_URL:=http://downloads.sourceforge.net/sourceforge/$(PKG_NAME)
PKG_HASH:=7e6636e400856984c4405ce7bd0843aaa3329fa3efd20c58df8400a9eaa35f09

PKG_MAINTAINER:=Mikhail E. Zakharov <zmey20000@yahoo.com>
PKG_LICENSE:=CUSTOM
PKG_LICENSE_FILES:=COPYRIGHT

include $(INCLUDE_DIR)/package.mk

define Package/empty
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Run applications under pseudo-terminal sessions
  URL:=http://empty.sourceforge.net/
endef

define Package/empty/description
  empty - run applications under pseudo-terminal (PTY) sessions to
  dialogue with interactive programs. Replace TCL/Expect with a simple
  tool and use your favorite shell (sh, bash, csh, tcsh, ksh, zsh, etc)
endef

TARGET_CFLAGS += -ffunction-sections -fdata-sections
TARGET_LDFLAGS += -Wl,--gc-sections

# Use Link time optimization
TARGET_CFLAGS += -flto
TARGET_LDFLAGS += -flto

define Package/empty/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/empty $(1)/usr/bin/
endef

$(eval $(call BuildPackage,empty))
