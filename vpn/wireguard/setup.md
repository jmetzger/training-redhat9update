# Setup wireguard 

## 2 peer - servers 

![image](https://github.com/user-attachments/assets/bf51649d-a118-4182-89d5-43b9be38723e)

## Prerequisites:

  * We will have 2 machines (peers)

```
Server:

Private key: <your private-key-of-this-server>
Tunnel IPv4 address: 192.0.2.1/24
Tunnel IPv6 address: 2001:db8:1::1/32
Client:

Public key: <your public-keyof-2-1-server>
Tunnel IPv4 address: 192.0.2.2/24
Tunnel IPv6 address: 2001:db8:1::2/32
```

## Step 1.1: Setup Server: Install wg-tools 

```
# it also install systemd-resolve for name resolution as dependency 
dnf install -y wireguard-tools
# now the wg command should be available 
wg --version 
```

## Step 1.2: Setup Server: Create private/public-key 

```
wg genkey | sudo tee /etc/wireguard/server_private.key | wg pubkey | sudo tee /etc/wireguard/server_public.key
# set permissions only privileged users can access
chmod 600 /etc/wireguard/server_private.key /etc/wireguard/server_public.key
cat /etc/wireguard/server_private.key
```

## Step 1.3: Setup Client: Install wg-tools 

```
# it also install systemd-resolve for name resolution as dependency 
dnf install -y wireguard-tools
# now the wg command should be available 
wg --version 
```

## Step 1.4: Setup Client: Create private/public-key 

```
wg genkey | sudo tee /etc/wireguard/server_private.key | wg pubkey | sudo tee /etc/wireguard/server_public.key
# set permissions only privileged users can access
chmod 600 /etc/wireguard/server_private.key /etc/wireguard/server_public.key
cat /etc/wireguard/server_private.key
```


## Step 1.5: Setup Server: Setup interface wg0 

  * Now back to server 

```
nano /etc/wireguard/wg0.conf
```


```
[Interface]
Address = 192.0.2.1/24, 2001:db8:1::1/32
ListenPort = 51820
PrivateKey = <private-key from Step 1.2 from server>

[Peer]
PublicKey = <public-key from Step 1.4 from client>
AllowedIPs = 192.0.2.2, 2001:db8:1::2
```
```
# Enable connection
systemctl enable --now wg-quick@wg0
# Status ?
systemctl status wg-quick@wg0
# New Interface
ip a
# Get info through wg - command
wg show wg0 
```

## Step 1.6.  Setup Server: Setup Firewall 

```
firewall-cmd --permanent --add-port=51820/udp --zone=public
firewall-cmd --permanent --zone=public --add-masquerade
firewall-cmd --reload
```

## Step 1.7. Setup Client: Setup interface wg0 

```
nano /etc/wireguard/wg0.conf 
```

```
[Interface]
Address = 192.0.2.2/24, 2001:db8:1::2/32
PrivateKey = <private-key-from-1.4>
[Peer]
PublicKey = <public-key-from-1.2>
AllowedIPs = 192.0.2.1, 2001:db8:1::1

# Endpoint = <public-ip-of-server-1.1-1.3>:51820
# e.g. 
Endpoint = 192.168.56.110:51820
PersistentKeepalive = 20
```

```
# Enabling the interface 
systemctl enable --now wg-quick@wg0
```

## Step 1.8 Testen vom client aus zum Server 

```
ping -c 4 192.0.2.1 
```

## Step 1.9  Test vom server aus zum client 

```
# das geht nicht 
ping -c 4 192.168.0.2
```


## Reference:

  * https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/9/html/configuring_and_managing_networking/assembly_setting-up-a-wireguard-vpn_configuring-and-managing-networking
