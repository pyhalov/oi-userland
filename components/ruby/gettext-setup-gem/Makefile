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

include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=		gettext-setup-gem
COMPONENT_VERSION=	0.28
COMPONENT_SUMMARY=	A simple gem to set up i18n for Ruby projects
COMPONENT_SRC=		$(COMPONENT_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=	$(COMPONENT_SRC).tar.gz
COMPONENT_ARCHIVE_HASH=	\
    sha256:ef2fa58570fd2fd685f3ae7e4cb84b07c0333dfe23b3d148c094835393362738
COMPONENT_ARCHIVE_URL=	https://github.com/puppetlabs/gettext-setup-gem/archive/$(COMPONENT_VERSION).tar.gz
COMPONENT_PROJECT_URL=  https://github.com/puppetlabs/gettext-setup-gem
COMPONENT_FMRI=		livrary/ruby/gettext-setup-gem
COMPONENT_CLASSIFICATION=	Development/Ruby
COMPONENT_LICENSE=	Apache v2.0

include $(WS_MAKE_RULES)/prep.mk
include $(WS_MAKE_RULES)/ips.mk
include $(WS_MAKE_RULES)/gem.mk
include $(WS_MAKE_RULES)/ruby.mk

GEMSPEC=gettext-setup

GEM_INSTALL_ACTION= (cd $(@D); $(GEM) install $(GEM_INSTALL_ARGS) $(GEMSPEC))

ASLR_MODE = $(ASLR_NOT_APPLICABLE)

# common targets
build:		$(BUILD_32)

install:	$(INSTALL_32)

test:		$(NO_TEST)

REQUIRED_PACKAGES += runtime/ruby-23
