# Example files with selinux and httpd (apache) 

```
# as root
cd /var/www/html
echo "mydata" > test.html
cp -a test.html test2.html
# show labels 
ps auxZ | grep httpd
chcon -t var_t test2.html
# now we cannot access it anymore in the browser 

# Restore it to the settings defined in the policy
restorecon -vr /var/www
```
