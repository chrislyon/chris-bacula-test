
## -------------------------
## nom des fichiers de conf
## -------------------------
DIR_CONF=./bacula-dir.conf
SD_CONF=./bacula-sd.conf
FD_CONF=./bacula-fd.conf
CONSOLE_CONF=./bconsole.conf
TRAY_CONF=./tray-monitor.conf

SAV_DIR=./sav

ALL_FILES=$(DIR_CONF) $(SD_CONF) $(FD_CONF) $(CONSOLE_CONF) $(TRAY_CONF)

.PHONY: test

test:
	bacula-dir -t -c $(DIR_CONF)
	bacula-sd -t -c $(SD_CONF)
	bacula-fd -t -c $(FD_CONF)

.PHONY: sauve

sauve:
	tar --create \
		--gzip \
		--totals \
		--file=$(SAV_DIR)/$(shell date "+sav%Y%m%d_%H%M".tgz) $(ALL_FILES)


