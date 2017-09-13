#
# This file and its contents are supplied under the terms of the
# Common Development and Distribution License ("CDDL"). You may
# only use this file in accordance with the terms of the CDDL.
#
# A full copy of the text of the CDDL should have accompanied this
# source. A copy of the CDDL is also available via the Internet at
# http://www.illumos.org/license/CDDL.
#

#
# Copyright 2017 Alexander Pyhalov
#

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=	mongodb
COMPONENT_SRC= $(COMPONENT_NAME)
COMPONENT_SUMMARY= MongoDB distributed document-oriented database
COMPONENT_PROJECT_URL=	https://www.mongodb.com/
COMPONENT_FMRI=	database/mongodb-head
COMPONENT_CLASSIFICATION= System/Databases
COMPONENT_LICENSE=	Apache v2.0
COMPONENT_LICENSE_FILE=	APACHE-2.0.txt

COMPONENT_MAJOR_VERSION=3.5

GIT=git
GIT_REPO=git://github.com/mongodb/mongo.git
GIT_BRANCH=master
GIT_CHANGESET=HEAD

COMPONENT_REVISION=$(shell cd $(COMPONENT_SRC); git rev-list HEAD --count)

CLEAN_PATHS += $(BUILD_DIR)
CLOBBER_PATHS += $(SOURCE_DIR)

include $(WS_MAKE_RULES)/justmake.mk

$(SOURCE_DIR)/.downloaded:
	@[ -d $(SOURCE_DIR) ] || \
	$(GIT) clone -b $(GIT_BRANCH) $(GIT_REPO) $(SOURCE_DIR)
	@cd $(SOURCE_DIR); $(GIT) checkout $(GIT_BRANCH); $(GIT) pull \
	  $(GIT_REPO); $(GIT) log -1 --format=%H > .downloaded

update:
	@[ -d $(SOURCE_DIR) ] || \
	$(GIT) clone -b $(GIT_BRANCH) $(GIT_REPO) $(SOURCE_DIR)
	cd $(SOURCE_DIR); $(GIT) pull $(GIT_REPO); \
	  [ $$($(GIT) log -1 --format=%H) == $$(cat .downloaded) ] || \
	  $(GIT) log -1 --format=%H > .downloaded

download:: $(SOURCE_DIR)/.downloaded

PATCH_DIR ?=    patches
PATCH_PATTERN ?=        *.patch
PATCHES =       $(shell find $(PATCH_DIR) $(PARFAIT_PATCH_DIR) -type f -name '$(PATCH_PATTERN)' \
                                2>/dev/null | sort) $(EXTRA_PATCHES)

$(SOURCE_DIR)/.patched: $(SOURCE_DIR)/.downloaded $(PATCHES)
	$(MKDIR) $(@D)
	cd $(SOURCE_DIR) && \
	$(GIT) checkout -f && \
	      $(GIT) clean -f
	for p in $(PATCHES); do \
	  $(GPATCH) -d $(@D) $(GPATCH_FLAGS) < $$p; \
	done
	@cd $(SOURCE_DIR); $(GIT) log -1 --format=%H > .downloaded
	$(TOUCH) $@

prep::  $(SOURCE_DIR)/.prep

$(SOURCE_DIR)/.prep: $(SOURCE_DIR)/.patched $(SOURCE_DIR)/.downloaded 
	$(TOUCH) $@

$(BUILD_DIR)/%/.built: $(SOURCE_DIR)/.patched

# MongoDB 3.4 wants GCC 7 compiler
GCC_ROOT=/usr/gcc/7

BUILD_TOOLS= $(BUILD_DIR)/tools/.built
INSTALL_TOOLS= $(BUILD_DIR)/tools/.installed

MONGO_PREFIX=usr/mongodb/head

GMAKE=scons

