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
# Copyright 2017 Alexander Pyhalov
#

BUILD_BITS=64
BUILD_STYLE=cmake
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME= 	pgAgent
COMPONENT_VERSION= 	4.0.0
COMPONENT_SUMMARY= 	pgAgent job scheduler for PostgreSQL
COMPONENT_SRC= 		$(COMPONENT_NAME)-$(COMPONENT_VERSION)-Source
COMPONENT_ARCHIVE= 	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH= \
  sha256:57bd047401629533ac6c5238bc94026f0ea0bf9f1f33a2bccc754b27132ea7e8
COMPONENT_ARCHIVE_URL= \
  https://ftp.postgresql.org/pub/pgadmin/pgagent/$(COMPONENT_ARCHIVE)
COMPONENT_PROJECT_URL = http://www.pgadmin.org/
COMPONENT_FMRI=	database/postgres/pgagent
COMPONENT_CLASSIFICATION=	System/Databases
COMPONENT_LICENSE=	MIT
COMPONENT_LICENSE_FILE=	LICENSE

# Don't depend on host default pg_config
PATH=		$(PG_BINDIR.$(BITS)):/usr/sbin:/usr/bin

include $(WS_MAKE_RULES)/common.mk

CFLAGS += -pthread
CXXFLAGS += -pthread

COMPONENT_PRE_CMAKE_ACTION =        (cp -a $(SOURCE_DIR)/* $(@D))

POSTGRESQL_VERSIONS = 9.6 10 11 12

CMAKE_OPTIONS = -D STATIC_BUILD=NO
# Don't depend on host default pg_config
CMAKE_OPTIONS += -D CMAKE_PROGRAM_PATH=$(PG_BINDIR.$(BITS)):/usr/sbin:/usr/bin
CMAKE_OPTIONS += -D CMAKE_BUILD_WITH_INSTALL_RPATH="TRUE"
CMAKE_OPTIONS += -D CMAKE_INSTALL_RPATH_USE_LINK_PATH="TRUE"

CMAKE_OPTIONS += -D CMAKE_INSTALL_PREFIX=/usr

COMPONENT_POST_INSTALL_ACTION += ( \
			cd $(PROTO_DIR)/usr/postgres; \
			for v in $(POSTGRESQL_VERSIONS); do \
				$(CP) -r 9.5  $$v; \
			done )

# Auto-generated dependencies
REQUIRED_PACKAGES += $(GXX_RUNTIME_PKG)
REQUIRED_PACKAGES += $(GCC_RUNTIME_PKG)
REQUIRED_PACKAGES += $(PG_LIBRARY_PKG)
REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/boost
