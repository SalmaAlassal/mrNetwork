# VTY

- **VTY** stands for Virtual Teletype. It is a kind of virtual interface that is used to get CLI access of a Cisco Router or Switch over **Telnet/SSH.** 

- All the connections are remotely over the network, so there is no hardware associated with it.

## Line VTY Command 

**Example:** `R1(config)# line vty 0 4`

It will open 5 virtual interfaces, i.e. (0,1,2,3,4) for remote access. That means, 5 different administrators/connections can access the Cisco Router/Switch at the same time using Telnet or SSH.

# Telnet

- Telnet operates using **TCP** **port 23** and it was designed specifically for LANs.

- Telnet is **not a secure** communication protocol because it does not use any security mechanism and transfers the data over network/internet in a **plain-text** form including the passwords and so any one can sniff the packets to get that important information.

# Telnet Password

**Configure Router 1**

```
Router>enable
Router#show ip interface
Router#configure terminal 
Router(config)#hostname R1
R1(config)#interface fastEthernet 0/0
R1(config-if)#ip address 10.0.0.1 255.255.255.252
R1(config-if)#no shutdown
```

 **Configure Router 2**
 
 ```
Router>enable
Router#show ip interface
Router#configure terminal 
Router(config)#hostname R2

R2(config)#interface fastEthernet 0/0
R2(config-if)#ip address 10.0.0.2 255.255.255.252  --> Assign an IP address to the interface
R2(config-if)#no shutdown 

R2(config-if)#do ping 10.0.0.1    ---> In order to verify the connectivity
R2(config-if)#exit

R2(config)#enable password 123
R(config)#enable secret cisco2

R2(config)#line vty 0 4
R2(config-line)#password cisco
R2(config-line)#login

```

**As shown above :**
- the enable password was set to 123 
- the enable secret was set to cisco2
- the telnet  password was set to cisco


To verify your vty line password configuration you can telnet to your local interface to initiate a telnet session as shown below;

```
R1#telnet 10.0.0.2 

Trying 10.0.0.2 ...Open
User Access Verification
Password: 

R2>enable
Password: 
R2#
```


**Note that** if you didn't configure “enable” password and try to gain privileged level access. You’ll immediately notice that you’ll be prompted for an “enable” password in which 
case none is set so therefore you cannot gain privileged level access.

```
R1#telnet 10.0.0.2 

Trying 10.0.0.2 ...Open
User Access Verification
Password: 
R2>enable
% No password set

R2>
````

**So , configure an enable password and secret for the Cisco router to gain privileged level access to the device via telnet.**

---------------------------------------------
