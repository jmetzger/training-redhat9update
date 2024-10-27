# Example for containers podman (Pods and Deployment with podman and ansible)

## Step 1: install ansible and collection 

```
dnf install ansible-core 
ansible-galaxy collection install containers.podman
```

## Step 2: Create project folder  

```
cd
mkdir playtest
cd playtest
```
## Step 3: create playbook 

```
echo "hallo welt" > index.html 
```

```
nano playbook.yml
```

```
---
- hosts: podman
  tasks:
  - name: installing podman
    package:
      name: "podman"
      state: present
  - name: Pull an image
    containers.podman.podman_image:
      name: docker.io/library/httpd
  - name: Copying file into home
    copy:
      src: /root/playtest/index.html
      dest: /home
  - name: Re-create a httpd container
    containers.podman.podman_container:
      name: web
      image: httpd
      state: started
      detach: true
      exposed_ports:
        - 80
      ports:
        - 4444:80
      volumes: /home/:/usr/local/apache2/htdocs/
```

```
ansible-playbook playbook.yml
```

## Step 4: Try with alpine 

```
nano playbook-alpine.yml
```

```
---
- hosts: localhost
  tasks:
  - name: Pull an image
    containers.podman.podman_image:
      name: docker.io/library/alpine
  - name: create a podman container 
    containers.podman.podman_container:
      name: web
      image: docker.io/library/alpine
      command:
        - sleep
        - infinity
      cap_drop:
        - ALL
      state: started
      detach: true
```

```
ansible-playbook playbook-alpine.yml
```

```
# now let us have a look into the capabilities
podman exec -it web cat /proc/1/status | grep -i cap
```



## Reference: 
  * https://www.redhat.com/en/blog/automate-podman-ansible
