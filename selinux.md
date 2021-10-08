# SELinux 

## sestatus

 * Zeigt an, obwohl selinux aktiviert und wie

## Modi 

 * disabled 
 * enforcing (enabled)
 * permissive (enabled) 

## Persistente Konfiguration 

```
/etc/selinux/config
```
## Dateien mit context anzeigen

```
ls -laZ 
```

## Für nächsten Boot Kontext-Labels neu setzen 

```
# als root
cd / 
touch .autorelabel 
reboot
# Achtung relabeln kann dauern !!! durchaus 5 Minuten 
```
