logconv_NAME = pm_logconv
logconv_SCRIPTS = $(logconv_NAME).py
logconv_CONFIG = $(logconv_NAME).conf.sample

MAINTAINERCLEANFILES = Makefile.in
logconvdir = @HA_NOARCHDATAHBDIR@/$(logconv_NAME)
logconvcfdir = @CONFIG_DIR@

SUBDIRS         = init

SHAREDIR = $(logconvdir)
SPEC = $(logconv_NAME).spec
TARFILE = $(PACKAGE_NAME)-$(VERSION).tar.gz
EXTRA_DIST = $(logconv_SCRIPTS) $(logconv_CONFIG) $(SPEC) init

install-data-hook:
	@$(NORMAL_INSTALL)
	test -z "$(logconvcfdir)" || $(mkdir_p) "$(DESTDIR)$(logconvcfdir)"
	$(INSTALL_DATA) "$(logconv_CONFIG)" "$(DESTDIR)$(logconvcfdir)"

$(TARFILE):
	$(MAKE) dist

RPM_ROOT	= $(CURDIR)
RPMBUILDOPTS	= --define "_sourcedir $(RPM_ROOT)" --define "_specdir $(RPM_ROOT)"

srpm: clean
	rm -f $(TARFILE)
	$(MAKE) $(SPEC) $(TARFILE)
	rpmbuild $(WITH_LIST) $(RPMBUILDOPTS) --nodeps -bs --rmsource $(SPEC)

rpm: clean
	rm -f $(TARFILE)
	$(MAKE) $(SPEC) $(TARFILE)
	rpmbuild $(WITH_LIST) $(RPMBUILDOPTS) -ba --rmsource $(SPEC)

