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
# Copyright 2020 Andreas Wacknitz
#

BUILD_STYLE = archive
include ../../../make-rules/shared-macros.mk

COMPONENT_NAME=				jetbrains-mono
COMPONENT_SUMMARY=			A typeface for developers
COMPONENT_VERSION= 			2.001
IPS_COMPONENT_VERSION=		2.0.0.1
COMPONENT_PROJECT_URL= 		https://www.jetbrains.com/lp/mono/
COMPONENT_SRC_NAME=			JetBrainsMono
COMPONENT_SRC=				$(COMPONENT_SRC_NAME)-$(COMPONENT_VERSION)
COMPONENT_ARCHIVE=      	$(COMPONENT_SRC).zip
COMPONENT_ARCHIVE_URL=		https://github.com/JetBrains/JetBrainsMono/archive/v${COMPONENT_VERSION}.zip
COMPONENT_ARCHIVE_HASH= 	sha256:dedeed7f466c64cf1cfb1b21cb5548f68ed6db9d9eda94a2bf0af17cf9a6b2a8
COMPONENT_LICENSE=			Apache 2.0
COMPONENT_LICENSE_FILE=		LICENSE

FONT_TYPE = TTF

include $(WS_MAKE_RULES)/font.mk

COMPONENT_FONT_SRC_DIR     =
COMPONENT_FONT_FILES      += ttf/*.ttf
COMPONENT_FONTCONF_SRC_DIR =
COMPONENT_FONTCONF_FILES   =

