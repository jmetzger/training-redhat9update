# In-Place Upgrade Step-By-Step (RHEL 8.10 -> RHEL 9.4) 

## Step 1: What is not supported (but the leapp preupgrade will show you !)

  * Find out if there is something that is not supported, e.g.
    * Having ansible tower installed (migration process is different) 
    * wanting to shift from bios tu uefi boot
   
## Step 2: Vorbereitungsschritte

  1. Es sollte kein Ansible/Puppet Änderung am Systme machen
  1. Von auch Rhel 7 auf RHEL 8 auch mit LEAPP durchgeführen ?
     * Dann löschen: sudo rm -rf /root/tmp_leapp_py3
  1. Ist Abonnenment da ?
     * sudo subscription-manager list --installed  -> Status: subskribiert

## Step 3: Make backup of system 

  * In our case, we will make a "Sicherung" in virtualbox
  * In addition we will create a clone beforehand 

## Step 4: Sicherstellen, dass beide Repos aktiviert sind, Stand sperren und update durchführen  

```
sudo subscription-manager repos --enable rhel-8-for-x86_64-baseos-rpms --enable rhel-8-for-x86_64-appstream-rpms
sudo subscription-manager release --set 8.10
sudo dnf update
```

## Step 5: leapp-upgrade installiere und alle Anwendungssperren entfernen 

```
sudo dnf install -y leapp-upgrade
# if you get command not found, this dnf plugin is not installed
# that's o.k. , then you also will have no versionlocks 
dnf versionlock clear  
```

## Step 6: Disable AllowDriftingZone in Firewall 

```
cat /etc/firewalld/firewalld.conf | grep -i allowzonedrifting 
# if you have yes here, disable -> set to no  (with vi or nano) 
```

## Step 7: Do the preupdate checks with leapp 

```
# it might take its time, so verbose and debug might be a good idea.
# ON MY SYSTEM it TOOK 35 minutes and then 2nd on 17 minutes  
sudo leapp preupgrade --debug --verbose --target 9.4
# Report is written to :
# /var/log/leapp/leapp-report.json
# And also writes results to the screen 
```

## (Optional) Step 8: View report in cockpit 

```
dnf install cockpit-leapp
```

### Step 9: Upcoming error Processor: Unsupported Family 

```
# will adjust the configuration/checks file in leap, because we now this processor is working
# we installed it under RHEL 9 already
# Looks like a typical error in virtualbox
```


  * https://access.redhat.com/solutions/7052222

### Step 9.5: Upgrading system 

```
sudo leapp upgrade --debug --verbose --target 9.4
```

### Step 9.6: Analyze errors: Possible error: cannot open database file 

  * Database file cannot be opened because of too many open files

```
# default seems to be 1024 - which could be too small
# shows max for open file descriptors 
ulimit -n

# rerun command with strace, to see the problems
strace -fttTvyyo /tmp/leapp.strace -s 128 leapp upgrade --debug --verbose --target 9.4
# You will see the errors here
grep "1 EMFILE" /tmp/leapp.strace
```


  * https://access.redhat.com/solutions/6878881

### Step 9.7: Fix error 

```
ulimit -n 16384
# rerun upgrade 
leapp upgrade --debug --verbose --target 9.4
```

### Step 10: Reboot into initramfs (for update)

  * There was a special initramfs created to complete the upgrade

```
reboot
```

### Step 11: Post-Upgrade check 

```
cat /etc/redhat-release
uname -r
subscription-manager list --installed
subscription-manager release
```

  * There are some notes, about it here: https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/upgrading_from_rhel_8_to_rhel_9/verifying-the-post-upgrade-state_upgrading-from-rhel-8-to-rhel-9#verifying-the-post-upgrade-state_upgrading-from-rhel-8-to-rhel-9

## Step 12: Post-upgrade cleanup (Part 1)

  * We need to do some cleanup

```
#  1. Delete all packages from the exclude list 
dnf config-manager --save --setopt exclude=''
```

## Step 13: Post-upgrade cleanup (Part 2)

```
# Locate the packages from RHEL 8 
rpm -qa | grep -e '\.el[78]' | grep -vE '^(gpg-pubkey|libmodulemd|katello-ca-consumer)' | sort
```

```
# Delete all the packages from RHEL 8
dnf remove $(rpm -qa | grep -e '\.el[78]' | grep -vE '^(gpg-pubkey|libmodulemd|katello-ca-consumer)' | sort)
```

```
dnf remove leapp-deps-el9 leapp-repository-deps-el9
```

## Optional: Step 14: Delete related upgrade data 

  * Eventually, you want to do this later, when everything is o.k.

```
rm -rf /var/log/leapp /root/tmp_leapp_py3 /var/lib/leapp
```

## Step 15: Update Kernel Command (set new default) 

```
BOOT_OPTIONS="$(tr -s "$IFS" '\n' </proc/cmdline | grep -ve '^BOOT_IMAGE=' -e '^initrd=' | tr '\n' ' ')"
echo $BOOT_OPTIONS > /etc/kernel/cmdline
```

## Step 16: Delete existing initramfs for rescue mode and create new one 

```
rm /boot/vmlinuz-*rescue* /boot/initramfs-*rescue* 
```
```
/usr/lib/kernel/install.d/51-dracut-rescue.install add "$(uname -r)" /boot "/boot/vmlinuz-$(uname -r)"
```

## Step 17: Verify new rescure system 

```
ls /boot/vmlinuz-*rescue* /boot/initramfs-*rescue*
lsinitrd /boot/initramfs-*rescue*.img | grep -qm1 "$(uname -r)/kernel/" && echo "OK" || echo "FAIL"
```

```
# check if entry in bootmenu refers to the right rescue kernel
grubby --info $(ls /boot/vmlinuz-*rescue*)
```

## Step 18: Check and activate security profile 

```
# Are there any denials ? 
ausearch -m AVC,USER_AVC -ts boot
# set tto enforcing
vi /etc/selinux/config
```

```
# from permissive 
.... enforcing
```

```
reboot
```

## Reference:

  * [https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/upgrading_from_rhel_8_to_rhel_9/index](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html-single/upgrading_from_rhel_8_to_rhel_9/index#planning-an-upgrade_planning-an-upgrade-to-rhel-9)
  * https://www.computerweekly.com/de/ratgeber/Wie-man-RHEL-8-auf-RHEL-9-aktualisiert
