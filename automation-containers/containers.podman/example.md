# Example for containers podman (Pods and Deployment with podman and ansible)

## Step 1: install ansible and collection 

```
dnf install ansible-core 
ansible-galaxy collection install containers.podman
```

## Step 2: Create playbook 

```
cd
mkdir playtest
cd playtest
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
      src: /root/ws1/index.html
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


## Reference: 
  * https://www.redhat.com/en/blog/automate-podman-ansible
