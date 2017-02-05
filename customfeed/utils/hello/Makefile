include $(TOPDIR)/rules.mk

PKG_NAME:=hello
PKG_VERSION:=2.10
PKG_RELEASE:=1

PKG_SOURCE_NAME:=$(PKG_NAME)-$(PKG_VERSION)

PKG_SOURCE:=$(PKG_SOURCE_NAME).tar.gz
PKG_SOURCE_URL:=https://ftp.gnu.org/pub/gnu/hello/
PKG_MD5SUM:=6cd0ffea3884a4e79330338dcc2987d6
PKG_MAINTAINER:=Alexey Cherepanov <a@cherepanov.info>
PKG_LICENSE:=BSD

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_NAME)

PKG_BUILD_PARALLEL:=1
PKG_INSTALL:=1

PKG_FIXUP:=autoreconf

PKG_CONFIG_DEPENDS:=HELLO_FOO

include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk

define Package/hello
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=GNU Hello
  URL:=http://gnu.org/
  DEPENDS:=+libc
endef

define Package/hello/description
GNU Hello World
endef

define Package/hello/config
  source "$(SOURCE)/Config.in"
endef

define Package/hello/conffiles
/etc/hello.conf
endef

define Build/Configure
	( cd $(PKG_BUILD_DIR) ; \
		GNULIB_TEST_STRERROR=0 ./configure \
		--prefix=/usr \
		--disable-nls \
		--host=mips \
	)
endef

define Build/Compile
	+$(MAKE) $(PKG_JOBS) -C $(PKG_BUILD_DIR) \
		CC="$(TARGET_CC)" \
		-I$(PKG_BUILD_DIR)/lib \
		CFLAGS="$(CFLAGS) $(TARGET_CFLAGS)" \
		LDFLAGS="$(TARGET_LDFLAGS)"
endef

define Package/hello/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/hello $(1)/usr/bin/hello
endef

$(eval $(call BuildPackage,hello))
