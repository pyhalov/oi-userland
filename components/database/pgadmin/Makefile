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
# Copyright 2019 Alexander Pyhalov
#

BUILD_BITS=64
BUILD_STYLE=justmake

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= 	pgadmin4
COMPONENT_VERSION= 	4.15
COMPONENT_SUMMARY= 	pgAdmin4 administration and development GUI for PostgreSQL
COMPONENT_SRC= 		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE= 	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= \
  sha256:3131299953bf402b3d5d523c478c942dfb0ba619404a02c60908e467ca0d42bc
COMPONENT_ARCHIVE_URL= \
  http://ftp.postgresql.org/pub/pgadmin/pgadmin4/v$(COMPONENT_VERSION)/source/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL = http://www.pgadmin.org

PYTHON_VERSION=3.5

QTDIR=/usr/lib/qt/5.8
QTPATH.32=$(QTDIR)/bin
QTPATH.64=$(QTDIR)/bin/$(MACH64)

# Don't depend on host default pg_config
PATH=$(PG_BINDIR.$(BITS)):$(QTPATH.$(BITS)):/usr/sbin:/usr/bin

LDFLAGS+=   -L$(PG_LIBDIR.$(BITS))   -R$(PG_LIBDIR.$(BITS))
LDFLAGS+=   -lsocket -lnsl

CONFIGURE_OPTIONS += --with-pgsql=$(PG_HOME)

TEST_TARGET=$(NO_TESTS)
include $(WS_MAKE_RULES)/common.mk

QMAKE=$(QTPATH.$(BITS))/qmake

COMPONENT_BUILD_ENV+= LDFLAGS="$(LDFLAGS)"
COMPONENT_BUILD_ENV+= PYTHON_CONFIG=/usr/bin/python$(PYTHON_VERSION)-config

COMPONENT_PRE_BUILD_ACTION = \
        cd $(@D)/runtime; $(ENV) $(COMPONENT_BUILD_ENV) \
        $(QMAKE) CONFIG+=release QMAKE_CC="$(CC)" QMAKE_CXX="$(CXX)"

COMPONENT_BUILD_ACTION = \
        cd $(@D)/runtime; $(ENV) $(COMPONENT_BUILD_ENV) \
	$(GMAKE)

COMPONENT_INSTALL_ACTION = \
	$(MKDIR) $(PROTO_DIR)/usr/bin &&\
	$(CP) $(@D)/runtime/pgAdmin4 $(PROTO_DIR)/usr/bin

# Auto-generated dependencies
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += library/qt5
REQUIRED_PACKAGES += runtime/python-35
REQUIRED_PACKAGES += system/library
