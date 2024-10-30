# In-Place Upgrade Step-By-Step (RHEL 8.10 -> RHEL 9.4) 

## Step 1: What is not supported 

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
sudo leapp preupgrade --target 9.4
# Report is written to :
# /var/log/leapp/leapp-report.json
# And also writes results to the screen 
```


## Reference:

  * [https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/upgrading_from_rhel_8_to_rhel_9/index](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html-single/upgrading_from_rhel_8_to_rhel_9/index#planning-an-upgrade_planning-an-upgrade-to-rhel-9)
  * https://www.computerweekly.com/de/ratgeber/Wie-man-RHEL-8-auf-RHEL-9-aktualisiert
