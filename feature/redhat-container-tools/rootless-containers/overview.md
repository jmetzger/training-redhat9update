# Rootless containers 

## Techn Preview in RHEL 8, now stable/supported in RHEL 9 

## Attention: 

  * The wording: rootless containers in this case means:
  * You can run containers as unprivileged user (e.g. user kurs)
    * the containers themselves can also run privileged (though)
   
## Walkthrough 

```
# as unprivileged user e.g. kurs
# when adding a new user with useradd
# this uses is automatically setup to use podman unprivileged
# run image alpine from hub.docker.com and show the id 
# after that please delete
# container still runs under root 
podman run --rm -it alpine id

```

```
![image](https://github.com/user-attachments/assets/81318db9-9b9a-4a3c-aa3e-4ca38298b357)
```

## Reference

  * https://docs.redhat.com/de/documentation/red_hat_enterprise_linux/9/html-single/building_running_and_managing_containers/index#proc_setting-up-rootless-containers_assembly_starting-with-containers
