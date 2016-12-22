ACLOCAL_AMFLAGS = -I m4

BINARCHDIR = bin/$(GAPARCH)
GAPINSTALLLIB = $(abs_top_srcdir)/$(BINARCHDIR)/zeromq.so

lib_LTLIBRARIES = zeromq.la

zeromq_la_SOURCES = \
    src/zmqgap.c \
    src/zmqgap.h
zeromq_la_CPPFLAGS = $(GAP_CPPFLAGS) -DCONFIG_H $(ZEROMQ_CPPFLAGS)
zeromq_la_LDFLAGS = -module -avoid-version
if SYS_IS_CYGWIN
zeromq_la_LDFLAGS += -no-undefined -version-info 0:0:0 -Wl,$(GAPROOT)/bin/$(GAPARCH)/gap.dll
endif
zeromq_la_LDFLAGS += $(ZEROMQ_LDFLAGS) $(ZEROMQ_LIBS)


all-local: zeromq.la
	$(mkdir_p) $(top_srcdir)/$(BINARCHDIR)
if SYS_IS_CYGWIN
	cp .libs/zeromq.dll $(GAPINSTALLLIB)
else
	cp .libs/zeromq.so $(GAPINSTALLLIB)
endif
	@echo "SUCCESS!"

distclean-local:
	rm -rf bin
	(cd doc ; ./clean)

doc:	doc/manual.six

doc/manual.six: doc/*.xml PackageInfo.g
	($(GAPROOT)/bin/gap.sh -A makedoc.g)