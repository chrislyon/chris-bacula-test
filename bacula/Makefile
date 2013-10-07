
## -------------------------
## nom des fichiers de conf
## -------------------------
DIR_CONF=./trav/bacula-dir.conf
SD_CONF=./trav/bacula-sd.conf
FD_CONF=./trav/bacula-fd.conf
CONSOLE_CONF=./bconsole.conf
#TRAY_CONF=./tray-monitor.conf
bat=./bat.conf

SAV_DIR=./sav
BACULA_CONF_DIR=/etc/bacula

ALL_FILES=$(DIR_CONF) $(SD_CONF) $(FD_CONF) $(CONSOLE_CONF) $(TRAY_CONF)

TEST_DIR=/root/chris-bacula-test/bacula/trav/
INST_DIR=/etc/bacula/

.PHONY: test

test:
	@echo "Purge répertoire de travail"
	@rm -f trav/*.conf
	@echo "Compilation des fichiers de conf ..."
	@cat ./bacula-dir.conf | sed -e 's:!!BACULA_TRAV!!:$(TEST_DIR):' > $(DIR_CONF)
	@cat ./bacula-sd.conf | sed -e 's:!!BACULA_TRAV!!:$(TEST_DIR):' > $(SD_CONF)
	@cat ./bacula-fd.conf | sed -e 's:!!BACULA_TRAV!!:$(TEST_DIR):' > $(FD_CONF)
	@cp ./bacula-dir-*.conf $(TEST_DIR)
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
	@echo "Purge répertoire de travail"
	@rm -f trav/*.conf
	@echo "Compilation des fichiers de conf ..."
	@cat ./bacula-dir.conf | sed -e 's:!!BACULA_TRAV!!:$(INST_DIR):' > $(DIR_CONF)
	@cat ./bacula-sd.conf | sed -e 's:!!BACULA_TRAV!!:$(INST_DIR):' > $(SD_CONF)
	@cat ./bacula-fd.conf | sed -e 's:!!BACULA_TRAV!!:$(INST_DIR):' > $(FD_CONF)
	@cp ./bacula-dir-*.conf $(INST_DIR)
	cp $(TEST_DIR)* $(BACULA_CONF_DIR)

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
