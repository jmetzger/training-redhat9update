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

```
To create a new filesystem that will be compatible with the RHEL 8 kernel, disable these new features by adding -m bigtime=0,inobtcount=0 to the mkfs.xfs command line. A filesystem created in this way will not support timestamps beyond the year 2038.
```

## Migration 

  * The LEAPP - in place- migration - tool, does NOT do this for you  (changing it with xfs_admin)
  * You have do it manually, it does not work if filesystem is mounted

```
xfs_admin -O bigtime=1,inobtcount=1 /dev/mapper/rhel-root
```

## Reference:

  * https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/considerations_in_adopting_rhel_9/assembly_file-systems-and-storage_considerations-in-adopting-rhel-9#ref_file-systems_assembly_file-systems-and-storage
