# Mikrotik preparation and configuration

### Mikrotik WireGuard VPN module **[WISECP](https://puqcloud.com/link.php?id=78)** 

##### [Order now](https://puqcloud.com/index.php?rp=/store/wisecp-module-mikrotik-wireguard-vpn) | [Download](https://download.puqcloud.com/WISECP/Product/PUQ_WISECP-Mikrotik-WireGuard-VPN/) | [FAQ](https://faq.puqcloud.com/)

<p class="callout info align-center">Note: **Enter the following commands one by one and wait for the command to complete.**</p>

##### Check RouterOS version

<p class="callout warning">**Make sure that the version of RouterOS is 7+**</p>

```shell
system/package/print 
```

#####  

##### Enabling HTTPS Create your own root CA on your router

```
/certificate
add name=LocalCA common-name=LocalCA key-usage=key-cert-sign,crl-sign
```

#####  

##### Sign the newly created CA certificate

```
/certificate
sign LocalCA
```

##### Create a new certificate for Webfig (non-root certificate)

<p class="callout info">Note: as common-name=XXX.XXX.XXX.XXX You enter public IP adddress of the router.</p>

```
/certificate
add name=Webfig common-name=XXX.XXX.XXX.XXX
```

#####  

##### Sign the newly created certificate for Webfig

```
/certificate
sign Webfig ca=LocalCA 
```

#####  

##### Enable SSL (*www-ssl)* and specify to use the newly created certificate for Webfig

```
/ip service
set www-ssl certificate=Webfig disabled=no
```

#####  

##### Enable api-ssl and specify to use the newly created certificate for Webfig

```
 /ip service 
 set api-ssl certificate=Webfig disabled=no 
```

#####  

##### Enable WireGuard VPN server

[![image-1700908664667.png](https://doc.puq.info/uploads/images/gallery/2023-11/scaled-1680-/image-1700908664667.png)](https://doc.puq.info/uploads/images/gallery/2023-11/image-1700908664667.png)

#####   
Add IP address on Wireguard interface

[![image-1700908821470.png](https://doc.puq.info/uploads/images/gallery/2023-11/scaled-1680-/image-1700908821470.png)](https://doc.puq.info/uploads/images/gallery/2023-11/image-1700908821470.png)

##### Configuring NAT rules on the firewall

[![image-1700908941106.png](https://doc.puq.info/uploads/images/gallery/2023-11/scaled-1680-/image-1700908941106.png)](https://doc.puq.info/uploads/images/gallery/2023-11/image-1700908941106.png)