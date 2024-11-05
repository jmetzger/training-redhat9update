# Sha1 - deprecated 

## Signed Packages 

  * No problems with packages from redhat
  * They are signed with sha256 
  * https://www.redhat.com/en/blog/rhel-security-sha-1-package-signatures-distrusted-rhel-9

## DNSSEC 

  * https://access.redhat.com/solutions/6955455

## ssh 

  * Problem connections from new to old
  * If you're running a mixture of new and old RHEL versions, you may have problems SSHing from new to old

### Workaround for connection to old system (RHEL5, RHEL 6)

  * https://rwmj.wordpress.com/2022/08/08/ssh-from-rhel-9-to-rhel-5-or-rhel-6/
