# cgroups-v2 

  * Enabled by default
  * subtree_control controls the levels beneath / granularity for subfolders

## Which version of cgroups, v1 or v2 is enabled 

```
mount | grep cgroup
```

## Behaviour of controllers 

  * If a controller was disabled in cgroup it cannot get enable in the next level 
