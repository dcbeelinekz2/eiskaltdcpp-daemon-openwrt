include $(TOPDIR)/rules.mk

PKG_NAME:=eiskaltdcpp
PKG_VERSION:=2.2.10
PKG_RELEASE:=3
PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/eiskaltdcpp/eiskaltdcpp.git
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=52af555638f7b1b4baa58b43be75985fcf82760e
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DEPENDS:=zlib bzip2 gettext iconv

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk
include $(INCLUDE_DIR)/nls.mk

define Package/eiskaltdcpp
  SECTION:=base
  CATEGORY:=Network
  TITLE:=Eiskalt DC++ Client
  URL:=https://github.com/eiskaltdcpp/eiskaltdcpp
  DEPENDS:=+zlib +bzip2 +libopenssl +libpthread +libstdcpp +iconv +gettext
endef
define Package/eiskaltdcpp/description
  EiskaltDC++ is a cross-platform program that uses the Direct Connect and ADC protocols
endef

define Build/Configure
	$(call Build/Configure/Default)
endef

CMAKE_OPTIONS = \
	-DUSE_IDNA=OFF  \
	-DLINK=STATIC  \
	-DUSE_QT5=OFF  \
	-DFREE_SPACE_BAR_C=OFF  \
	-DDBUS_NOTIFY=OFF  \
	-DUSE_LIBNOTIFY=OFF  \
	-DNO_UI_DAEMON=ON  \
	-DJSONRPC_DAEMON=ON  \
	-DWITH_EMOTICONS=OFF  \
	-DFORCE_XDG=OFF  \
	-DLOCAL_BOOST=ON  \
	-DDO_NOT_USE_MUTEX=ON \
	-DCMAKE_FIND_ROOT_PATH="$(STAGING_DIR)" \
	-DCMAKE_FIND_ROOT_PATH_MODE_PROGRAM=NEVER \
	-DCMAKE_FIND_ROOT_PATH_MODE_LIBRARY=ONLY \
	-DCMAKE_CXX_FLAGS="-pipe -I${ICONV_PREFIX}/include -I${INTL_PREFIX}/include -fno-caller-saves -fhonour-copts -Wno-error=unused-but-set-variable -fpic -fomit-frame-pointer -Wall" \
	-DCMAKE_C_FLAGS="-pipe -I${ICONV_PREFIX}/include -I${INTL_PREFIX}/include -fno-caller-saves -fhonour-copts -Wno-error=unused-but-set-variable -fpic -fomit-frame-pointer -Wall" \
	-DICONV_LIBRARIES=${STAGING_DIR}/usr/lib \
	-DICONV_INCLUDE_DIR=${ICONV_PREFIX}/include \
	-DGETTEXT_INCLUDE_DIR="$(INTL_PREFIX)/include" \
	-DCMAKE_PREFIX_PATH="$(STAGING_DIR)/"


define Package/eiskaltdcpp/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/eiskaltdcpp-daemon/eiskaltdcpp-daemon $(1)/usr/bin/
endef

$(eval $(call BuildPackage,eiskaltdcpp))
