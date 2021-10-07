# SSH absichern 

## sshd_config // Server

```
#/etc/ssh/sshd_config 
X11Forwarding no

# if possible - no one can login with password
PasswordAuthentication no 
PermitRootLogin no 
# user must belong to a specific group to be allowed to login
AllowGroups wheel
# if sftp is not need comment it - defaults to no 
# Subsystem     sftp    /usr/libexec/openssh/sftp-server
```

```
Restart sshd 
systemctl restart sshd 
```

## Setup private/public key authentication 

```
# Authentication with password must be possible
# When setting it up 
# Disable PasswordAuthentication afterwards 

# server2 client 
# as user kurs
ssh-keygen 
# set password set important
ssh-copy-id kurs@server1 

## Now you can login with public/private key 
ssh kurs@server1 

```
