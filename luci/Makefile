#
# Copyright (C) 2026 RomikB <romikb@mail.ru>
#

include $(TOPDIR)/rules.mk

PKG_NAME:=luci
PKG_VERSION:=0.11.1
PKG_RELEASE:=1

PKG_FORCE_PREBUILT:=y

LUCI_BUILD_PACKAGES:=


### Core package ###
define Package/luci-lib-core
  SECTION:=luci
  CATEGORY:=LuCI
  TITLE:=LuCI - Lua Configuration Interface
  URL:=http://luci.subsignal.org/
  MAINTAINER:=LuCI Development Team <luci@lists.subsignal.org>
  SUBMENU:=8. Libraries
  DEPENDS:=+lua +libuci-lua +libubus-lua
  TITLE:=LuCI core libraries
endef

define Package/luci-lib-core/install
  true
endef

LUCI_BUILD_PACKAGES += luci-lib-core


### Libraries ###
define library
  define Package/luci-lib-$(1)
    SECTION:=luci
    CATEGORY:=LuCI
    TITLE:=LuCI - Lua Configuration Interface
    URL:=http://luci.subsignal.org/
    MAINTAINER:=LuCI Development Team <luci@lists.subsignal.org>
    SUBMENU:=8. Libraries
    TITLE:=$(if $(2),$(2),LuCI $(1) library)
    $(if $(3),DEPENDS:=+luci-lib-core $(3))
  endef

  define Package/luci-lib-$(1)/install
	true
  endef

  LUCI_BUILD_PACKAGES += luci-lib-$(1)
endef

$(eval $(call library,ipkg,LuCI IPKG/OPKG call abstraction library))
$(eval $(call library,json,LuCI JSON library))
$(eval $(call library,lua-cjson,Lua CJSON library,+liblua))
$(eval $(call library,nixio,NIXIO POSIX library,+PACKAGE_luci-lib-nixio_openssl:libopenssl +PACKAGE_luci-lib-nixio_cyassl:libcyassl))
$(eval $(call library,sys,LuCI Linux/POSIX system library))
$(eval $(call library,web,MVC Webframework,+luci-lib-sys +luci-lib-nixio +luci-sgi-cgi))
$(eval $(call library,xiaoqiang,XiaoQiang util,+lua-curl-v3 +libstdcpp +luci-lib-core +luci-lib-json +liblua))


### Protocols ###
define protocol
  define Package/luci-proto-$(1)
    SECTION:=luci
    CATEGORY:=LuCI
    TITLE:=LuCI - Lua Configuration Interface
    URL:=http://luci.subsignal.org/
    MAINTAINER:=LuCI Development Team <luci@lists.subsignal.org>
    SUBMENU:=6. Protocols
    TITLE:=$(if $(2),$(2),LuCI $(1) protocol support)
    DEPENDS:=$(3)
  endef

  define Package/luci-proto-$(1)/install
	true
  endef

  LUCI_BUILD_PACKAGES += luci-proto-$(1)
endef

$(eval $(call protocol,core,Support for static/dhcp/none))
$(eval $(call protocol,ppp,Support for PPP/PPPoE/PPPoA/PPtP))


### Modules ###
define module
  define Package/luci-mod-$(1)
    SECTION:=luci
    CATEGORY:=LuCI
    TITLE:=LuCI - Lua Configuration Interface
    URL:=http://luci.subsignal.org/
    MAINTAINER:=LuCI Development Team <luci@lists.subsignal.org>
    SUBMENU:=2. Modules
    TITLE:=$(if $(2),$(2),LuCI $(1) module)
    $(if $(3),DEPENDS+=$(3))
  endef

  define Package/luci-mod-$(1)/install
	true
  endef

  LUCI_BUILD_PACKAGES += luci-mod-$(1)
endef

$(eval $(call module,admin-CN-common,LuCI Administration - common chinese -featured for full control,+luci-mod-admin-core +luci-lib-ipkg +luci-mod-admin-base))
$(eval $(call module,admin-base,LuCI Administration - base-featured for full control,+luci-mod-admin-core +luci-lib-ipkg))
$(eval $(call module,admin-core,Web UI Core module,+luci-lib-web +luci-proto-core))
$(eval $(call module,admin-diagnosis,LuCI Administration - diagnosis-featured for web control,+luci-mod-admin-core +luci-lib-ipkg))
$(eval $(call module,func-anti_attack,Interfaces for anti dos/scan attack,+luci-mod-admin-core))
$(eval $(call module,func-mipctl,Error page for access intercepted by miparentalctl,+luci-mod-admin-core))
$(eval $(call module,product-retails,LuCI Administration - Retail products -featured for full control,+luci-mod-admin-core +luci-lib-ipkg))


