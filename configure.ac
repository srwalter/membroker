#                                               -*- Autoconf -*-
# Process this file with autoconf to produce a configure script.
AC_PREREQ([2.68])
AC_INIT([membroker], [1.0])

AM_INIT_AUTOMAKE(subdir-objects foreign)
LT_INIT

# Checks for programs.
AC_PROG_CC
AM_PROG_CC_C_O

AC_ARG_ENABLE(server, AS_HELP_STRING([--disable-server], [build client library only]))
AS_IF([test "x$enable_server" != "xno"], [
       AM_CONDITIONAL(HAVE_SERVER, [true])
       # systemd
       PKG_PROG_PKG_CONFIG
       PKG_CHECK_MODULES(LIBSYSTEMD, libsystemd,
                         [AM_CONDITIONAL(HAVE_SYSTEMD, [true])],
                         [AM_CONDITIONAL(HAVE_SYSTEMD, [false])])
       ], [
       AM_CONDITIONAL(HAVE_SERVER, [false])
       AM_CONDITIONAL(HAVE_SYSTEMD, [false])
       ])
AM_COND_IF([HAVE_SYSTEMD],
           [AC_SUBST([systemdsystemunitdir],
                     [$($PKG_CONFIG --variable=systemdsystemunitdir systemd)])])

# Checks for libraries.
AC_CHECK_LIB(pthread, pthread_create)
# Reset LIBS. Don't want pthread on every link line
LIBS=

AC_CONFIG_FILES(Makefile membroker.pc membrokerserver.pc src/membroker.service)
AC_OUTPUT
