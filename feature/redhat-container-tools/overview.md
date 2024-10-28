# Redhat Container Tools 

## Metapackage for a couple of container - tools 

  * This holds a couple of packages: Podman, Buildah, Skopeo, CRIU, Udica

## Install 

```
dnf install -y container-tools
```

![image](https://github.com/user-attachments/assets/8a2d0e90-e987-4224-975d-1c77ee1cd8d3)

## How it works in Redhat 9 (it w

### 2 ways to consume container tools 

#### Way 1: move quickly -> application stream 

  * Applicaton Stream
  * Released every 12 weeks 
  * For developers and users, who want to access the latest podman, buildah and skopeo 

#### Way 2: stable stream 

  * Additional Subscription: Extended Update Support (EUS) 
  * Maintaining a consistent version of podman.
  * Support security backports for 2 years.

### Notes on podman-docker 

```
The podman-docker package replaces the Docker command-line interface and docker-api with the matching Podman commands. Every time you run a Docker command, the system will actually run a Podman command
```

## Reference:

  * https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html-single/considerations_in_adopting_rhel_9/index#ref_changes-to-containers_assembly_containers