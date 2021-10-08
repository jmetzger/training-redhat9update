# nmcli 

## Verbindungen anzeigen 

```
nmcli connection show
# or 
nmcli conn show 
```

## Netzwerk-Interface statisch auf Server neu einrichten (server 2)

```
# muss in der Liste sichtbar sein 
nmcli con add type ethernet con-name enp0s9 ifname enp0s9 ipv4.method manual ipv4.addresses 192.168.1.2/24
nmcli con mod enp0s9 autoconnect yes

# verbindung neu hochziehen
nmcli con up enp0s9

# verbindungseigenschaften anzeigen
nmcli con show 

```

## Netzwerk-Interface statisch auf Server neu einrichten (server 3)

```
# muss in der Liste sichtbar sein 
nmcli con add type ethernet con-name enp0s9 ifname enp0s9 ipv4.method manual ipv4.addresses 192.168.1.3/24
nmcli con mod enp0s9 autoconnect yes

# verbindung neu hochziehen
nmcli con up enp0s9

# verbindungseigenschaften anzeigen
nmcli con show 

```





## Netzwerk-Interface modifizieren (server 3) 

```
# muss in der Liste sichtbar sein 
nmcli con mod ens3 ipv4.method manual ipv4.addresses 192.168.1.3/24
nmcli con mod ens3 autoconnect yes
# set the correct interface for the connection 
nmcli con mod ens3 ifname eth1

# verbindung neu hochziehen
nmcli con up ens3

# verbindungseigenschaften anzeigen
nmcli conn show ens3 

```

## Netzwerk-Interface modifizieren (server 4) 

```
nmcli conn show 
# muss in der Liste sichtbar sein 
nmcli con mod "Wired connection 1" ipv4.method manual ipv4.addresses 192.168.1.4/24
nmcli con mod "Wired connection 1" autoconnect yes
# set the correct interface for the connection if not present !!!
# nmcli con mod "Wired connection 1" ifname eth1

# verbindung neu hochziehen
nmcli con up "Wired connection 1"

# verbindungseigenschaften anzeigen
nmcli conn show "Wired connection 1"

# Does it have an ip 
# eth1
ip a


```




## Ref:

  * https://www.howtoforge.de/anleitung/wie-man-eine-statische-ip-adresse-unter-centos-8-konfiguriert/
