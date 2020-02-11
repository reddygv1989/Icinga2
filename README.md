# Icinga2

# Installation on Ubuntu
https://icinga.com/docs/icinga2/latest/doc/02-installation/

```shell commands
apt-get update
apt-get -y install apt-transport-https wget gnupg

wget -O - https://packages.icinga.com/icinga.key | apt-key add -

. /etc/os-release; if [ ! -z ${UBUNTU_CODENAME+x} ]; then DIST="${UBUNTU_CODENAME}"; else DIST="$(lsb_release -c| awk '{print $2}')"; fi; \
 echo "deb https://packages.icinga.com/ubuntu icinga-${DIST} main" > \
 /etc/apt/sources.list.d/${DIST}-icinga.list
 echo "deb-src https://packages.icinga.com/ubuntu icinga-${DIST} main" >> \
 /etc/apt/sources.list.d/${DIST}-icinga.list

apt-get update
```
You can install Icinga 2 by using your distribution’s package manager to install the icinga2 package. The following commands must be executed with root permissions unless noted otherwise.
```shell commands
apt-get install icinga2
```

# Setting up Check Plugins
Without plugins Icinga 2 does not know how to check external services. The Monitoring Plugins Project provides an extensive set of plugins which can be used with Icinga 2 to check whether services are working properly.

```shell command
apt-get install monitoring-plugins
```
# Running Icinga 2
# Systemd Service
The majority of supported distributions use systemd. The Icinga 2 packages automatically install the necessary systemd unit files.

The Icinga 2 systemd service can be (re-)started, reloaded, stopped and also queried for its current status.

````
systemctl status icinga2

icinga2.service - Icinga host/service/network monitoring system
   Loaded: loaded (/usr/lib/systemd/system/icinga2.service; disabled)
   Active: active (running) since Mi 2014-07-23 13:39:38 CEST; 15s ago
  Process: 21692 ExecStart=/usr/sbin/icinga2 -c ${ICINGA2_CONFIG_FILE} -d -e ${ICINGA2_ERROR_LOG} -u ${ICINGA2_USER} -g ${ICINGA2_GROUP} (code=exited, status=0/SUCCESS)
  Process: 21674 ExecStartPre=/usr/sbin/icinga2-prepare-dirs /etc/sysconfig/icinga2 (code=exited, status=0/SUCCESS)
 Main PID: 21727 (icinga2)
   CGroup: /system.slice/icinga2.service
           21727 /usr/sbin/icinga2 -c /etc/icinga2/icinga2.conf -d -e /var/log/icinga2/error.log -u icinga -g icinga --no-stack-rlimit

Jul 23 13:39:38 nbmif icinga2[21692]: [2014-07-23 13:39:38 +0200] information/ConfigItem: Checked 309 Service(s).
Jul 23 13:39:38 nbmif icinga2[21692]: [2014-07-23 13:39:38 +0200] information/ConfigItem: Checked 1 User(s).
Jul 23 13:39:38 nbmif icinga2[21692]: [2014-07-23 13:39:38 +0200] information/ConfigItem: Checked 15 Notification(s).
Jul 23 13:39:38 nbmif icinga2[21692]: [2014-07-23 13:39:38 +0200] information/ConfigItem: Checked 4 ScheduledDowntime(s).
Jul 23 13:39:38 nbmif icinga2[21692]: [2014-07-23 13:39:38 +0200] information/ConfigItem: Checked 1 UserGroup(s).
Jul 23 13:39:38 nbmif icinga2[21692]: [2014-07-23 13:39:38 +0200] information/ConfigItem: Checked 1 IcingaApplication(s).
Jul 23 13:39:38 nbmif icinga2[21692]: [2014-07-23 13:39:38 +0200] information/ConfigItem: Checked 8 Dependency(s).
Jul 23 13:39:38 nbmif systemd[1]: Started Icinga host/service/network monitoring system.
````
# Command	Description
* start	The start action starts the Icinga 2 daemon.
* stop	The stop action stops the Icinga 2 daemon.
* restart	The restart action is a shortcut for running the stop action followed by start.
* reload	The reload action sends the HUP signal to Icinga 2 which causes it to restart. Unlike the restart action reload does not wait until Icinga 2 has restarted.
* status	The status action checks if Icinga 2 is running.
* enable	The enable action enables the service being started at system boot time (similar to chkconfig)

