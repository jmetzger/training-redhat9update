# cgroups-v2 

  * Enabled by default
  * subtree_control controls the levels beneath / granularity for subfolders

## Which version of cgroups, v1 or v2 is enabled 

```
mount | grep cgroup
```

## systemd 

### system.slice 

```
# Service is under system.slice
ls -la /sys/fs/cgroup/system.slice/
ls -la /sys/fs/cgroup/system.slice/sshd.service 
```

### nice overview 

```
# show a list 
systemd-cgls
systemd-cgls  -u system.slice
ps ax -o pid,cmd,cgroup | grep sshd
```

## Exercise CGroups V2 -> systemd 

### Step 1: Create a one shot service 

```
systemctl edit --force --full myservice1.service
```

```
# Put in this content
[Service]
Type=oneshot
ExecStart=/usr/lib/systemd/generate_load.sh
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

```
echo '#!/bin/bash' > /usr/lib/systemd/generate_load.sh
echo 'for i in {1..4};do while : ; do : ; done & done' >> /usr/lib/systemd/generate_load.sh
```

```
sudo chmod +x /usr/lib/systemd/generate_load.sh
sudo systemctl enable myservice1 --now
systemd-cgls
systemd-cgls -u system.slice
```

## Step 2: Create slice and set cpu for myservice1 

```
# create drop-ins
systemctl edit myservice1
```

```
# use this content
[Service]
Slice=my_custom_slice2.slice
MemoryAccounting=yes
CPUAccounting=yes
CPUWeight=200
```

## Step 3: Create service2 

```
cp -a  /usr/lib/systemd/generate_load.sh  /usr/lib/systemd/generate_load2.sh
chmod u+x /usr/lib/systemd/generate_load2.sh
```

```
systemctl edit --full --force myservice2
```

```
[Service]
Slice=my_custom_slice2.slice
Type=oneshot
ExecStart=/usr/lib/systemd/generate_load2.sh
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

```
systemctl edit myservice2
```

```
[Service]
CPUWeight=400
```

```
# Restarting and starting stuff
sudo systemctl daemon-reload
sudo systemctl restart myservice1
sudo systemctl enable myservice2 --now
```

### Step 3: See what is going on with cpu 

```
systemd-cgtop
```

![image](https://github.com/user-attachments/assets/949aeb49-8cbf-4bd8-8f30-7cd6c1a74190)


### Step 4: Experimenting with set propery 

```
# This settings are placed under 
/etc/systemd/system.control
```

```
cp -a  /usr/lib/systemd/generate_load.sh  /usr/lib/systemd/generate_load3.sh
chmod u+x /usr/lib/systemd/generate_load3.sh
```

```
systemctl edit --full --force myservice3
```

```
[Service]
Type=oneshot
ExecStart=/usr/lib/systemd/generate_load3.sh
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes
Slice=my_custom_slice2.slice

[Install]
WantedBy=multi-user.target
```

```
sudo systemctl daemon-reload
sudo systemctl enable myservice3 --now
```


### Step 5: use set property for myservice3

```
sudo systemctl set-property myservice3.service CPUWeight=800
cat /etc/systemd/system.control/myservice3.service.d/50-CPUWeight.conf
```

```
sudo systemctl daemon-reload
sudo systemctl restart myservice1
sudo systemctl restart myservice2
sudo systemctl restart myservice3
```

```
systemd-cgtop
```
