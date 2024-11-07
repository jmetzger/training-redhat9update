# cgroups-v2 

  * Enabled by default
  * subtree_control controls the levels beneath / granularity for subfolders

## Which version of cgroups, v1 or v2 is enabled 

```
mount | grep cgroup
```

## Behaviour of controllers 

  * If a controller was disabled in cgroup it cannot get enable in the next level 

## Difference to v1 

  * v2: no thread-level granularity for all controller, only process-level for all (like in v1)

## Exercise CGroups V2 -> systemd 

```
ps ax -o pid,cmd,cgroup | grep sshd

```
