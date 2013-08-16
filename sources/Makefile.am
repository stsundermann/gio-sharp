RAW_API = $(ASSEMBLY_NAME)-api.raw
API = $(ASSEMBLY_NAME)-api.xml
METADATA = $(ASSEMBLY_NAME).metadata
DLL = $(top_srcdir)/out/$(ASSEMBLY_NAME).dll
DLLMAP = $(top_srcdir)/out/$(ASSEMBLY_NAME).dll.config
GLUEDIR = $(srcdir)/glue

gapidir = $(GAPIXMLDIR)
gapi_DATA = $(API)

# Add any extra source files you need here
sources = custom/FileEnumerator.cs

build_sources = AssemblyInfo.cs $(sources)

CLEANFILES = $(DLL) generated-stamp generated/*.cs $(API)

DISTCLEANFILES = AssemblyInfo.cs $(DLLMAP)

noinst_DATA = $(DLL)

EXTRA_DIST = \
	$(RAW_API) \
	$(sources) \
	$(METADATA) \
	AssemblyInfo.cs.in \
	$(ASSEMBLY_NAME).snk

all: generated-stamp $(ASSEMBLY)

$(API): $(srcdir)/$(RAW_API) $(srcdir)/$(METADATA)
	cp $(srcdir)/$(RAW_API) $(API)
	chmod u+w $(API)
	$(GAPI_FIXUP) --api=$(srcdir)/$(API) --metadata=$(srcdir)/$(METADATA)

generated-stamp: $(API)
	 $(GAPI_CODEGEN) --generate $(srcdir)/$(API) $(GTK_SHARP_CFLAGS) \
		--outdir=generated \
		--glue-filename=$(GLUEDIR)/generated.c --gluelib-name=libgiosharpglue-2.36.0.so \
		--glue-includes=/usr/include/gio-unix-2.0/gio/gdesktopappinfo.h,/usr/include/gio-unix-2.0/gio/gfiledescriptorbased.h,/usr/include/gio-unix-2.0/gio/gunixconnection.h,/usr/include/gio-unix-2.0/gio/gunixcredentialsmessage.h,/usr/include/gio-unix-2.0/gio/gunixfdlist.h,/usr/include/gio-unix-2.0/gio/gunixfdmessage.h,/usr/include/gio-unix-2.0/gio/gunixinputstream.h,/usr/include/gio-unix-2.0/gio/gunixmounts.h,/usr/include/gio-unix-2.0/gio/gunixoutputstream.h,/usr/include/gio-unix-2.0/gio/gunixsocketaddress.h,gio/gio.h, --gapidir=$(gapidir) \
	 	--assembly-name=$(ASSEMBLY_NAME) && touch generated-stamp

$(DLL): $(build_sources) generated-stamp
	$(CSC) -nowarn:169 -unsafe -target:library $(GTK_SHARP_LIBS) \
		$(build_sources)  generated/*.cs -out:$(DLL)

install-data-local:
	echo "$(GACUTIL) /i $(DLL) /f $(GACUTIL_FLAGS)";  \
        $(GACUTIL) /i $(DLL) /f $(GACUTIL_FLAGS) || exit 1;

uninstall-local:
	echo "$(GACUTIL) /u $(ASSEMBLY_NAME) $(GACUTIL_FLAGS)"; \
        $(GACUTIL) /u $(ASSEMBLY_NAME) $(GACUTIL_FLAGS) || exit 1;
