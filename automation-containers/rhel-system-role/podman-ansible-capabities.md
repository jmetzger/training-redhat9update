# Use capabilities with RHEL System Roles (ansible), ansible and podman

![image](https://github.com/user-attachments/assets/2260917c-eba7-4ef8-b79c-5300ab1bebc5)

## Step 1: Configure management-node (on our redhat-master - node)  

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
nano ~/.inventory 
```

```
[DE]
redhat-node.training.local ansible_host=192.168.56.108
```




### Reference:

  * https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/automating_system_administration_by_using_rhel_system_roles/assembly_preparing-a-control-node-and-managed-nodes-to-use-rhel-system-roles_automating-system-administration-by-using-rhel-system-roles



## Reference: 

  * https://www.redhat.com/en/blog/automating-podman-rhel-system-roles
