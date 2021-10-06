# Apache installieren (firewalld/selinux)

## Walkthrough 

```
## Schritt 1:
# suche // apache heisst auf centos httpd
yum search httpd
# oder
dnf search httpd

## Schritt 2: 
yum install httpd 

## Wie heisst der Dienst und Starten und Enablen (für nächsten Reboot)  
yum list-unit-files --type=service | grep httpd
systemctl enable httpd 
systemctl start httpd 

## Schritt 3: 
# Konfiguration anpassen
# /etc/httpd/conf/httpd.conf # Hauptkonfigurationsdatei
# Änderungen mit Editor vornehmen z.B. nano 
cd /etc/httpd/conf/httpd.conf; nano httpd.conf 
# Danach Neustart oder Reload 
# Restart funktioniert immer
systemctl restart httpd 

## Schritt 4:
# Firewall freigeben 
# D.h. welche zone ist active -> public 
firewall-cmd --get-active-zones  
# konfigurieren 
firewall-cmd --add-service=http --permanent 
firewall-cmd --add-service=https --permanent 
firewall-cmd --reload 

## Schritt 5: 
# Mit Browser testen 
```

## Apache started nicht wg Port-Änderung (Port: 82)  - Quick and Dirty Lösung

```
# /etc/httpd/httpd.conf
# zeile hinzufügen 
Listen 82

# Es kommt ein Fehler bei Apache port 82 (Listen 82) 
systemctl restart httpd

# Schritt 1: Prüfen, ob selinux aktiv ist
sestatus # Sucht 2 Einträgen enforcing 

# Schritt 2: selinux testweise abschalten 
setenforce 0 # das heisst, regeln werden protokolliert, aber nicht durchgesetzt 

# Schritt3: 
systemctl restart httpd 

# Wenn das der Fall ist, selinux deaktivieren 
/etc/selinux/config 
# mit editor 
SELINUX=permissive
# oder wenn man generell selinux nicht einsetzten möchte:
SELINUX=disabled 
# Danach rebooten 
```

## Apache started nicht wg Port-Änderung (Port: 82)  - Nice and Smooth (better!) 

```
# Falls sealert nicht installiert ist -> sealert -> command not found 
yum whatprovides sealert 

sealert -a /var/log/audit/audit.log > /root/report
# In der Datei finden wir Handlungsanweisungen 

# Welche port-typen gibt es für http
semanage port -l | grep http
# Wir entscheiden uns für http_port_t weil hier auch die 80 auftaucht 
semanage port -a -t http_port_t -p tcp 82 
setenforce 1 
systemctl restart httpd 

# Don't forget to add firewall rules 
firewall-cmd --list-all # is the port listed here ? 
firewall-cmd --add-port=82/tcp --zone=public --permanent # Sets in configuration but not in runtime 
firewall-cmd --reload 

# Now test with and your public ip 
# get it with 
ip a 

```
