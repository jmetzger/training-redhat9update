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
