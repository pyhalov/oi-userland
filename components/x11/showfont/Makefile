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
# Copyright 2015 Aurelien Larcher
#

X11_CATEGORY=APP
include ../../../make-rules/shared-macros.mk
include $(WS_MAKE_RULES)/x11.mk

COMPONENT_NAME=     showfont
COMPONENT_VERSION=  1.0.5
COMPONENT_REVISION= 1
COMPONENT_FMRI=     x11/xfs/showfont
COMPONENT_SUMMARY=  showfont - font server data display utility
COMPONENT_ARCHIVE_HASH= \
  sha256:e9735c1c530b8a52edfab7415cc0fd7f8d2889095114f4cb689a27476461ac89

include $(WS_MAKE_RULES)/common.mk

REQUIRED_PACKAGES += system/library
REQUIRED_PACKAGES += x11/library/libfs
