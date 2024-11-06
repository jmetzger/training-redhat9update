# Application Streams (appstream - repos) 

  * Applikation streams where introduced in Redhat 8

## Advantages 

  * You can switch to a different version 
  * More new version are introduced, and you can decide which version to use

## Disadvantages 

  * Only one version of the software can be installed at a time

## Overview over different software packages and versions 


## Modules, Stream and profiles 

  * module: Name of the software (e.g. postgresql)
  * stream: The version (e.g. 15)
  * profile: Different use cases, e.g. client / server

## Walkthrough Postgresql 

### Step 1: What modules are available ? 

```
dnf module list
```

### Step 2: List all versions for postgresql 

```
dnf module info postgresql
```

### Step 3: Try to install a version  

```
# This does not work 
dnf install @postgresql
```

### Step 4: We will decided for a version 

 * Format for a specific version: dnf install @module:version/profile

```
# for the profile we take the default -> server 
dnf install @postgresql:15
```

### Step 5: Switch to a newer version 

```
dnf module reset postgresql
# this does not yet install the components
dnf list --installed | grep postgresql
```

```
# now install the newer version
dnf install @postgresql:16
dnf list --installed | grep postgresql 
```

```
# just to be sure, all modules do have the proper version
dnf distro-sync 
```

### Step 6: switch back to version 15 

```
dnf reset module postgresql
dnf install @postgresql:15
```

```
# now check for the installed version
dnf list --installed | grep postgresql
```

## Reference 

  * https://www.redhat.com/en/blog/introduction-appstreams-and-modules-red-hat-enterprise-linux
