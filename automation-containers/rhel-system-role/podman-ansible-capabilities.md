# Use capabilities with RHEL System Roles (ansible), ansible and podman

![image](https://github.com/user-attachments/assets/2260917c-eba7-4ef8-b79c-5300ab1bebc5)

## Step 1: Configure management-node (on our redhat-master - node)  

```
# this alos includes all the necessary ansible packages
sudo dnf install rhel-system-roles
```

```
# Create user 
sudo useradd ansible
sudo su - ansible
```

```
# Create public/private key.
# For testing no pass please
ssh-keygen 
```

```
# Create ~/.ansible.cfg file
nano ~/.ansible.cfg
```

```
[defaults]
inventory = /home/ansible/inventory
remote_user = ansible

[privilege_escalation]
become = True
become_method = sudo
become_user = root
become_ask_pass = True
```

```
# Create inventory file
nano ~/inventory 
```

```
[DE]
redhat-node.training.local ansible_host=192.168.56.108
```

## Step 2: on node: configure redhat-node.training.local (our node to deploy)

```
# on redhat-node as root 
useradd ansible
usermod -aG wheel ansible 
# Set a password and please remember it ! 
passwd ansible 
```

## Step 3: on master node:

```
# on maaster-node as ansible user (where we do have the public key
# change your ip accordingly 
ssh-copy-id ansible@192.168.56.108 
```

```
# Issue a test command
ansible -m ping all
```

## Step 4: on master node: build the script 

  * Ref: https://www.redhat.com/en/blog/automating-podman-rhel-system-roles

```
nano ubi8-httpd-24.yml 
```

```
apiVersion: v1
kind: Pod
metadata:
  name: ubi8-httpd-24
spec:
  containers:
    - name: ubi8-httpd-24
      image: registry.access.redhat.com/ubi8/httpd-24
      ports:
        - containerPort: 8080
          hostPort: 8080
      volumeMounts:
        - mountPath: /var/www/html:Z
          name: ubi8-httpd-24-html
  volumes:
    - name: ubi8-httpd-24-html
      hostPath:
        path: /home/ansible/ubi8-httpd-24-html

```

```
# build the inventory.yml file
nano inventory.yml
```

```
all:
  hosts:
    redhat-node.training.local:
       ansible_host: 192.168.56.108
  vars:
    #podman system role variables:
    podman_firewall:
      - port: 8080/tcp
        state: enabled
    podman_create_host_directories: true
    podman_host_directories:
      "/home/ansible/ubi8-httpd-24-html":
        owner: ansible
        group: ansible
        mode: "0755"
    podman_kube_specs:
      - state: started
        run_as_user: ansible
        run_as_group: ansible
        kube_file_src: ubi8-httpd-24.yml

    #cockpit system role variables:
    cockpit_packages:
      - cockpit-podman
    cockpit_manage_firewall: true
```

```
nano system_roles.yml 
```

```
- name: Run podman RHEL system role
  hosts: all
  roles:
    - redhat.rhel_system_roles.podman

- name: Run cockpit RHEL system role
  hosts: all
  roles:
    - redhat.rhel_system_roles.cockpit
```

```
ansible-playbook -i inventory.yml -b system_roles.yml
```

### Reference:

  * https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/automating_system_administration_by_using_rhel_system_roles/assembly_preparing-a-control-node-and-managed-nodes-to-use-rhel-system-roles_automating-system-administration-by-using-rhel-system-roles



## Reference: 

  * https://www.redhat.com/en/blog/automating-podman-rhel-system-roles
