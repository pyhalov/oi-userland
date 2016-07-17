#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"), version 1.0.
# You may only use this file in accordance with the terms of version
# 1.0 of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source.  A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2016 Alexander Pyhalov
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= kvmadm
COMPONENT_VERSION= 0.10.3
COMPONENT_SUMMARY= Open source KVM administration tool for illumos based distributions
COMPONENT_SRC= $(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= $(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= \
  sha256:f1d4ea09a83cb97ad1596c22342aaf707667df36cd5b7449a319bfcb0670cfeb
COMPONENT_ARCHIVE_URL= \
  https://github.com/hadfl/kvmadm/releases/download/v$(COMPONENT_VERSION)/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL = http://www.kvmadm.org/
COMPONENT_FMRI=         system/qemu/kvmadm
COMPONENT_LICENSE_FILE= LICENSE
COMPONENT_LICENSE=      GPLv3
COMPONENT_CLASSIFICATION=       System/Virtualization

include $(WS_TOP)/make-rules/prep.mk
include $(WS_TOP)/make-rules/configure.mk
include $(WS_TOP)/make-rules/ips.mk

CONFIGURE_PREFIX=/opt/kvmadm

COMPONENT_PRE_CONFIGURE_ACTION = ($(CLONEY) $(SOURCE_DIR) $(@D))

CONFIGURE_OPTIONS += --enable-svcinstall=/lib/svc/manifest/system/
CONFIGURE_ENV += PERL=$(PERL)

build: $(BUILD_32)

install: $(INSTALL_32)

test: $(NO_TESTS)
