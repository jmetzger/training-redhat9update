# rpm ist now using zstd as default mechanism for the payload 

## What is payload 

  * Payload is the cpio-archive that holds the binaries as an archive (like tar)
  * This file is compressed.
    * It used to be xz, now it is zstd (Z Standard)

## Why is zstd used ?

  * Takes less cpu
  * Is faster

## Source from redhat 

```
RPM now supports the Zstandard (zstd) compression algorithm

In RHEL 9, the default RPM compression algorithm has switched
to Zstandard (zstd). As a result, packages now install faster,
which can be especially noticeable during large transactions.
```

## How to test ?

```
# as root 
cd /usr/src
dnf download nano
# Which compression is used
rpm -q --queryformat '%{PAYLOADCOMPRESSOR}\n' -p nano*.rpm
```

## We are using special variables, what are they ? 

  * https://rpm-software-management.github.io/rpm/manual/tags.html#packages-with-files
