# VPN update method. 

1. Open the .conf that you download from the vpn.phil.us
2. Update whatever is required to update. For instance, recently we need to add more to allowedIPs
3. Save it
4. Open terminal and input the below command. From: [NMCLI setup](https://www.firezone.dev/docs/user-guides/client-instructions#linux-network-manager)
```sh
nmcli connection modify [old name] connection.id [new name]
sudo nmcli connection import type wireguard file /path/to/configuration.conf
```
5. start vpn again.

Additional reference:
- Ubuntu installation: [Click here](https://www.wireguard.com/install/#ubuntu-module-tools)
