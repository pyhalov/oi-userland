#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL)". You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2016 Alexander Pyhalov
#

BUILD_BITS = 32
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		gnome-doc-utils
COMPONENT_VERSION=	0.20.10
COMPONENT_REVISION=	3
COMPONENT_PROJECT_URL=	http://www.gnome.org
COMPONENT_SUMMARY=	Documentation utilities for GNOME
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.xz
COMPONENT_ARCHIVE_HASH=	\
    sha256:cb0639ffa9550b6ddf3b62f3b1add92fb92ab4690d351f2353cffe668be8c4a6
COMPONENT_ARCHIVE_URL=	http://ftp.gnome.org/pub/GNOME/sources/$(COMPONENT_NAME)/0.20/$(COMPONENT_ARCHIVE)

PYTHON_VERSION = 3.5

include $(WS_MAKE_RULES)/common.mk

PATH=$(PATH.gnu)

#COMPONENT_PREP_ACTION = (cd $(@D) && autoreconf -fi)

# Missing files in build dir for xml2po without this.
COMPONENT_PRE_CONFIGURE_ACTION = ($(CLONEY) $(SOURCE_DIR) $(@D))

CONFIGURE_OPTIONS+=	--sysconfdir=/etc

CONFIGURE_ENV+=  PERL=$(PERL)
CONFIGURE_ENV+=  PYTHON=$(PYTHON)
CONFIGURE_ENV+=  am_cv_python_pythondir="$(PYTHON.$(PYTHON_VERSION).VENDOR_PACKAGES.32)"

COMPONENT_BUILD_ARGS += V=1

COMPONENT_POST_INSTALL_ACTION +=	cd  $(PROTO_DIR)/$(PYTHON_VENDOR_PACKAGES)/xml2po && \
					$(PYTHON) -m compileall . && \
					cd $(PROTO_DIR)/$(PYTHON_VENDOR_PACKAGES)/xml2po/modes && \
					$(PYTHON) -m compileall . 

REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += library/python/libxml2-27
REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += shell/bash
