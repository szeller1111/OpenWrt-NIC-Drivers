#
# Drivers Copyright (C) 2019 Intel Corporation
#
# This is free software, licensed under the GNU General Public License v2.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=kmod-igb-intel
PKG_VERSION:=5.14.16
PKG_RELEASE:=1

PKG_SOURCE:=igb-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://sourceforge.net/projects/e1000/files/igb%20stable/$(PKG_VERSION)/
PKG_MD5SUM:=eaacff1aa1c82c275d9733bad6234d76


include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

PKG_UNPACK:=zcat $(DL_DIR)/$(PKG_SOURCE) | $(TAR) -C $(PKG_BUILD_DIR) --strip-components=1 -xf -

MAKE_PATH:=src

MAKE_VARS:= \
  KSRC="$(LINUX_DIR)" 

MAKE_OPTS:= \
  ARCH="$(LINUX_KARCH)" \
  CROSS_COMPILE="$(KERNEL_CROSS)" 

define KernelPackage/igb-intel
  SUBMENU:=Network Devices
  TITLE:=Intel igb drivers - out of tree version
  DEPENDS:=+kmod-ptp @PCI_SUPPORT 
  KCONFIG:=CONFIG_IGB \
    CONFIG_IGB_HWMON=n \
    CONFIG_IGB_DCA=n
  FILES:=$(PKG_BUILD_DIR)/src/igb.ko
  AUTOLOAD:=$(call AutoLoad,35,igb)
endef

define KernelPackage/igb-intel/description
 Kernel modules for Intel igb out of tree drivers
 Warning: do not select the core package kmod-igb as this is an
 updated version of the igb driver that shares the same module name
endef

$(eval $(call KernelPackage,igb-intel))
