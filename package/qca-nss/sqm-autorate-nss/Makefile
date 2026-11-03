include $(TOPDIR)/rules.mk

PKG_NAME:=sqm-autorate-nss
PKG_VERSION:=20261101
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/nihilt/sqm-autorate-nss.git
PKG_SOURCE_VERSION:=d6397b3e1e0451bff3fd1c3ededd3eb1e63b8f08
PKG_MIRROR_HASH:=skip

PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

define Package/sqm-autorate-nss
  SECTION:=net
  CATEGORY:=Base system
  TITLE:=SQM-Autorate-NSS latency-aware SQM daemon for NSS builds
  URL:=https://github.com/nihilt/sqm-autorate-nss
  DEPENDS:=@TARGET_ipq806x +sqm-scripts-nss +sqm-scripts +jsonfilter +perl \
           +perlbase-ipc +perlbase-threads +perlbase-symbol +perlbase-file \
           +perlbase-io +perlbase-time +perlbase-storable +perlbase-cwd \
           +perlbase-digest +perlbase-data +perlbase-fcntl +perlbase-socket \
           +perlbase-getopt +ip-full +tc-full +iputils-ping +fping \
           +logrotate +procps-ng +coreutils +procd
  PKGARCH:=all
endef

define Package/sqm-autorate-nss/description
  SQM-Autorate-NSS latency-aware SQM daemon for OpenWrt NSS builds,
  adjusting nsstbl rates via nss-rk.qos.
endef

define Package/sqm-autorate-nss/conffiles
/etc/sqm-default
/etc/logrotate.d/sqm-autorate
/etc/sqm-profiles/sqm-autorate-custom.conf
/etc/sqm-profiles/sqm-autorate-debug.conf
/etc/sqm-profiles/sqm-autorate-gaming.conf
/etc/sqm-profiles/sqm-autorate-performance.conf
/etc/sqm-profiles/sqm-autorate-streaming.conf
endef

define Build/Configure
endef

define Build/Compile
endef

SRC_ROOT:=$(PKG_BUILD_DIR)/files

define Package/sqm-autorate-nss/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(SRC_ROOT)/usr/bin/sqm-autorate.pl $(1)/usr/bin/
	$(INSTALL_BIN) $(SRC_ROOT)/usr/bin/sqm-status $(1)/usr/bin/
	$(INSTALL_BIN) $(SRC_ROOT)/usr/bin/switch-profile $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc
	$(INSTALL_CONF) $(SRC_ROOT)/etc/sqm-default $(1)/etc/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) $(SRC_ROOT)/etc/init.d/sqm-autorate $(1)/etc/init.d/

	$(INSTALL_DIR) $(1)/etc/logrotate.d
	$(INSTALL_CONF) $(SRC_ROOT)/etc/logrotate.d/sqm-autorate $(1)/etc/logrotate.d/

	$(INSTALL_DIR) $(1)/etc/sqm-profiles
	$(INSTALL_CONF) $(SRC_ROOT)/etc/sqm-profiles/*.conf $(1)/etc/sqm-profiles/
endef

$(eval $(call BuildPackage,sqm-autorate-nss))
