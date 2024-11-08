# MultiPath TCP 

```
echo "net.mptcp.enabled=1" > /etc/sysctl.d/90-enable-MPTCP.conf
sysctl -p /etc/sysctl.d/90-enable-MPTCP.conf
```

## TestPage 

  * curl http://www.multipath-tcp.org

## Exercise 

```
echo "net.mptcp.enabled=1" > /etc/sysctl.d/90-enable-MPTCP.conf
sysctl -p /etc/sysctl.d/90-enable-MPTCP.conf
sysctl net.mptcp.enabled
dnf install -y  mptcpd iperf3
# Listener 
mptcpize run iperf3 -s &
while true ; do ss -nti '( dport :5201 )'; done

## Dann im Client -> 
# client 
mptcpize run iperf3 -c 127.0.0.1 -t 3
nstat -s MPTcp*
```


## Joining 

![image](https://github.com/user-attachments/assets/dc7adea8-d75a-4b1d-941f-6dccfa60e9fd)

## Reference 

  * https://www.mptcp.dev/
  * https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/configuring_and_managing_networking/getting-started-with-multipath-tcp_configuring-and-managing-networking
    
