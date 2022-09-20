# RIP Basic Configurations (Lab 1) 

![Lab 1](imgs/Lab1.png)

## Configure Routers

### R1

```
Router>en
Router#config t
Router(config)#line console 0
Router(config-line)#logging syn
Router(config-line)#hostname R1

R1(config)#int f0/0
R1(config-if)#ip address 10.0.0.1 255.255.255.0
R1(config-if)#no shutdown

R1(config-if)#int loop 1
R1(config-if)#ip address 1.1.1.1 255.255.255.255
```

### R2

```
Router>en
Router#config t
Router(config)#line console 0
Router(config-line)#logging syn
Router(config-line)#hostname R2

R2(config)#int f0/0
R2(config-if)#ip address 10.0.0.2 255.255.255.0
R2(config-if)#no shut

R2(config-if)#int loop 2
R2(config-if)#ip address 2.2.2.2  255.255.255.255
```

### `R#show ip protocols`

This command displays a summary of configured routing protocol information. It is useful for quickly verifying how routing protocols are configured.

### R2

```
R2#show ip protocols
*** IP Routing is NSF aware ***

Routing Protocol is "application"
  Sending updates every 0 seconds
  Invalid after 0 seconds, hold down 0, flushed after 0
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Maximum path: 32
  Routing for Networks:
  Routing Information Sources:
    Gateway         Distance      Last Update
  Distance: (default is 4)
```
**Nothing shows up as we haven’t configured any routing protocol yet.**

------------------------------------------

#  Rip Configurations

`Router(config)#router rip`

`Router(config-router)# network [directly-connected-classful-network-address]`

It enables the sending and receiving of RIP updates for interfaces that belong to the specified network.

### R1

```
R1(config)#router rip
R1(config-router)#network 10.0.0.0
R1(config-router)#network 1.1.1.1

R1(config-router)#do show run | section rip
router rip
 network 1.0.0.0
 network 10.0.0.0
R1(config-router)#
```

> Only classful routing supported since RIPv1 does not send subnet mask, so it will consider `1.1.1.1` as class A which use a default subnet mask of `255.0.0.0 (/8)` so the network address will be `10.0.0.0` .
 It means if we have another network (1.2.3.4) on R1, the RIP protocol will be automatically run on it. 
 
### R2

```
R2(config)#router rip
R2(config-router)#network 10.0.0.0
R2(config-router)#network 2.0.0.0
```

### Verify

### R1

```
R1#show ip route

Gateway of last resort is not set

      1.0.0.0/32 is subnetted, 1 subnets
C        1.1.1.1 is directly connected, Loopback1
R     2.0.0.0/8 [120/1] via 10.0.0.2, 00:00:15, FastEthernet0/0
      10.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        10.0.0.0/24 is directly connected, FastEthernet0/0
L        10.0.0.1/32 is directly connected, FastEthernet0/0

```
Note that distance information and the route metric appear in the output of `show ip route` inside square brackets with the distance information first, followed by a “/” and the route metric: [distance/metric]. E.g, `R     2.0.0.0/8 [120/1] via 10.0.0.2, 00:00:15, FastEthernet0/0` → 120 = AD, 2 = Metric value




### R2
```
R2#show ip route

Gateway of last resort is not set

R     1.0.0.0/8 [120/1] via 10.0.0.1, 00:00:03, FastEthernet0/0
      2.0.0.0/32 is subnetted, 1 subnets
C        2.2.2.2 is directly connected, Loopback2
      10.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        10.0.0.0/24 is directly connected, FastEthernet0/0
L        10.0.0.2/32 is directly connected, FastEthernet0/0
R2#
```

`R     1.0.0.0/8 [120/1] via 10.0.0.1, 00:00:03, FastEthernet0/0` :

- `00:00:03` → Update timer : Every 30 seconds IP RIP sends a complete copy of its routing table. 

> Notice that the update time shouldn’t exceed 30 sec ( [0,30] ) and if it exceeds that time, this is an indicator of a problem in the update between the two routers.


### Test Connectivity

If a network appeared in routing table, it doesn't mean that the connection is good because **you can reach a network that can't reach you**, so always use `ping` command.

```
R1#ping 2.2.2.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 2.2.2.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 88/92/96 ms
```

-----------------------------------------------

# RIP Versions

##  Default version

```
R1#show ip protocols
*** IP Routing is NSF aware ***

Routing Protocol is "application"
  Sending updates every 0 seconds
  Invalid after 0 seconds, hold down 0, flushed after 0
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Maximum path: 32
  Routing for Networks:
  Routing Information Sources:
    Gateway         Distance      Last Update
  Distance: (default is 4)

Routing Protocol is "rip"
  Outgoing update filter list for all interfaces is not set
  Incoming update filter list for all interfaces is not set
  Sending updates every 30 seconds, next due in 19 seconds
  Invalid after 180 seconds, hold down 180, flushed after 240
  Redistributing: rip
  Default version control: send version 1, receive any version
    Interface             Send  Recv  Triggered RIP  Key-chain
    FastEthernet0/0       1     1 2
    Loopback1             1     1 2
  Automatic network summarization is in effect
  Maximum path: 4
  Routing for Networks:
    1.0.0.0
    10.0.0.0
  Routing Information Sources:
    Gateway         Distance      Last Update
    10.0.0.2             120      00:00:16
  Distance: (default is 120)
```

> Note that : Default version control: send version 1, receive any version

## Change Versions

### To change the configuration to send and receive version 1 only

```
R1(config)#router rip
R1(config-router)#version 1
```
**The router now sends and receives only version 1**

### To change the configuration to send and receive version 2 only

