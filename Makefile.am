ACLOCAL_AMFLAGS = -I m4
AM_CPPFLAGS = $(PGINCLUDES) $(all_includes)

noinst_LTLIBRARIES = libiplike_common.la
libiplike_common_la_SOURCES = iplike.c
libiplike_common_la_LDFLAGS = $(PGLIBS)

plugindir = @PGPLUGINDIR@
plugin_LTLIBRARIES = iplike.la

iplike_la_SOURCES =
iplike_la_LIBADD = libiplike_common.la
iplike_la_LDFLAGS = -module -avoid-version -no-undefined $(PG_BUNDLE_LOADER)

sbin_SCRIPTS = install_iplike.sh

check_PROGRAMS = iplike
iplike_SOURCES = iplike-cmd.c
iplike_LDADD = libiplike_common.la
iplike_LDFLAGS = $(CLI_LDFLAGS)

TESTS = tests.sh

MAINTAINERCLEANFILES = aclocal.m4 config.guess config.h.in config.sub configure depcomp install-sh ltmain.sh Makefile.in missing *~

EXTRA_DIST = m4/* debian/po/* debian/* $(TESTS) *.dat

if MAKE_RPMS
rpm: @RPM_TARGET@

.PHONY: rpm

EXTRA_DIST += iplike.spec

$(RPM_TARGET): $(DISTFILES)
	${MAKE} dist
	-mkdir -p $(RPM_DIR)/SRPMS
	-mkdir -p `dirname $(RPM_TARGET)`
	$(RPMBUILD_PROG) $(RPM_ARGS) $(RPM_TARBALL)
	@echo "$(RPM_TARGET) created"
endif
