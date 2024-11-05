# New keyfile-format for network profiles 

## Old version 

  * Network Profiles used to be stored here

```
/etc/sysconfig/network-scripts
```

  * This folder and format is deprecated
  * New files will not be created there anymore 

## New version 

  * no stored here:

```
/etc/NetworkManager/system-connections
```

  * ini-format (easily parseable)
  * Example:

```
[connection]
id=enp0s8
uuid=d58039f9-d191-4b2a-beda-d3a84b11cd7e
type=ethernet
interface-name=enp0s8

[ethernet]

[ipv4]
method=auto

[ipv6]
addr-gen-mode=eui64
method=auto

[proxy]
```

## Migration 

  * After in-place upgrade still the old files will be present
  * migration (will be migrated and removed from /etc/sysconfig/network-scripts)

```
nmcli conn migrate
```

