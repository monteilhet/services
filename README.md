
# Init system

## systemd

**systemd** is a relatively recent “init system”, and it becomes the default in Debian Jessie.

https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units


## sysvinit

**sysvinit** was derived and inherited from System V Unix systems (System V init)

---

# commands

## status

*systemd*

systemctl - Control the systemd system and service manager


```bash
# shows only active units by default
$ systemctl
# <=> systemctl list-units
### --all to see loaded but inactive units, to
$ systemctl --all
### list all the types of units
$ systemctl -t help
### list only services
$ systemctl list-units -t service
### Show system status (process tree) --all : including the status of all units
$ systemctl status
### To see every available unit file within the systemd paths, including those that systemd has not attempted to load
$ systemctl list-unit-files
### Displaying a Unit File
$ systemctl cat atd.service
### Checking Unit Properties
$ systemctl show sshd.service

### check the status of a service on your system
$ systemctl status sshd

### old syntax still working
$ service sshd status

```

*sysvinit*

```bash
$ service --status-all

$ service sshd status

```

## starting & stopping

*systemd*

```bash
$ systemctl start sshd
$ systemctl start sshd.service
$ systemctl stop sshd.service
$ systemctl restart sshd.service
$ systemctl reload sshd.service
$ systemctl reload-or-restart application.service
# Restarts if the service is already running.
$ systemctl condrestart foobar.service

### NB sysvinit syntax is still working but redirected to systemctl
$ service sshd start
$ service sshd stop
$ service sshd restart
$ service sshd reload
```

*sysvinit*

```bash
$ service sshd start
$ service sshd stop
$ service sshd restart
$ service sshd reload
```


## activation

*systemd*

```bash
$ systemctl enable sshd.service
### <=> ln -s '/usr/lib/systemd/system/sshd.service' '/etc/systemd/system/multi-user.target.wants/sshd.service'
$ systemctl disable sshd.service
### <=> rm '/etc/systemd/system/multi-user.target.wants/sshd.service'

$ systemctl is-enabled NetworkManager.service
$ systemctl is-active sshd.service
$ systemctl is-failed application.service


# Reload the systemd process scanning for new or changed units
$ systemctl daemon-reload
```

*sysvinit*


```bash
chkconfig NetworkManager on
chkconfig NetworkManager off
chkconfig NetworkManager

```

## system control

*systemd*

```bash
$ systemctl poweroff
### <=> init 0
$ systemctl reboot
### <=> init 6

```

*sysvinit*


```bash
init 0  # poweroff
init 6  # reboot


```



# Tips

## Convenient way to check if system is using systemd or sysvinit in bash

+ http://unix.stackexchange.com/questions/121654/convenient-way-to-check-if-system-is-using-systemd-or-sysvinit-in-bash


```bash
#!/bin/sh
if [ command -v systemctl >/dev/null ]
then
    systemctl service start
else
    /etc/init.d/service start
fi
```

## How to daemonize a process

### systemd

+ http://www.linuxtricks.fr/wiki/systemd-les-commandes-essentielles
+ https://alan-mushi.github.io/2014/10/26/execute-an-interactive-script-at-boot-with-systemd.html


### sysvinit

http://codingfreak.blogspot.com/2012/03/daemon-izing-process-in-linux.html

*daemonize — A tool to run a command as a daemon*
+ http://software.clapper.org/daemonize/

*Don’t Daemonize your Daemons! (another approach)*
+ http://www.mikeperham.com/2014/09/22/dont-daemonize-your-daemons/





