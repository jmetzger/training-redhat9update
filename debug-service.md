# Debug Service 

## Walkthrough 

```
# Dienst startet nicht / nach Ausführen von systemctl restart wird Fehlermeldung ausgegeben
systemctl restart mariadb.service 

# Schritt 1 : status -> was sagen die logs (letzte 10 Zeilen) 
systemctl status mariadb.service 

# Nicht fündig-> Schritt 2:
jourrnalctl -xe

# Nicht fündig -> Schritt 3:
# -e springt ans Ende des Pages
journalctl -e -u mariadb.service 

# Nicht fündig -> Schritt 4:
# Spezifisches Log von Dienst suchen 
# und evtl. LogLevel von Dienst hochsetzen
# z.B. bei mariadb (durch Internetrecherche herausfinden) 
less /var/log/mysql/error.log 
# oder schneller
# Zeige alle Zeilen mit dem Wort error an (case insensitive) 
# also auch z.B. ERROR 
cat /var/log/mysql/error.log | grep -i error


# Nicht fündig -> Schritt 5
# Allgemeines Log
# Debian/Ubuntu 
/var/log/syslog
# REdhat/Centos 
/var/log/messages 
```

## Wie verfahren bei SystemV 

```
Wie bei walkthrough aber ab Schritt 4
```

## Find error in logs quickly

```
cd /var/log/mysql 
# -i = case insensitive // egal ob gross- oder kleingeschrieben
cat error.log | grep -i error
```

## Found wrong config-value, what now ?

```
# You know the wrong config value, but not 
# where it is (in which file)
# assuming gummitulpe is the wrong config value 
grep -r gummitulpe /etc

# Ausgabe
/etc/my.cnf.d/mariadb-server.cnf:gummitulpe=/nix
```