```
R2(config)#router rip
R2(config-router)#version 2
```
> This may cause a problem as version 1 and version 2 is not compatible with each other.

Once we do this, **R1 will no longer receive any updates from R2**. At this moment the **invalid** and **flush timer** will increase. In the first 180 seconds, nothing will happen:

```
R1#show ip route rip
..
..

R     2.0.0.0/8 [120/1] via 10.0.0.2, 00:01:52, FastEthernet0/0


R1#ping 2.2.2.2
Type escape sequence to abort.
Sending 5, 100-byte ICMP Echos to 2.2.2.2, timeout is 2 seconds:
!!!!!
Success rate is 100 percent (5/5), round-trip min/avg/max = 20/27/32 ms


R1#show ip route rip
..
..

R     2.0.0.0/8 [120/1] via 10.0.0.2, 00:03:00, FastEthernet0/0
```

**After 180 seconds** the invalid timer will have expired and the **holddown timer starts**.

```
R1#show ip route rip
..
..

R     2.0.0.0/8 is possibly down, routing via 10.0.0.2, FastEthernet0/0
```

The `2.0.0.0/8` will remain in the routing table of R1, but it says it’s **“possibly down”**. 

60 seconds later after the route went in holddown , the `2.0.0.0/8` is now finally gone from the routing table…

```
R1(config-router)#do show ip route rip
..
..

Gateway of last resort is not set
```

**now the network `2.2.2.2` is unpingable**

### To return to the default version
 
 `R1(config-router)#no version`


### what if we configure R1 to use the default which is sending version 1 and receive any version, and hard code R2 to use version 2?

- R1 will receive all the updates from R2 (`2.0.0.0` pingable)
- R2 will not accept any updates from R1 (`1.0.0.0` unpingable)

-----------------------------------------------------------------------------------

# Troubleshooting

## Debug Command

- Cisco IOS **Show commands** can tell you many things about what is going on with your router or switch, but they can’t tell you everything. For example, Show commands cannot tell you when routes drop in or out of the routing table, why an ISDN line failed to connect, whether a packet really went out the router, or what ICMP error code was received. On the other hand, Cisco IOS Debug commands can tell you all these things, and more.

- Debug commands have the benefit of providing information in “**real time**” (or dynamically). This is contrary to Show commands that just take a snapshot in time and display the results on your console (somewhat static results). This real-time difference can be very helpful in diagnosing problems.

- The debug operation **takes a lot of CPU resources** (it may crash the device!) and should not be used often in production environments. It is meant to be used as a troubleshooting tool for only a short period of time

|Command                          |Description                                              |
|---------------------------------|---------------------------------------------------------|
|`R1#debug ip icmp`               |Enable debugging only for the ICMP events (such as pings)|
|`R1#no debug ip icmp`            |To disable debugging of the ICMP events                  |
|`R1#debug all`                   |Enable debugging of everything happening on your device  |
|`R1#undebug all` <br> `R1#u all` | To disable debugging of everything                      |
|`Router# show debug`             |To verify what debugging is enabled                      |


- The output from whatever type of debug is enabled will be sent to wherever the Cisco IOS logging system tells that output to go. Either you will receive the output on your screen, it will go to the buffered log on the router, or it will go to a syslog server across the network (or all of these).
  
  - To see what level the various outputs are set to and where the output will go : `Router# show logging` 

[More examples](https://www.vskills.in/certification/tutorial/debug-command-and-rip/)

-----------------------------------------------------------------------

### Let's troubleshoot our problem now :

```
R1#debug ip rip
RIP protocol debugging is on

*Apr 28 18:52:52.531: RIP: sending v1 update to 255.255.255.255 via Loopback1 (1.1.1.1)
*Apr 28 18:52:52.531: RIP: build update entries
*Apr 28 18:52:52.535:   network 10.0.0.0 metric 1
*Apr 28 18:53:09.119: RIP: sending v1 update to 255.255.255.255 via FastEthernet0/0 (10.0.0.1)
*Apr 28 18:53:09.119: RIP: build update entries
*Apr 28 18:53:09.119:   network 1.0.0.0 metric 1
*Apr 28 18:53:13.539: RIP: ignored v2 packet from 10.0.0.2 (illegal version)   ---> once the problem appear stop debugging

R1#no debug ip rip
RIP protocol debugging is off
R1#
```

**Now we can fix it :**

```
R1(config)#router rip
R1(config-router)#version 2
```

------------------------------------------------------------------------------

# Important Note

If you use **RIPv2**, turn off automatic summarization : `R(config-router)#no auto-summary`

We will discuss the reason later.


### R1
```
R1(config-router)#do show ip route
...
...
      1.0.0.0/32 is subnetted, 1 subnets
C        1.1.1.1 is directly connected, Loopback1
R     2.0.0.0/8 [120/1] via 10.0.0.2, 00:00:12, FastEthernet0/0
      10.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        10.0.0.0/24 is directly connected, FastEthernet0/0
L        10.0.0.1/32 is directly connected, FastEthernet0/0


R1(config-router)#no auto-summary

R1(config-router)#do show ip route
...
...

      1.0.0.0/32 is subnetted, 1 subnets
C        1.1.1.1 is directly connected, Loopback1
      2.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
R        2.0.0.0/8 [120/1] via 10.0.0.2, 00:00:22, FastEthernet0/0
R        2.2.2.2/32 [120/1] via 10.0.0.2, 00:00:02, FastEthernet0/0
      10.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        10.0.0.0/24 is directly connected, FastEthernet0/0
L        10.0.0.1/32 is directly connected, FastEthernet0/0
```

### R2
```
R2(config-router)#no auto-summary
```

------------------------------------------------------------------------------
------------------------------------------------------------------------------