# Commands

|                Command                       |Description|
|----------------------------------------------|-----------|
|`R(config)# hostname Cisco`                   |Sets a host name to the current Cisco network device.|
|`R# show ip interface [type] [number] `       |Displays useful information about the configuration and status of the IP protocol and its services, on all interfaces. You can also use it also to know which interfaces are present on this router.|
|`R(config)# interface [interface_name]`       |Opens interface configuration mode.|
|`R(config-if)# ip [address] [ip-address mask]`|Assigns an IP address and a subnet mask.|
|`R(config-if)# shutdown`                      |Shuts down the interface.|
|`R(config-if)# no shutdown`                   |Brings up the interface.|
|`R# ping [IP]`                                |It’s a handy tool that you can use to test whether your computer can reach another device.|
|`R# telnet [IP]`                              | Opens a telnet session. |

### Configuring Telent Password

|  Password Type |Commands|Mode|
|----------------|--------|----|
|Telnet Password |`R1> en` <br> `R1# config t` <br> `R1(config)# line vty 0 4` <br> `R1(config-line)# password cisco` <br> `R1(config-line)# login`|`R2# telnet 10.0.0.2`  <br> `Trying 10.0.0.1 ...Open` <br> `User Access Verification` <br> `Password:`  <br> `R2>`|

### Removing Telent Password

|  Password Type |Commands|
|----------------|--------|
|Telnet Password |`R(config-line)# line vty 0 4` <br> `R(config-line)# no password`<br> `R(config-line)# no login`|
