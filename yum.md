# yum 

## Mögliche Paket anzeigen (die installiert sind und installiert werden können)

```
yum list
```

## Installierte Pakete anzeigen 

```
yum list --installed 
```

## Herausfinden, wie ein Paket heisst, dass ich installieren will

```
yum list | grep mariadb 

```

## Ist ein Paket installiert 

```
yum list --installed | grep mariadb 
```

## Nach einem Paket suchen 

```
yum search mariadb 

```

## Infos zu einem Paket abrufen 

```
yum info mariadb-server
```

## Welche Programmpaket installiert ein bestimmtes Programm

```
# Beispiel sealert 
yum whatprovides sealert 

```


## Cheatsheet

  * https://access.redhat.com/sites/default/files/attachments/rh_yum_cheatsheet_1214_jcs_print-1.pdf