COMPONENT_BUILD_ARGS += TARGET_ARCH=x86_64
COMPONENT_BUILD_ARGS += CXXFLAGS="$(CXXFLAGS)"
COMPONENT_BUILD_ARGS += CC="$(CC)"
COMPONENT_BUILD_ARGS += CXX="$(CXX)"
COMPONENT_BUILD_ARGS += CFLAGS="$(CFLAGS)"
COMPONENT_BUILD_ARGS += LIBPATH=/usr/lib/$(MACH64)
COMPONENT_BUILD_ARGS += LINKFLAGS="$(LDFLAGS)"
COMPONENT_BUILD_ARGS += MONGO_VERSION=$(COMPONENT_MAJOR_VERSION).$(COMPONENT_REVISION)

COMPONENT_BUILD_ARGS += --prefix=$(PROTO_DIR)/$(MONGO_PREFIX)
COMPONENT_BUILD_ARGS += --use-system-zlib
COMPONENT_BUILD_ARGS += --ssl
COMPONENT_BUILD_ARGS += --release
# Fixes gcc 7 build
COMPONENT_BUILD_ARGS += --disable-warnings-as-errors
COMPONENT_BUILD_ARGS += --disable-ggdb

COMPONENT_BUILD_TARGETS=	all

COMPONENT_INSTALL_ARGS = $(COMPONENT_BUILD_ARGS)

$(BUILD_TOOLS):	$(BUILD_64)
	$(MKDIR) $(@D)/bin
	$(CP) -a $(SOURCE_DIR)/src/mongo/gotools/* $(@D) 
	cd $(@D) && /usr/bin/bash build.sh ssl
	$(TOUCH) $(@)

$(INSTALL_TOOLS): $(BUILD_TOOLS) $(INSTALL_64)
	$(CP) $(BUILD_DIR)/tools/bin/* $(PROTO_DIR)/$(MONGO_PREFIX)/bin
	$(TOUCH) $(@)

TEST_SUITES += core
TEST_SUITES += dbtest
TEST_SUITES += dur_jscore_passthrough
TEST_SUITES += generational_jstestfuzz
TEST_SUITES += jstestfuzz
TEST_SUITES += jstestfuzz_replication
TEST_SUITES += jstestfuzz_sharded
TEST_SUITES += replica_sets_jscore_passthrough
TEST_SUITES += unittests

# A bit of magic to replace spaces with commas
comma:= ,
empty:=
space:= $(empty) $(empty)

COMPONENT_TEST_CMD = $(PYTHON) buildscripts/resmoke.py \
				--continueOnFailure \
				--staggerJobs=on \
				--reportFailureStatus=fail \
				--dbpathPrefix=/tmp/db \
				--suites=$(subst $(space),$(comma),$(TEST_SUITES))

COMPONENT_TEST_TARGETS =

COMPONENT_TEST_TRANSFORMS +=	'-e "s/\[resmoke\][ -+0-9T:\.\-]*//"' \
				'-e "s/\s\s*[0-9][0-9]*\.[0-9][0-9]* seconds/ SEC seconds/"' \
				'-n ' \
				'-e "/Summary of all suites/,\\$$p"'

# Not strictly necessary, but simplifies jenkins job
$(TEST_64):	$(INSTALL_64) $(INSTALL_TOOLS)

build:		$(BUILD_64) $(BUILD_TOOLS)

install:	$(INSTALL_64) $(INSTALL_TOOLS)

test:		$(TEST_64)

REQUIRED_PACKAGES += SUNWcs
REQUIRED_PACKAGES += developer/build/scons
REQUIRED_PACKAGES += developer/gcc-7
REQUIRED_PACKAGES += developer/golang
REQUIRED_PACKAGES += library/python/typing-27
REQUIRED_PACKAGES += library/security/openssl
REQUIRED_PACKAGES += library/zlib
REQUIRED_PACKAGES += runtime/python-27
REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += system/library/boost
REQUIRED_PACKAGES += system/library/libpcap
REQUIRED_PACKAGES += system/library/math
