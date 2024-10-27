# Ansible with podman and capabilities

## Requirements: Last exercise 01-ansible......

## Simple pod 

```
cd
mkdir podtest
cd podtest
```

```
nano pod.yml 
```

```
apiVersion: v1
kind: Pod
metadata:
  name: alpine
spec:
  containers:
    - name: cont
      image: alpine
      securityContext:
        capabilities:
          drop: ["ALL"]
```

```
nano inventory.yml
```

```
all:
  hosts:
    redhat-node.training.local:
       ansible_host: 192.168.56.108
  vars:
    podman_kube_specs:
      - state: started
        run_as_user: ansible
        run_as_group: ansible
        kube_file_src: pod.yml
```

```
nano system_roles.yml
```

```
- name: Run podman RHEL system role
  hosts: all
  roles:
    - redhat.rhel_system_roles.podman
```

```
ansible-playbook -i inventory.yml -b system_roles.yml
```
