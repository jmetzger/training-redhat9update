# Yopad 

```
# Redhat 9 - Update 

## Documentation 

https://github.com/jmetzger/training-redhat9update

## Analyse - Server 

1. Welche Interfaces 
ip a 
ip route
top  
iostat 





## Übung 3.4 

systemctl list-units | grep core
systemctl status systemd-coredump.socket

# systemd-coredump maskieren
# Dadurch wird er nicht verwendet 

# Deaktivieren 
systemctl mask systemd-coredump.socket
systemctl stop systemd-coredump.socket qq

# Aktivieren 
systemctl unmask systemd-coredump.socket
systemctl start systemd-coredump.socket

######## Teil 2  -  verwenden -> als root 
# Terminal 1: root 
dnf install yum-utils
debuginfo-install -y vim-debuginfo

# config für systemd-coredump 
# /etc/systemd/system.conf 
#DumpCore=yes
DefaultLimitCore=infinity 

# Terminal 2: als kurs 
ulimit -S -c unlimited > /dev/null 2>&1
vim testfile 
sleep 3 & kill -SEGV $!
# was reinschreiben ohne speichern, d.h. vim offen lassen 

# Terminal 1:  (root)
# process id von vim rausfinden 
ps ax | grep testfile 
kill -s SIGSEGV 41262 
coredumpctl 


## Übung 3.4 


## Übung 3.3.

https://github.com/jmetzger/training-redhat9update/blob/main/feature/filesystems-xfs/bigtime-inobtcount.md

## Übung 3.2 

https://github.com/jmetzger/training-redhat9update/blob/main/feature/cgroups-v2/overview.md



## Documentation - Tag 3  / Übung 3.1 

https://github.com/jmetzger/training-redhat9update/blob/main/network/mptcp/overview.md

echo "net.mptcp.enabled=1" > /etc/sysctl.d/90-enable-MPTCP.conf
sysctl -p /etc/sysctl.d/90-enable-MPTCP.conf
sysctl net.mptcp.enabled
dnf install -y  mptcpd iperf3
# Listener 
mptcpize run iperf3 -s &
while true ; do ss -nti '( dport :5201 )'; done

## Dann im Client -> 
# client 
mptcpize run iperf3 -c 127.0.0.1 -t 3
nstat -s MPTcp*


## Documentation - Tag 1

https://github.com/jmetzger/training-redhat9update/blob/main/distros/overview-in-comparison-to-rhel-9.md
https://github.com/jmetzger/training-redhat9update/blob/main/network/systemd-networkd/overview.md
https://github.com/jmetzger/training-redhat9update/blob/main/network/ipv6/overview.md

## Documentation - Tag 2
https://github.com/jmetzger/training-redhat9update/blob/main/feature/redhat-container-tools/overview.md
https://github.com/jmetzger/training-linux-sicherheit-und-haertung/blob/main/secureboot/06-encrypt-data-with-luks-tpm.md

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/considerations_in_adopting_rhel_9/index

https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/security_hardening/using-the-system-wide-cryptographic-policies_security-hardening#using-the-system-wide-cryptographic-policies_security-hardening

## Übung 2.4. 

training ALL=(ALL) /usr/bin/systemctl reload sshd,/usr/bin/chown
useradd training :
passwd training
su - training 
cdcat /etioas



## Übung 2.3 

1. Reboot und in bootmanager gehen (ESC) -> e für edit der 1. Zeile 
2. Zeile linux, und schreiben ans Ende: init=/bin/bash 
3. CTRL x 
4. mount -o remount,rw / 
5. Passwort ändern 
passwd
6. touch /.autorelabel 
7. -> vm stopen/schliessen
8. neu starten 
9. einloggen mit root mit neuem Passwort 


## Übung 2.2 

https://github.com/jmetzger/training-redhat9update/blob/main/feature/rpm-zstd/overview.md

# Übung 2.1 

Make redhat 8 great again 
https://github.com/jmetzger/training-redhat9update/blob/main/upgrade/in-place/step-by-step.md#step-96-analyze-errors-possible-error-cannot-open-database-file


## Übung 1.2 

in-place upgrade RHEL 8.10 ->> 9.4 

https://github.com/jmetzger/training-redhat9update/blob/main/upgrade/in-place/step-by-step.md


## Übung 1.1 

https://github.com/jmetzger/training-redhat9update/blob/main/application_streams/overview.md


## Default Target setzen 

systemctl set-default multi-user.target 
reboot 

## in kernel param

systemd.unit=multi-user.target

## Target während des Betriebs 

systemctl isolate multi-user.target 
systemctl set-default multi-user.target 
reboot 

## Ip - Adresse anzeigen 

ip a show enp0s8 




```
