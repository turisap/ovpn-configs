## Tutorial
* [how to setup openvpn on Debian](https://www.digitalocean.com/community/tutorials/how-to-set-up-an-openvpn-server-on-debian-10)
* [how to setup Debian server with firewall](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-debian-10)
* [how to setup Pihole with OpenVPN](https://www.digitalocean.com/community/tutorials/how-to-block-advertisements-at-the-dns-level-using-pi-hole-and-openvpn-on-ubuntu-16-04)


## Troubleshooting
* if Pihole installation does not ask for a static IP and gateway IP addresses check if this file is present `/etc/dhcpcd.conf` and create an empty one if not.
* if connection hangs after pointing OpenVPN access server to Pihole instance check if the following configurations are present  in `server.conf`
```
topology subnet
push "redirect-gateway def1 bypass-dhcp"
push "dhcp-option DNS 10.8.0.1"
```

## Handy tools

* check logs `tail -f /var/log/ovpn-<<server name>>.log`
* restart service `systemctl restart openvpn@<<server name>>`
* check status `systemctl status openvpn@<<server name>>`

## Express setup without CA
* download the installation script
```shell
wget https://github.com/Nyr/openvpn-install/raw/master/openvpn-install.sh
chmod 755 openvpn-install.sh
```

At this moment, the script has a bug. The bug is a deprecated option `openvpn --genkey --secret` which I fixed manually to `openvpn --genkey secret`

* run the script and follow the installation wizard

```shell
./openvpn-install.sh
```
