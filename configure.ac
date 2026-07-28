AC_PREREQ(2.69)
AC_INIT([libvmod-curl], [1.0.4])
AC_COPYRIGHT([Copyright (c) 2011-2016 Varnish Software])
AC_CONFIG_MACRO_DIR([m4])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_SRCDIR(src/vmod_curl.vcc)
AM_CONFIG_HEADER(config.h)

AC_CANONICAL_SYSTEM
AC_LANG(C)

AM_INIT_AUTOMAKE([1.12 -Wall -Werror foreign color-tests parallel-tests])
AM_SILENT_RULES([yes])

AC_GNU_SOURCE
AC_PROG_CC
AC_PROG_CC_STDC
if test "x$ac_cv_prog_cc_c99" = xno; then
	AC_MSG_ERROR([Could not find a C99 compatible compiler])
fi
AC_PROG_CPP

AC_PROG_INSTALL
AC_PROG_LIBTOOL
AC_PROG_MAKE_SET

AC_ARG_VAR([RST2MAN], [the program to build manuals from reStructuredText])
AC_CHECK_PROGS(RST2MAN, [rst2man rst2man.py])

# Check for pkg-config
PKG_PROG_PKG_CONFIG
PKG_CHECK_MODULES([CURL], [libcurl])

# Checks for header files.
AC_HEADER_STDC
AC_CHECK_HEADERS([sys/stdlib.h])

# Check for python
AC_CHECK_PROGS(PYTHON, [python3 python3.1 python3.2 python2.7 python2.6 python2.5 python2 python], "no")
if test "x$PYTHON" = "xno"; then
	AC_MSG_ERROR([Python is needed to build this vmod, please install python.])
fi

VINYL_PREREQ([9.0.0])
VINYL_VMODS([curl])

AX_CURLOPT_CHECK([CURLOPT_TIMEOUT_MS])
AX_CURLOPT_CHECK([CURLOPT_CONNECTTIMEOUT_MS])
AX_CURLOPT_CHECK([CURLOPT_UNIX_SOCKET_PATH])

AM_PROG_AR

LT_PREREQ([2.2.6])
LT_INIT([dlopen disable-static])

AC_CONFIG_FILES([
	Makefile
	src/Makefile
])

AC_CHECK_PROG([HAVE_GIT], [git], [yes], [no])
if test "x$HAVE_GIT" = "xyes"; then
	if git rev-parse --git-dir >/dev/null 2>&1; then
		HAVE_GIT_REPO=yes
	else
		HAVE_GIT_REPO=no
	fi
else
	HAVE_GIT_REPO=no
fi
AM_CONDITIONAL([HAVE_VCS_VMOD_VERSION], [test -f "src/vmod_vcs_version.txt" || test "x$HAVE_GIT_REPO" = "xyes"])
if test "x$HAVE_GIT_REPO" != "xyes" && test ! -f "src/vmod_vcs_version.txt"; then
   AC_MSG_WARN([Building without version control metadata - vmod_vcs_version.txt will be unavailable])
fi

AC_OUTPUT

AS_ECHO("
	==== $PACKAGE_STRING ====

	vinyl:	        $VINYL_VERSION
	prefix:		$prefix
	vmoddir:	$vmoddir
	vcldir:		$vcldir
	pkgvcldir:	$pkgvcldir

	compiler:	$CC
	cflags:		$CFLAGS
	ldflags:	$LDFLAGS
")
