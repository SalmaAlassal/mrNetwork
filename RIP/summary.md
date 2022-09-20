# RIP Configurations

|Commands|Description|
|--------|-----------|
|`R(config)#router rip` <br> `R(config-router)#network [directly-connected-classful-network-address]`|Enable RIP and specify those networks that should be advertised using RIP.|
|`R1(config-router)#no network 2.0.0.0`  |To stop the network `2.0.0.0` from being advertised.            |
|`R(config-router)#version 1` <br> or <br> `R(config-router)#version 2` |To change the configuration to send and receive version 1 or 2 only|
|`R(config-router)#no version`           |To return to the default version.                               |
|`R(config-router)#maximum-path [Number]`|To change the number of maximum path in equal cost load balance.|
|`R1#show ip route rip`                  |To display only RIP entries in the routing table.               |

## Turns on RIP Authentication

|Command                                                                        |Description                         |
|-------------------------------------------------------------------------------|------------------------------------|
|`R(config)#int f0/0` <br> `R(config-if)#ip rip authentication key-chain [name]`|To turn on clear text authentication|
|`R(config)#int f0/0` <br> `R(config-if)#ip rip authentication mode md5`        |To turn on MD5 authentication       |

--------------------------------------------------------------

# Creating a Keychain

|Command                                   |Description                                                 |
|------------------------------------------|------------------------------------------------------------|
|`R(config)#key chain [name]`              | Create the keychain and enters keychain configuration mode |
|`R(config)#no key chain [name]`           | Remove the keychain and any keys that the keychain contains|
|`R(config-keychain)#key [Number]`         | Create the key ID                                          |
|`R(config-keychain-key)#key-string [pass]`| Create the key password                                    |
|`R#show key chain`                        | Display the keychain configuration                         |
|`R#show key chain CCNA`                   | Display CCNA keychain                                      |
|`R(config-keychain-key)#accept-lifetime [start-time] [end-time]`|Defines the accept lifetimes of a key |

--------------------------------------------------------------

# Configure Backup Static Route

To configure R to see the `2.2.2.2/32` network using static route, we will increase the Administrative Distance value:

`R(config)#ip route 2.2.2.2 255.255.255.255 11.0.0.2 121`

# `R#show ip protocols`

This command displays a summary of configured routing protocol information. It is useful for quickly verifying how routing protocols are configured.


# `R#traceroute 10.0.0.1` 

This command is used to identify the path used by a packet to reach its target. It identifies all the routers in the path from the source host to destination host, and it can be useful when troubleshooting network problems. 

--------------------------------------------------------------

## Debug Command

|Command                        |Description                                              |
|-------------------------------|---------------------------------------------------------|
|`R#debug ip RIP`               |Enable debugging only for the RIP packets.               |
|`R#no debug ip RIP`            |To disable debugging of the RIP packets.                 |
|`R#debug all`                  |Enable debugging of everything happening on your device. |
|`R#undebug all` <br> `R1#u all`|To disable debugging of everything.                      |
|`R# show debug`                |To verify what debugging is enabled.                     |


--------------------------------------------------------------
