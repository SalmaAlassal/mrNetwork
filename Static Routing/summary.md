
|Command          | Description |
|-----------------|-------------|
|`R#show ip route`| To show the router's routing table.|
|`R(config)# ip route Destination_Network Subnet_Mask <Next_Hop_IP_Address> [AD]` <br> Or <br> `R(config)# ip route Destination_Network Subnet_Mask <Exit interface> [AD]`|To configure Static Route.|
|`R(config)#ip route 0.0.0.0 0.0.0.0 [Next_Hop_IP_Address]` <br> Or <br> `R(config)#ip route 0.0.0.0 0.0.0.0 [Exit interface]`| To configure the default route.|
|`R(config)#int loopback pNumber]`|To configure loopback interface.|
