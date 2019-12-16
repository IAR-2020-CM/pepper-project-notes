
# initialisation

To be able to communicate with pepper, you will have to configure a DHCP server

First install the `dhcp` packet

Configure dhcpd by editing the `/etc/dhcpd.conf` file

```
# dhcpd.conf
#
# Sample configuration file for ISC dhcpd
#

option domain-name-servers 9.9.9.9, 9.9.9.10;

subnet 10.142.0.0 netmask 255.255.0.0 {
    option routers 10.142.0.1;
    range 10.142.254.1 10.142.254.254;

    host pepper {
        hardware ethernet 00:1a:a0:2b:da:af;
        fixed-address 10.142.42.48;
    }
}
```

Add the `10.142.0.1` ip to your computer and set the interface up

```bash
sudo ip a add 10.142.0.1/16 dev <INTERFACE>
sudo ip l set <INTERFACE> up
```

Then start the dhcp daemon using :
```bash
sudo systemctl start dhcpd4.service
```

You will then have to enable ip transmission
```bash
# TODO: WRITE
```
