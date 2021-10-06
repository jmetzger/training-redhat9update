# Alle Prozesse eines Dienstes anzeigen

```
# inkl header - 2 Befehle getrennt durch ';' 
ps aux | head -n 1;  ps aux | grep mysqld | grep -v 'grep'


## Ausgabe 
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
mysql      16938  0.0  1.1 1778456 94776 ?       Ssl  09:51   0:00 /usr/libexec/mysqld --basedir=/usr

```
