# fapolicyd 

## Einschränkung: 

  * Standardmäßig darf der Root-Benutzer alle Kommandos ausführen
  * d.h. als root funktioniert nicht Übung nicht 

## Exercise 

```
# as root 
dnf install -y fapolicyd
systemctl enable --now fapolicyd
cp -a /bin/ls /tmp/ls
```

```
# as unprivileged user
/tmp/ls
# <- now allowed
```

```
# as privileged user
fapolicyd-cli --file add /tmp/ls --trust-file myapp
fapolicyd-cli --update
```

```
# as unprivileged user
/tmp/ls
```

## Reference: 

  * https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/security_hardening/assembly_blocking-and-allowing-applications-using-fapolicyd_security-hardening#marking-files-as-trusted-using-an-additional-source-of-trust_assembly_blocking-and-allowing-applications-using-fapolicyd
