# Copyright © 2014 Broadcom
#
# Permission is hereby granted, free of charge, to any person obtaining a
# copy of this software and associated documentation files (the "Software"),
# to deal in the Software without restriction, including without limitation
# the rights to use, copy, modify, merge, publish, distribute, sublicense,
# and/or sell copies of the Software, and to permit persons to whom the
# Software is furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice (including the next
# paragraph) shall be included in all copies or substantial portions of the
# Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL
# THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
# FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS
# IN THE SOFTWARE.

include Makefile.sources
include $(top_srcdir)/src/gallium/Automake.inc

if USE_VC4_SIMULATOR
SIM_LDFLAGS = -lsimpenrose
endif

AM_CFLAGS = \
	-I$(top_builddir)/src/compiler/nir \
	-I$(top_srcdir)/include/drm-uapi \
	-I$(top_builddir)/src \
	-I$(top_srcdir)/src/broadcom \
	-I$(top_builddir)/src/broadcom \
	$(LIBDRM_CFLAGS) \
	$(GALLIUM_DRIVER_CFLAGS) \
	$(SIM_CFLAGS) \
	$(VALGRIND_CFLAGS) \
	$()

noinst_LTLIBRARIES = libvc4.la

libvc4_la_SOURCES = $(C_SOURCES)

libvc4_la_LIBADD = \
	$(SIM_LIB) \
	$()

if HAVE_ARM_ASM
noinst_LTLIBRARIES += libvc4_neon.la
libvc4_la_LIBADD += libvc4_neon.la
libvc4_neon_la_SOURCES = $(NEON_C_SOURCES)
libvc4_neon_la_CFLAGS = $(AM_CFLAGS) -mfpu=neon
endif

libvc4_la_LDFLAGS = $(SIM_LDFLAGS)

EXTRA_DIST = kernel/README meson.build
