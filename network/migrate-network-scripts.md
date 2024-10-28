# Migrate Network scripts (RHEL 8 -> RHEL 9) 

## Reason:

  * network-scripts has been deprecated in RHEL 8 is not available in RHEL 9

## Solution:

```
mkdir /opt/network-scripts/
# move custom network scripts to here 
mv /sbin/if*-local /opt/network-scripts/
# create dispatcher for networkmanager 
nano /etc/NetworkManager/dispatcher.d/20-if-local 
```

```
#!/bin/bash

test -n "$DEVICE_IFACE" || exit 0

run() {
    test -x "$1" || exit 0
    "$1" "$DEVICE_IFACE"
}                

case "$2" in 
    "up")   
        run /opt/network-scripts/ifup-local
        ;;      
    "pre-up")
        run /opt/network-scripts/ifup-pre-local
        ;;      
    "down") 
        run /opt/network-scripts/ifdown-local
        ;;      
    "pre-down")
        run /opt/network-scripts/ifdown-pre-local
        ;;      
esac
```

```
# Set permissions 
chown root:root /etc/NetworkManager/dispatcher.d/20-if-local
chmod +x /etc/NetworkManager/dispatcher.d/20-if-local
restorecon /etc/NetworkManager/dispatcher.d/20-if-local
```

```
# if pre-up pre-down events are needed 
ln -s ../20-if-local /etc/NetworkManager/dispatcher.d/pre-up.d/
ln -s ../20-if-local /etc/NetworkManager/dispatcher.d/pre-down.d/
```

## Reference: 

  * https://access.redhat.com/solutions/6900331
