# Use Docker Compose in RHEL 9 

## Preparation / Installation 

```
dnf -y update
dnf install -y podman git 
# version needs to be >=3.0 
podman --version
```

```
# for using docker-compose podman.service needs to be running 
systemctl status podman.service
systemctl enable --now podman.service
systemctl status podman.service
# enabling and starting podman.service also creates a socket 
systemctl status podman.socket
```

```
# docker commands get translated to podman commands under the hood 
dnf install -y podman-docker
docker images
```

```
# get latest docker-compose 
curl -L https://github.com/docker/compose/releases/download/v2.30.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
chmod u+x /usr/local/bin/docker-compose
docker-compose
```

```
# now test it with a project 
# we do this in the home folder of root 
cd 
git clone https://github.com/docker/awesome-compose
cd awesome-compose/
ls -la
```

```
cd gitea-postgres/
# -d - daemon-mode -- let's it run in the background 
docker-compose up -d 
docker-compose images
```

```
docker-compose --help
# stop and delete everything 
docker-compose down
docker-compose images
```

## Reference:

  * https://linuxhistory.com/2023/06/23/podman-how-to-configure-docker-compose-for-rhel9/
