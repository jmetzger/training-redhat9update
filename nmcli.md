# nmcli 

## Verbindungen anzeigen 

```
nmcli connection show
# or 
nmcli conn show 
```

## Netzwerk-Interface modifizieren

```
# muss in der Liste sichtbar sein 
nmcli con mod ens3 ipv4.method manual ipv4.addresses 192.168.1.3
nmcli con mod ens3 autoconnect yes

# verbindung neu hochziehen
nmcli con down ens3
nmcli con up ens3

# verbindungseigenschaften anzeigen
nmcli conn show ens3 


```


## Ref:

  * https://www.howtoforge.de/anleitung/wie-man-eine-statische-ip-adresse-unter-centos-8-konfiguriert/
