# systemd - coredump 

```
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


```

