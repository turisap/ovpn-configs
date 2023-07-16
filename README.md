## Prepare

* install openvpn
```
apt install openvpn
```

* get the latest version of easyRSA [here](https://github.com/OpenVPN/easy-rsa/releases)
* download the archive
```
    wget https://github.com/OpenVPN/easy-rsa/releases/download/v3.1.5/EasyRSA-3.1.5.tgz
```
* extract the archive 
```
tar -xvzf EasyRSA-3.1.5.tgz
```

## Initialize Public Key Infrastructure

* `cd cd EasyRSA-3.1.5/`
* initialize pki `./easyrsa init-pki` 

Adjust EasyRSA vars

* `vim pki/vars`
* set the following vars to this values
```
set_var EASYRSA_KEY_SIZE 4096
set_var EASYRSA_CA_EXPIRE 3650
set_var EASYRSA_CERT_EXPIRE 825
```

Prepare CA
* build CA `./easyrsa build-ca nopass` 
* build server `./easyrsa build-server-full nopass <<server name>>`
* build test client `./easyrsa build-client-full test-client nopass`
* generate diffie hellman param `./easyrsa gen-dh`
* generate HMAC secret key `openvpn --genkey secret ta.key`


## Copy generated files

```
cd /etc/openvpn/server/<<server name>>
cp /root/EasyRSA-3.1.5/pki/ca.crt ./
cp /root/EasyRSA-3.1.5/pki/ta.key ./
cp /root/EasyRSA-3.1.5/pki/dh.pem ./
cp /root/EasyRSA-3.1.5/pki/issued/<<server name>>-server.crt ./
cp /root/EasyRSA-3.1.5/pki/issued/<<server name>>.key ./
mkdir ccd
```


## Handy tools

* check logs `tail -f /var/log/ovpn-<<server name>>.log`
* restart service `systemctl restart openvpn-server@<<server name>>`
* check status `systemctl status openvpn-server@<<server name>>`
# ovpn-configs
