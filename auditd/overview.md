# Auditing with auditd 

## Example syscal rule

```
-a exit,always -F arch=b64 -F euid=0 -S execve -k  audit-wazuh-c
-a exit,always -F arch=b32 -F euid=0 -S execve -k  audit-wazuh-c
```

```
# after that
augenrules --load
```

  * Ref: https://wazuh.com/blog/monitoring-root-actions-on-linux-using-auditd-and-wazuh/
  * Ref: https://access.redhat.com/solutions/36278
  * Ref: https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/6/html/security_guide/sec-defining_audit_rules_and_controls_in_the_audit.rules_file#sec-Defining_Audit_Rules_and_Controls_in_the_audit.rules_file
