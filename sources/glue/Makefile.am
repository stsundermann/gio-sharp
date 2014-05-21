lib_LTLIBRARIES = libgiosharpglue-2.40.0.la

libgiosharpglue_2_40_0_la_SOURCES =

nodist_libgiosharpglue_2_40_0_la_SOURCES = generated.c

libgiosharpglue_2_40_0_la_LDFLAGS = -module -avoid-version -no-undefined

libgiosharpglue_2_40_0_la_LIBADD = $(GIO_LIBS)

INCLUDES = $(GIO_CFLAGS) -I$(top_srcdir)

libgiosharpglue.dll: $(libgiosharpglue_2_40_0_la_OBJECTS) libgiosharpglue.rc libgiosharpglue.def
	./build-dll libgiosharpglue $(VERSION)

CLEANFILES = lib*.a lib*.dll

EXTRA_DIST =
