include $(TOPDIR)/rules.mk

PKG_NAME:=sqm-autorate-nss
PKG_VERSION:=20261127
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/nihilt/sqm-autorate-nss.git
PKG_SOURCE_VERSION:=f98425c492dbcb23b1b3062cdac76f0f67bb25e4
PKG_MIRROR_HASH:=skip

PKG_MAINTAINER:=nihilt <56614537+nihilt@users.noreply.github.com>
PKG_LICENSE:=GPL-3.0-only
PKG_LICENSE_FILES:=LICENSE

include $(INCLUDE_DIR)/package.mk

SRC_ROOT:=$(PKG_BUILD_DIR)/files

define Package/sqm-autorate-nss
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Quality of Service
  TITLE:=Latency-aware rate control for the NSS SQM shaper
  URL:=https://github.com/nihilt/sqm-autorate-nss
  PKGARCH:=all
  DEPENDS:=+sqm-scripts +fping +perl +perlbase-fcntl +perlbase-io +perlbase-ipc +perlbase-posix +perlbase-symbol +perlbase-time
endef

define Package/sqm-autorate-nss/description
  A daemon that measures latency with fping and moves the rate of the NSS shaper (nsstbl)
  that nss-rk.qos builds, up when the line is quiet and down when queues build.
  Ships profiles, the helpers sqm-status and switch-profile, and a procd init script.
  Settings live in memory unless you ask for them to be kept across a reboot.
endef

define Package/sqm-autorate-nss/conffiles
/etc/sqm-default
/etc/sqm-profiles/sqm-autorate-custom.conf
/etc/sqm-profiles/sqm-autorate-debug.conf
/etc/sqm-profiles/sqm-autorate-gaming.conf
/etc/sqm-profiles/sqm-autorate-performance.conf
/etc/sqm-profiles/sqm-autorate-streaming.conf
/etc/logrotate.d/sqm-autorate
endef

define Build/Configure
endef

define Build/Compile
endef

define Build/Prepare
	$(call Build/Prepare/Default)
endef

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

	$(INSTALL_DIR) $(1)/usr/lib/sqm-autorate
	$(INSTALL_DATA) $(SRC_ROOT)/usr/lib/sqm-autorate/common.sh $(1)/usr/lib/sqm-autorate/
endef

$(eval $(call BuildPackage,sqm-autorate-nss))
