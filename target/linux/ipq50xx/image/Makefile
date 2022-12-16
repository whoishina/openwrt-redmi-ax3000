include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/image.mk

define Device/Default
  PROFILES := Default
  KERNEL_DEPENDS = $$(wildcard $(DTS_DIR)/$$(DEVICE_DTS).dts)
  KERNEL_LOADADDR := 0x41208000
  IMAGES := sysupgrade.tar
  IMAGE/sysupgrade.tar := sysupgrade-tar | append-metadata
endef

define Device/FitImage
  KERNEL_SUFFIX := -fit-uImage.itb
  KERNEL = kernel-bin | gzip | fit gzip $$(DTS_DIR)/$$(DEVICE_DTS).dtb
  KERNEL_NAME := Image
endef

define Device/UbiFit
  KERNEL_IN_UBI := 1
  IMAGES := nand-factory.ubi nand-sysupgrade.bin
  IMAGE/nand-factory.ubi := append-ubi
  IMAGE/nand-sysupgrade.bin := sysupgrade-tar | append-metadata
endef

define Device/redmi_ax3000
  $(call Device/FitImage)
  $(call Device/UbiFit)
  DEVICE_VENDOR := Redmi
  DEVICE_MODEL := AX3000
  DEVICE_DTS := qcom-ipq5018-ax3000
  BLOCKSIZE := 128k
  PAGESIZE := 2048
  DEVICE_DTS_CONFIG := config@mp02.1
  ROOTFSNAME_IN_UBI := ubi_rootfs
  IMAGES := nand-factory.ubi
endef
TARGET_DEVICES += redmi_ax3000

$(eval $(call BuildImage))
