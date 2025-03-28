## Process this file with automake to produce Makefile.in

SUBDIRS = data

NULL =

AM_CPPFLAGS =                                                                  \
	-I$(top_builddir) -I$(top_srcdir)                                      \
	-DPACKAGE_LIBEXEC_DIR=\""$(libexecdir)"\"                              \
	-DPACKAGE_SYSCONF_DIR=\""$(sysconfdir)"\"                              \
	-DPACKAGE_DATA_DIR=\""$(datadir)"\"                                    \
	-DPACKAGE_BIN_DIR=\""$(bindir)"\"                                      \
	-DPACKAGE_LOCALSTATE_DIR=\""$(localstatedir)"\"                        \
	-DPACKAGE_LOCALE_DIR=\""$(localedir)"\"                                \
	-DPACKAGE_LIB_DIR=\""$(libdir)"\"                                      \
	-D_POSIX_PTHREAD_SEMANTICS -D_REENTRANT                                \
	-DUDISKS_COMPILATION                                                   \
	$(POLKIT_GOBJECT_1_CFLAGS)                                             \
	$(GLIB_CFLAGS)                                                         \
	$(GIO_CFLAGS)                                                          \
	$(GUDEV_CFLAGS)                                                        \
	$(BLOCKDEV_CFLAGS)                                                     \
	$(WARN_CFLAGS)                                                         \
	$(NULL)

if ENABLE_DAEMON

BTRFS_MODULE_DIR = $(top_srcdir)/modules/btrfs

MODULE_SO = libudisks2_btrfs.so

BUILT_SOURCES =                                                                \
	$(NULL)

libudisks2_btrfsdir = $(libdir)/udisks2/modules
libudisks2_btrfs_LTLIBRARIES = libudisks2_btrfs.la

libudisks2_btrfsincludedir = $(includedir)/udisks2/udisks

libudisks2_btrfs_la_SOURCES =                                                  \
	$(BUILT_SOURCES)                                                       \
	udiskslinuxmodulebtrfs.h                                               \
	udiskslinuxmodulebtrfs.c                                               \
	udiskslinuxfilesystembtrfs.h                                           \
	udiskslinuxfilesystembtrfs.c                                           \
	udiskslinuxmanagerbtrfs.h                                              \
	udiskslinuxmanagerbtrfs.c                                              \
	udisksbtrfstypes.h                                                     \
	udisksbtrfsutil.h                                                      \
	udisksbtrfsutil.c                                                      \
	$(NULL)

libudisks2_btrfs_la_CPPFLAGS =                                                 \
	$(AM_CPPFLAGS)                                                         \
	-DG_LOG_DOMAIN=\"libudisks2-btrfs\"                                    \
	$(NULL)

libudisks2_btrfs_la_CFLAGS =                                                   \
	$(GLIB_CFLAGS)                                                         \
	$(GIO_CFLAGS)                                                          \
	$(GUDEV_CFLAGS)                                                        \
	$(POLKIT_GOBJECT_1_CFLAGS)                                             \
	$(BLOCKDEV_CFLAGS)                                                     \
	$(NULL)

libudisks2_btrfs_la_LDFLAGS =                                                  \
	-export-dynamic                                                        \
	-avoid-version                                                         \
	-module                                                                \
	-no-undefined                                                          \
	-export-symbols-regex                                                  \
	 '^udisks_.*|g_io_module_load|g_io_module_unload|g_io_module_query'    \
	$(NULL)

libudisks2_btrfs_la_LIBADD =                                                   \
	$(top_builddir)/src/libudisks-daemon.la                                \
	$(GLIB_LIBS)                                                           \
	$(GIO_LIBS)                                                            \
	$(GUDEV_LIBS)                                                          \
	$(POLKIT_GOBJECT_1_LIBS)                                               \
	$(BLOCKDEV_LIBS)                                                       \
	$(NULL)

all-local: module_link

endif # ENABLE_DAEMON

# ------------------------------------------------------------------------------

CLEANFILES =

EXTRA_DIST =                                                                   \
	$(NULL)

include ../Makefile.uninstalled

dist-hook:
	(for i in $(BUILT_SOURCES); do rm -f $(distdir)/$$i; done)

clean-local: module_unlink
	rm -f *~ $(BUILT_SOURCES)
