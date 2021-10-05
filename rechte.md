# Rechte 

## Arten 

```
r = Lesen 
w = Schreiben
x = Ausführen 
```

## Für welchen Bereich ? 

```
u = user 
g = gruppe
o = others (die anderen / die Welt) 
a = für alle (d.h. gleichzeitig für u und g und o) 
```

## Aufbau triple 

```
kurs@ubuntu2004-101:~$ # rwx | rw- | r--
kurs@ubuntu2004-101:~$ #  u    g      o
kurs@ubuntu2004-101:~$ # 421 | 42- | 4--
kurs@ubuntu2004-101:~$ #  7  |  6  | 4

# rwx | rw- | r--
#  u    g      o
# 421 | 42- | 4--
#  7  |  6  | 4
```

## Berechtigungen mit Symbolen setzen 

```
chmod g+w,o+r testfile
```

## Berechtigungen mit Octalzahlen setzen 

```
chmod 777 testfile
```

## Berechtigungen recursiv setzen 

```
chmod -R 777 testverzeichnis 
```
