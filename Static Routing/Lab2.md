# Floating Static Route (Lab 2)

Floating static routes are the routes whose default administrative distance is changed manually with a higher admnistrative distance value. The aim of this higher administrative distance is to use this floating static route as a backup route. Because a floating static route with an higher administrative distance value is not selectedas best path. Instead of it another route is selcted. And whenever this better path fails, then floating route is used as Best Path.

**Syntax:** 

- `R(config)# ip route Destination_Network Subnet_Mask <Exit interface> [AD]`  
         
or 

- `R(config)# ip route Destination_Network Subnet_Mask <Next_Hop_IP_Address> [AD]`

![Floating Static Route](imgs/Lab2.png)

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
R1(config-if)#no shut

R1(config-if)#int f1/0
R1(config-if)#ip address 11.0.0.1 255.255.255.0
R1(config-if)#no shut

R1(config-if)#do show ip route
..
..

      10.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        10.0.0.0/24 is directly connected, FastEthernet0/0
L        10.0.0.1/32 is directly connected, FastEthernet0/0
      11.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        11.0.0.0/24 is directly connected, FastEthernet1/0
L        11.0.0.1/32 is directly connected, FastEthernet1/0

```

> It is a normal behavior on IOS 15 to see 2 subnets because it is representing the real subnet mask (C = Connected) and showing the IP as host (L = Local).



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

R2(config-if)#int f1/0
R2(config-if)#ip address 11.0.0.2 255.255.255.0
R2(config-if)#no shut

R2(config-if)#int loop 2
R2(config-if)#ip address 2.2.2.2 255.255.255.255

R2(config-if)#do show ip route
..
..
      2.0.0.0/32 is subnetted, 1 subnets
C        2.2.2.2 is directly connected, Loopback2
      10.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        10.0.0.0/24 is directly connected, FastEthernet0/0
L        10.0.0.2/32 is directly connected, FastEthernet0/0
      11.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        11.0.0.0/24 is directly connected, FastEthernet1/0
L        11.0.0.2/32 is directly connected, FastEthernet1/0

```


### Static Routes


```
R1(config)#ip route 2.2.2.2 255.255.255.255 10.0.0.2
R1(config)#ip route 2.2.2.2 255.255.255.255 11.0.0.2 2

R1(config)#do show ip route
..
..

      2.0.0.0/32 is subnetted, 1 subnets
S        2.2.2.2 [1/0] via 10.0.0.2
      10.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        10.0.0.0/24 is directly connected, FastEthernet0/0
L        10.0.0.1/32 is directly connected, FastEthernet0/0
      11.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        11.0.0.0/24 is directly connected, FastEthernet1/0
L        11.0.0.1/32 is directly connected, FastEthernet1/0

```

If interface f0/0 has shut down it will go through the backup path ( 11.0.0.2)


```
R1(config)#int f0/0
R1(config-if)#shutdown
R1(config-if)#


R1(config-if)#do show ip route
..
..
      2.0.0.0/32 is subnetted, 1 subnets
S        2.2.2.2 [2/0] via 11.0.0.2
      11.0.0.0/8 is variably subnetted, 2 subnets, 2 masks
C        11.0.0.0/24 is directly connected, FastEthernet1/0
L        11.0.0.1/32 is directly connected, FastEthernet1/0
```

> Note that if a router sent message to another router through a specific path, it's not  must to send its reply through the same path.
