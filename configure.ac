#
# configure.ac
#
# Written by: Francesco Salvestrini <f DOT salvestrini AT nextworks DOT it>
#

AC_INIT([RINA raffig Generator],
        m4_esyscmd([build-aux/git-version-gen .tarball-version]),
        [f.salvestrini@nextworks.it],
        [rina-tgen],
        [http://irati.eu])

AC_PREREQ([2.68])

AC_CONFIG_HEADERS([src/config.h])
AC_CONFIG_SRCDIR([src/main.cc])
AC_CONFIG_AUX_DIR([build-aux])
AC_CONFIG_MACRO_DIR([m4])

AC_CANONICAL_BUILD
AC_CANONICAL_HOST
AC_CANONICAL_TARGET

AM_INIT_AUTOMAKE([1.11.1 tar-pax foreign std-options -Wall])

AC_PROG_SED
AC_PROG_GREP
AC_PROG_MKDIR_P
AC_PROG_LN_S

AC_PATH_PROG([FMT],  [fmt],  [/bin/false])
AC_PATH_PROG([SORT], [sort], [/bin/false])
AC_PATH_PROG([UNIQ], [uniq], [/bin/false])
AC_PATH_PROG([GIT],  [git],  [/bin/false])

AC_PROG_CPP
AC_PROG_CC
AM_PROG_CC_C_O

AC_PROG_CXXCPP
AC_PROG_CXX
AC_PROG_CXX_C_O

AC_CXX_HAVE_SSTREAM
AC_CXX_HAVE_STRSTREAM
AC_CXX_HAVE_LONG_LONG

# Just to avoid warning from libtool 1.14
AM_PROG_AR
LT_INIT

CPPFLAGS_EXTRA=""
CXXFLAGS_EXTRA=""

AX_CHECK_COMPILE_FLAG([ -Wall ], [
    CPPFLAGS_EXTRA="$CPPFLAGS_EXTRA -Wall"
])
AX_CHECK_COMPILE_FLAG([ -Wformat ], [
    CPPFLAGS_EXTRA="$CPPFLAGS_EXTRA -Wformat"
])
AX_CHECK_COMPILE_FLAG([ -Wnon-virtual-dtor ], [
    CPPFLAGS_EXTRA="$CPPFLAGS_EXTRA -Wnon-virtual-dtor"
])
AX_CHECK_COMPILE_FLAG([ -Woverloaded-virtual ], [
    CPPFLAGS_EXTRA="$CPPFLAGS_EXTRA -Woverloaded-virtual"
])
AX_CHECK_COMPILE_FLAG([ -Wextra ], [
    CPPFLAGS_EXTRA="$CPPFLAGS_EXTRA -Wextra"
])
AX_CHECK_COMPILE_FLAG([ -Werror ], [
    CPPFLAGS_EXTRA="$CPPFLAGS_EXTRA -Werror"
])
AX_CHECK_COMPILE_FLAG([ -Wfatal-errors ], [
    CPPFLAGS_EXTRA="$CPPFLAGS_EXTRA -Wfatal-errors"
])

want_debug=no
AX_SELECTOR_ENABLE([debug],[
    want_debug=yes
],[
    want_debug=no
])
AS_IF([test "$want_debug" = "yes"],[
    AX_CHECK_COMPILE_FLAG([ -g ], [
        CXXFLAGS_EXTRA="$CXXFLAGS_EXTRA -g"
    ])
    AS_IF([`echo $CXXFLAGS|$GREP '\\\-O2'`],[
        AC_MSG_NOTICE([Patching flags])
        CXXFLAGS="`echo $CXXFLAGS | $SED -e 's|-O2||'`"
        AC_MSG_NOTICE([Flags are now '$CXXFLAGS'])
    ])
    AX_CHECK_COMPILE_FLAG([ -O0 ], [
        CXXFLAGS_EXTRA="$CXXFLAGS_EXTRA -O0"
    ])
    AX_CHECK_COMPILE_FLAG([ -fno-inline ], [
        CXXFLAGS_EXTRA="$CXXFLAGS_EXTRA -fno-inline"
    ])
])

AC_SUBST(CPPFLAGS_EXTRA, $CPPFLAGS_EXTRA)
AC_SUBST(CXXFLAGS_EXTRA, $CXXFLAGS_EXTRA)

PKG_PROG_PKG_CONFIG([0.26])

#PKG_CHECK_MODULES([LIBRINA], [librina >= 0.2.0],, [
#    AC_MSG_ERROR([Your system lacks of librina support])
#])
## FIXME: A cleaner solution would be better
#AC_SUBST([LIBRINA_VERSION],`pkg-config --modversion librina`)

AC_CONFIG_FILES([
    Makefile

    src/Makefile
    src/tclap/Makefile
])

AC_OUTPUT