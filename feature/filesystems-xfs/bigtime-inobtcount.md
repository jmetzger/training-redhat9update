# New Features enable in Redhat 9 

## bigtime && inobtcount 

  * bigtime. Date support beyond 2038
  * inobtcount: Inode btree counters (inobtcount), to reduce mount time on large filesystems.

## It looks like this in RHEL 9

```
xfs_info /dev/mapper/rhel*root | grep -e bigtime -e inobtcount
```

![image](https://github.com/user-attachments/assets/4c79ccbb-c54a-4432-953d-50d1a6d9edc6)

## Not enabled in Redhat 8 

```
xfs_info /dev/mapper/rhel*root | grep -e bigtime -e inobtcount
```

![image](https://github.com/user-attachments/assets/80c87777-3520-4efa-afef-64de7e9d20be)

## Downward compability 

  * If you want to use a filesystem with these feature enabled in RHEL 9:

```
You have to disable these with
xfs_admin
```

## Migration 

  * The LEAPP - in place- migration - tool, does this for you (changing it with xfs_admin)

## Reference:

  * https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/considerations_in_adopting_rhel_9/assembly_file-systems-and-storage_considerations-in-adopting-rhel-9#ref_file-systems_assembly_file-systems-and-storage
