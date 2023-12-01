# Setting a Static IP in Ubuntu Using Netplan

Netplan is the Ubuntu network configuration tool in all recent Ubuntu versions. Netplan is based on a YAML-based configuration system that simplifies the configuration process.

**How to Configure Static IP Address on Ubuntu 20.04**

`vim /etc/netplan/01-network-manager-all.yaml`
```
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: no
      addresses:
        - 192.168.10.250/24
      gateway4: 192.168.10.1
      nameservers:
          addresses: [8.8.8.8, 8.8.4.4]
```
`sudo netplan apply`

`ip a`

`ifconfig`

**How to Configure Static IP Address on Ubuntu 22.04**

`vim /etc/netplan/01-network-manager-all.yaml`
```shell
network:
  version: 2
  renderer: networkd
  ethernets:
    ens33:
      dhcp4: no
      addresses:
        - 192.168.10.245/24
      routes:
        - to: default
          via: 192.168.10.1
      nameservers:
          addresses: [8.8.8.8, 8.8.4.4]
```

`sudo netplan apply`


**Explanation:**

  -   `network`: The top-level keyword indicating that this is a Netplan       network configuration file.
  -   `version: 2`: Specifies the Netplan configuration syntax version.
  -   `renderer: networkd`: Specifies the network renderer to use. In this case, it's set to use `systemd-networkd`.
  -   `ethernets`: Defines Ethernet (network interface) configurations.
  -   `ens33`: The name of the Ethernet interface. You may need to adjust this based on your actual interface name.   
  -   `dhcp4: no`:  Disables DHCP for IPv4 on this interface.It's default have `Yes`

        ````
        The term "dhcp4" typically refers to DHCP (Dynamic Host Configuration Protocol) version 4. DHCP is a network protocol used to automatically provide network parameters, such as IP addresses, subnet masks, default gateways, and DNS servers, to devices on a network. The "4" in "dhcp4" specifies that it's referring to DHCP version 4, which is the most widely used version in IPv4 networks.
        ````
-   `addresses: [192.168.10.245/24]`: Configures a static IPv4 address of `192.168.10.245` with a subnet mask of `24` (implying a    subnet mask of `255.255.255.0`).

    ````
    The addresses section specifies the IP address and subnet mask of the device. In this case, the device is assigned the IP address `192.168.10.245` with a subnet mask of `/24` (which represents a subnet mask of `255.255.255.0`). This implies that the device is part of the `192.168.10.0/24` subnet.
    ````

   -   `routes`: Configures a static route.
       -   `to: default`: Specifies that this is the default route.
       -   `via: 192.168.10.1`: Specifies the gateway for the default route. It's our own route or LAN ip.

       ```
       The `routes` section defines the routing configuration. In this case, there is a single route defined:
       `to: default:` This indicates that this route is the default route, used when there is no specific route for a destination.
       `via: 192.168.10.1:` Traffic that doesn't match any more specific routes will be sent via the gateway with the IP address 192.168.10.1.
       ```

   -   `nameservers`: Configures DNS (name servers) settings. The `nameservers` section specifies the DNS (Domain Name System) servers that the device should use for domain name resolution.
       -   `addresses: [8.8.8.8, 8.8.4.4]`: Sets Google's public DNS servers (`8.8.8.8` and `8.8.4.4`) as the DNS servers to be used.

### Route Details

```
ip route

route -n
```
- Get route IP address
