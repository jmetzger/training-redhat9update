# Systemd-networkd 

## Not supported on RHEL9 

```
Thank you for the request.  We have evaluated systemd-networkd and have determined we will not include it in Red Hat Enterprise Linux 9.

*** This bug has been marked as a duplicate of bug 1962257 ***
```

## Example 

```
# /etc/systemd/network/20-wired.network
[Match]
Name=enp1s0

[Network]
Address=10.1.10.9/24
Gateway=10.1.10.1
DNS=10.1.10.1
```

## Reference: 

  * https://bugzilla.redhat.com/show_bug.cgi?id=2020254
  * https://www.freedesktop.org/software/systemd/man/latest/systemd.network.html
