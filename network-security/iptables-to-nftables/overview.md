# Changes iptables to nftables 

## Overview 

  * iptables now uses the nftables api under the hood
  * iptables - rules will still work, but will be "translated" to nftables backend under the hood
    * but they will not show up under nftables

```
iptables -v
```

![image](https://github.com/user-attachments/assets/123d684e-9419-46a0-8a2c-a9d599413bc6)

## Recommended approach - migrate to nftables 

  * see next document 
