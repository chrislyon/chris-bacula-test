
## -------------------------
## nom des fichiers de conf
## -------------------------
DIR_CONF=./bacula-dir.conf
SD_CONF=./bacula-sd.conf
FD_CONF=./bacula-fd.conf
CONSOLE_CONF=./bconsole.conf
#TRAY_CONF=./tray-monitor.conf
bat=./bat.conf

SAV_DIR=./sav
BACULA_CONF_DIR=/etc/bacula

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


.PHONY: install

install:
		cp $(ALL_FILES) $(BACULA_CONF_DIR)

.PHONY: restart

#/etc/init.d/bacula-director restart
#/etc/init.d/bacula-fd restart
#/etc/init.d/bacula-sd restart
restart:
	service bacula-dir restart
	service bacula-fd restart
	service bacula-sd restart

.PHONY: stop_service

stop_service:
	service bacula-dir stop
	service bacula-fd stop
	service bacula-sd stop

.PHONY: start_service

start_service:
	service bacula-dir start
	service bacula-fd start
	service bacula-sd start
