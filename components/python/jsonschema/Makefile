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
# Copyright 2017 Gary Mills
# Copyright (c) 2015 Alexander Pyhalov
#

BUILD_BITS=NO_ARCH
BUILD_STYLE=setup.py
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		jsonschema
COMPONENT_VERSION=	2.4.0
COMPONENT_REVISION=	4
COMPONENT_PROJECT_URL=	https://pypi.python.org/pypi/jsonschema
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
    sha256:1298a2f1b2f4c4a7b921cccd159e4e42f6d7b0fb75c86c0cdecfc71f061833fa
COMPONENT_ARCHIVE_URL=	https://pypi.python.org/packages/source/j/jsonschema/$(COMPONENT_ARCHIVE)

PYTHON_VERSIONS=	2.7 3.5

TEST_TARGET=		$(NO_TESTS)
include $(WS_MAKE_RULES)/common.mk

COMPONENT_POST_INSTALL_ACTION = \
        (cd $(PROTO_DIR)/usr/bin ; \
                $(MV) jsonschema jsonschema-$(PYTHON_VERSION); )


# Auto-generated dependencies
REQUIRED_PACKAGES += library/python/setuptools-27
REQUIRED_PACKAGES += library/python/setuptools-35
REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += runtime/python-35
