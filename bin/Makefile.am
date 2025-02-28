## Process this file with automake to create Makefile.in

SUBDIRS = FvwmPrompt

bin_PROGRAMS = fvwm-root
fvwm_root_SOURCE= fvwm-root.c
fvwm_root_DEPENDENCIES = $(top_builddir)/libs/libfvwm3.a

bin_SCRIPTS = fvwm-perllib \
	fvwm-convert-2.6 \
	fvwm-menu-xlock fvwm-menu-directory \
	fvwm-menu-desktop \
	FvwmCommand

man_MANS = fvwm-menu-xlock.1 fvwm-menu-directory.1 fvwm-perllib.1

LDADD = -L$(top_builddir)/libs $(X_LIBS) -lfvwm3 $(xpm_LIBS) $(Xcursor_LIBS) \
	$(X_PRE_LIBS) -lXext -lX11 -lm $(X_EXTRA_LIBS) $(Xrender_LIBS) \
	$(Xcursor_LIBS) $(png_LIBS) $(rsvg_LIBS) $(XRandR_LIBS) \
	$(XFT_LIBS)
AM_CPPFLAGS = -I$(top_srcdir) $(xpm_CFLAGS) $(X_CFLAGS) $(png_CFLAGS) \
	$(rsvg_CFLAGS) $(XRandR_CFLAGS) $(XFT_CFLAGS)

configdir = @FVWM_DATADIR@
config_DATA = fvwm-menu-desktop-config.fpl

EXTRA_DIST = fvwm-menu-desktop-config.fpl $(man_MANS) FvwmPrompt

## The long generation for *.1 is to make both pod2man and 'make -j' happy.

_fvwm-menu-xlock.1: fvwm-menu-xlock
	@TMP=tmp-$$$$ NAME=fvwm-menu-xlock && (\
	mkdir $$TMP && \
	cp $$NAME.in $$TMP/$$NAME && \
	pod2man --center "Fvwm Utilities" --release "@VERSION@@VERSIONINFO@" \
		--name $$NAME $$TMP/$$NAME >$$TMP/$$NAME.1 && \
	mv $$TMP/$$NAME.1 .; \
	rm -rf $$TMP)

_fvwm-menu-directory.1: fvwm-menu-directory
	@TMP=tmp-$$$$ NAME=fvwm-menu-directory && (\
	mkdir $$TMP && \
	cp $$NAME.in $$TMP/$$NAME && \
	pod2man --center "Fvwm Utilities" --release "@VERSION@@VERSIONINFO@" \
		--name $$NAME $$TMP/$$NAME >$$TMP/$$NAME.1 && \
	mv $$TMP/$$NAME.1 .; \
	rm -rf $$TMP)

_fvwm-perllib.1: fvwm-perllib
	@TMP=tmp-$$$$ NAME=fvwm-perllib && (\
	mkdir $$TMP && \
	cp $$NAME.in $$TMP/$$NAME && \
	pod2man --center "Fvwm Utilities" --release "@VERSION@@VERSIONINFO@" \
		--name $$NAME $$TMP/$$NAME >$$TMP/$$NAME.1 && \
	mv $$TMP/$$NAME.1 .; \
	rm -rf $$TMP)

regenerate: \
	_fvwm-menu-xlock.1

## Create compatibility symlinks if available

fvwm_root_name =`echo "fvwm-root" | "$(SED)" -e "${transform}"`
FvwmCommand_name =`echo "FvwmCommand" | "$(SED)" -e "${transform}"`

uninstall-local:
	@rm -f $(DESTDIR)$(bindir)/$(FvwmCommand_name)$(EXEEXT)

CLEANFILES = $(bin_SCRIPTS) $(bin_PROGRAMS)