### Applications ###
define application
  define Package/luci-app-$(1)
    SECTION:=luci
    CATEGORY:=LuCI
    TITLE:=LuCI - Lua Configuration Interface
    URL:=http://luci.subsignal.org/
    MAINTAINER:=LuCI Development Team <luci@lists.subsignal.org>
    SUBMENU:=3. Applications
    TITLE:=$(if $(2),$(2),LuCI $(1) application)
	DEPENDS:=$(3)
  endef

  define Package/luci-app-$(1)/install
	true
  endef

  LUCI_BUILD_PACKAGES += luci-app-$(1)
endef

$(eval $(call application,firewall,Firewall and Portforwarding application,\
	+PACKAGE_luci-app-firewall:firewall))


### Server Gateway Interfaces ###
define sgi
  define Package/luci-sgi-$(1)
    SECTION:=luci
    CATEGORY:=LuCI
    TITLE:=LuCI - Lua Configuration Interface
    URL:=http://luci.subsignal.org/
    MAINTAINER:=LuCI Development Team <luci@lists.subsignal.org>
    SUBMENU:=7. Server Interfaces
    TITLE:=$(if $(2),$(2),LuCI $(1) server gateway interface)
	DEPENDS:=$(3)
  endef

  define Package/luci-sgi-$(1)/install
	true
  endef

  LUCI_BUILD_PACKAGES += luci-sgi-$(1)
endef

$(eval $(call sgi,cgi,CGI Gateway behind existing Webserver))


### Themes ###
define theme
  define Package/luci-theme-$(1)
    SECTION:=luci
    CATEGORY:=LuCI
    TITLE:=LuCI - Lua Configuration Interface
    URL:=http://luci.subsignal.org/
    SUBMENU:=4. Themes
    TITLE:=$(if $(2),$(2),LuCI $(1) theme)
	MAINTAINER:=$(if $(3),$(3),LuCI Development Team <luci@lists.subsignal.org>)
	DEPENDS:=$(if $(filter-out base,$(1)),+luci-theme-base) $(4)
	$(if $(5),DEFAULT:=PACKAGE_luci-lib-core)
  endef

  define Package/luci-theme-$(1)/install
	true
  endef

  LUCI_BUILD_PACKAGES += luci-theme-$(1)
endef

$(eval $(call theme,base,Common base for all themes))
$(eval $(call theme,openwrt,OpenWrt.org (default),,,1))
$(eval $(call theme,web,Afei Web Theme))


### Translations ###
define translation
  define Package/luci-i18n-$(1)
    SECTION:=luci
    CATEGORY:=LuCI
    TITLE:=LuCI - Lua Configuration Interface
    URL:=http://luci.subsignal.org/
    MAINTAINER:=LuCI Development Team <luci@lists.subsignal.org>
    SUBMENU:=5. Translations
    TITLE:=$(if $(2),$(2),$(1))
  endef

  define Package/luci-i18n-$(1)/install
	$(call Package/luci/install/template,$$(1),i18n/$(1))
  endef

  ifneq ($(CONFIG_PACKAGE_luci-i18n-$(1)),)
    LUCI_SELECTED_MODULES+=i18n/$(1)
  endif

  LUCI_BUILD_PACKAGES += luci-i18n-$(1)
endef

$(eval $(call translation,chinese,Chinese (by Chinese Translators)))
$(eval $(call translation,hongkong,HongKong Chinese))
$(eval $(call translation,taiwan,Taiwan Chinese))


### Collections ###
define collection
  define Package/luci$(if $(1),-$(1))
    SECTION:=luci
    CATEGORY:=LuCI
    TITLE:=LuCI - Lua Configuration Interface
    URL:=http://luci.subsignal.org/
    MAINTAINER:=LuCI Development Team <luci@lists.subsignal.org>
    SUBMENU:=1. Collections
    TITLE:=$(if $(2),$(2),LuCI $(if $(1),$(1),general) collection)
    $(if $(3),DEPENDS:=$(3))
  endef

  define Package/luci$(if $(1),-$(1))/install
	true
  endef

  LUCI_BUILD_PACKAGES += luci$(if $(1),-$(1))
endef

$(eval $(call collection,,\
	Standard OpenWrt set including full admin with ppp support and the \
	default OpenWrt theme,\
	+uhttpd +luci-mod-admin-base +luci-mod-admin-CN-common +luci-theme-openwrt \
	+luci-app-firewall +luci-proto-core +luci-proto-ppp +libiwinfo-lua))


include $(INCLUDE_DIR)/package.mk

$(foreach b,$(LUCI_BUILD_PACKAGES),$(eval $(call BuildPackage,$(b))))
