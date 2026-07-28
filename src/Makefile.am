AM_CFLAGS = $(VINYLAPI_CFLAGS)

# Modules

vmod_LTLIBRARIES = \
	libvmod_curl.la

libvmod_curl_la_CFLAGS = $(AM_CFLAGS) $(CURL_CFLAGS)

libvmod_curl_la_LDFLAGS = $(VMOD_LDFLAGS) $(CURL_LIBS)

libvmod_curl_la_SOURCES = \
	vmod_curl.c \
	debug_flags.h

nodist_libvmod_curl_la_SOURCES = \
	vcc_curl_if.c \
	vcc_curl_if.h

DISTCLEANFILES = vmod_vcs_version.txt

vmod_vcs_version.txt: $(nodist_libvmod_hoailona_la_SOURCES)

@BUILD_VMOD_CURL@

# Test suite

AM_TESTS_ENVIRONMENT = \
	PATH="$(abs_builddir):$(VINYL_TEST_PATH):$(PATH)" \
	LD_LIBRARY_PATH="$(VINYL_LIBRARY_PATH)"
TEST_EXTENSIONS = .vtc
VTC_LOG_COMPILER = vinyltest -lv
AM_VTC_LOG_FLAGS = \
	-p vcl_path="$(abs_top_srcdir)/vcl:$(VINYLAPI_VCLDIR)" \
	-p vmod_path="$(abs_builddir)/.libs:$(vmoddir):$(VINYLAPI_VMODDIR)"

TESTS = \
	tests/test01.vtc \
	tests/test02.vtc \
	tests/test03.vtc \
	tests/test04.vtc \
	tests/test05.vtc \
	tests/test06.vtc \
	tests/test07.vtc \
	tests/test08.vtc \
	tests/test09.vtc \
	tests/test10.vtc \
	tests/test11.vtc \
	tests/test12.vtc \
	tests/test13.vtc \
	tests/test14.vtc

# Documentation

dist_doc_DATA = \
	vmod_curl.vcc \
	$(TESTS)

if HAVE_VCS_VMOD_VERSION
dist_doc_DATA += vmod_vcs_version.txt
endif

dist_man_MANS = \
	vmod_curl.3


.rst.1:
	$(AM_V_GEN) $(RST2MAN) $< $@
