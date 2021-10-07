# Podman 

## Walkthrough 

```
# runtergeladenen images
podman images
# image von online ziehen (registry) 
# Sucht bei redhat danach bei docker.io 
podman pull alpine:latest
# Image ist jetzt lokal vorhanden 
podman images
# Container mit diesem image starten
podman run --name=myalpine alpine
# Prozess läuft nicht mehr, da bereits beendet 
podman ps
# hiermit werden alle prozesse angezeigt auch die beendeten.
podman ps -a

# Beendeten container löschen über container - id (muss eindeutig sein bei z.B. 2 Ziffern) 
podman rm 08
# liste der container ist jetztleer
podman ps -a 

```

## Container interactive mit terminal 

```
# das sind die Optionen -i -t 
podman run -it --name=myalpine2 alpine

```

## Walkthrough II

```
# interactive mit terminal und detached
# Detached - es läuft weiter im hintergrund 
podman run -dit --name=myalpine3 alpine
# in maschine reinwechseln, Kommanda ls -la ausführen
# danach wieder raus
podman exec -it myalpine3 ls -la

podman ps -a

# geht nicht, weil es im container keine bash gibt
# das ist bei alpine der fall, hier gibt es nur busybox
podman exec -it myalpine3 bash

# einen sh - befehl gibt in jedem Linux
# dieser verweist auf die aktuelle Shell
podman exec -it myalpine3 sh

# Die Ausgabe des ersten Befehls wird geloggt 
podman run -it --name=myalpine4 alpine ls -la
# Logs anzeigen 
podman logs myalpine4

```

## Configuration abfragen

```
# Alle Konfigurationen
podman inspect myalpine3 
# oder container id
podman inspect a23e

podman inspect -f "{{.NetworkSettings.IPAddress}}" myalpine3
10.88.0.7



```


