# Commands

|                Command               |Description|
|--------------------------------------|-----------|
|`R(config)#ip domain name [name]`     |Set up a domain name for generating SSH keys.|
|`R(config)#crypto key generate rsa`   |Generate RSA public and private keys |
|`R(config-line)#transport input ssh`  |To enable only the SSH access to a device.|
|`R#show crypto key mypubkey rsa`      |To view the configured public key.|  


### Setting up SSH Only

```
R#config t
R(config)#int f0/0 
R(config-if)#ip add 10.0.0.1 255.255.255.252
R(config-if)#no sh 
R(config-if)#exit

R(config)#username salma password abc

R(config)#ip domain name cisco.com

R(config)#crypto key generate rsa

R(config)#line vty 0 4
R(config-line)#login local
R(config-line)#transport input ssh
```